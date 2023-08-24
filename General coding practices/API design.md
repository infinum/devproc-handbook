Designing an API is a fluid process which requires input from both the producer and consumer. We're fortunate in the sense that we mostly work on APIs which are used internally amongst our teams. That means that there is plenty of place and will for compromises when it comes to designing how resources are exposed.
### Planning API changes
  The producer and consumer of the API should sit down together and inspect a feature request. They should try to answer the following questions for each and every UI component on a screen:

  - what type of resource is displayed in a collection
  - which endpoints will serve this resource data
  - how will labels map to resource attributes
  - how will the collection be sorted by default, what are the additional sort options
  - how will the collection be filtered by default, what are the additional filter options
  - what is a sensible page size
  - how will pagination behave
  - which attributes should be included in search queries

  The pairing of the producer and consumer point of view will often come up with questions that may have been forgotten in the design or requirement collection phase.

  The agreement should be noted down for future reference. The producers and consumers will be able to use this document to help them split out smaller technical tasks. Design (e.g. Figma) annotations are also particularly useful for presenting this data visually. Each UI element can have a comment attached to it for easier reference.

### Trust, but verify
  Keeping an API healthy doesn't require just careful change planning beforehand, but also regular checkups before and after a feature deployment.

  The API usage document is an agreement we make at a point in time with the knowledge that we have then. Requirements often change during the integration phase as we find new constraints. The initially defined API might have been perfect, but changes during development could have easily turned it into a performance problem waiting to blow up. The producers and consumers of the API should review the final feature implementation **together**, **before** a feature is released. Checking which screens use which endpoints, how often those are called and what their page sizes are is an easy check to make.

  Deployment of an API change does not mark the end of our part, but the start of the most important one.

  > "Production is the only environment that matters." - Charity Majors

  The combinatorial explosion of thousands of users using our application in hundreds of different ways will expose the smallest of problems in our code. It is our job as producers of the API to keep an eye on things. There are two questions we should be asking ourselves periodically:

  1. How is the API actually being used by consumers?
  2. How is it performing?

  Some form of application level performance monitoring should be included in every project. We should periodically observe at least

  - rate of requests to an endpoint
  - 99th percentile response times ([don't bother with averages](https://www.infoq.com/presentations/latency-response-time/))
  - errors and error rates

## JSON:API
  We mostly follow the [JSON:API](https://jsonapi.org) specification on projects where we are producing the API. It is not a perfect choice (see the following chapters), but it has historically brought us benefits on multiple fronts.

  - There is no bikeshedding about response formatting. The specification is clearly written and covers a big chunk of our use cases. We can focus our time on solving business problems instead of coming up with yet another way of formatting resource and relationship data in JSON.
  - The specification is written with a lot of useful features in mind - **compound documents**, sparse fieldsets, pagination, sorting, filtering and scoping. This allows us to rapidly produce performant content-rich applications.
  - We are using one standard of integration on most projects across the frontend, mobile and backend teams. Consequently we have a lot of established tooling. This allows up to reduce project setup time and share a big collection of learned experiences. Most times somebody else has already encountered a specific problem and solved it.

### Has many relationships
  Compound documents are one of the strategies that JSON:API provides for reducing the number of HTTP requests that an API consumer has to make. The API can respond with the requested resource and its related resources inside a single response with no need for a separate request.

  The consumers of the API only need to make 1 requests to fetch a multitude of different resources (e.g `/posts?include=comments`). They don't have to handle consecutive API calls and think about asynchronous local state. They send one request and get all the resources needed to show the UI.

  The compound documents are fetched via a relationship (`comments`) on the base resource (`post`) serializer. These relationships can connect a base resource to either multiple related resources (a post has many comments) or a single related resource (a post has one author).

  This type of API integration is attractive at first glance and seems to offer no downsides. It may be acceptable for some smaller projects, but it is **actively discouraged** due to a number of issues that it causes in the long term.

### Collection issues
  Let's explore these issues on a simple example of 3 related resources

  - **Post** (*title*, *content*, *created_at*) which has many comments
  - **Comment** (*content*, *post_id*) which belongs to exactly one post and has many reports
  - **Report** (*message*, *comment_id*) which belongs to exactly one comment

#### Pagination
Requirement: a post detail page that shows its comments

Endpoint: `/posts?include=comments`

The Post resource includes **all** (*0..n*) related comments. This might work great locally on a smaller data set, but what happens when a Post on production gets 100 comments? Not only will the Post detail page be slower due to a bigger payload size and slower response time, the index page will be even worse since the problem will be repeated for each Post in the collection. The database and the producer application layer have to calculate the whole result set of **each** has many relationship **every time**, even if you only need the first 5 comments.

You may be able to guess the maximum number of comments a Post will have and be safe for a while, but once you start nesting has many relationships (e.g. `/posts?include=comments.reports`) on any given endpoint the number of serialized resources will grow without you even realising it. We never know less than we know right now and we shouldn't shoot ourselves in the foot. Use pagination from the start and you won't run into any issues.

> A good shepherd of the API will use pagination for all resources and always request the smallest possible page size that fits the UI. Additional elements can be loaded later when the user actually needs them.

Preferred endpoints:

```
/posts?page[size]=10&page[number]=1
```

```
/posts?page[size]=10&page[number]=1
```

```
/comments?filter[post_id]=1,2,3&page[size]=10&page[number]=1
```

```
/reports?filter[comment_id]=1,2,3&page[size]=10&page[number]=1
```

#### Filtering

Initial Requirement: a page that displays posts and their comments

Endpoint: `/posts?include=comments`

has many relationships don't support additional filters. The relationship that's exposed on the API has exactly one subset of data and the consumers can't request another one from the API.

We get a feature request for showing only a post's pinned comments on a new page. One option is to expose yet another filtered has many relationship (e.g. `Post.pinned_comments`) which will only be accessible through the Post resource. That's clunky, but still doable. The next feature request comes up, we need just pinned comments on the homepage, not related to any specific post.

Exposing one-off has many relationship quickly becomes a maintenance burden, especially once you need to apply multiple optional filters on a resource.

> A good shepherd of the API will expose filters on the endpoint of that specific resource that you want a subset collection of. This enables fetching page specific collections which can be composed of multiple optional filters.

Preferred endpoints:

```
/comments?filter[post_id]=1,2,3&filter[pinned]=true
```

```
/comments?filter[pinned]=true
```


#### Sorting

Initial Requirement: a page that displays posts and their comments ordered by the **created_at attribute ascending**

Endpoint: `/posts?include=comments`

has many relationships don't support additional sort options. The relationship that's exposed on the API has exactly one order of data and the consumers can't request another one from the API.

We get a feature request for showing post comments sorted by **created_at descending** on a new page. The only option we have is exposing yet another sorted has many relationship (e.g. `Post.comments_created_at_desc`).

The downside here is similar to filtering, adding per page relationships and maintaining them is a burden. What will happen when you'll need a custom filtered has many that needs to be sorted in two different ways?

> A good shepherd of the API will expose sort options on the endpoint of that specific resource that they want sorted. This enables fetching of page specific sorted collections.

Preferred endpoints:

```
/comments?filter[post_id]=1&sort=created_at
```

```
/comments?filter[post_id]=1&sort=-created_at
```

### Performance issues

One of the core benefits of has many relationship inclusions is accessing a resource and all of its connected resources in one request. While this is much simpler to deal with from a consumer side it is a big performance burden on the producer.

Let's look at a real world request.

`/lectures/113?include=chapters,articles,authors,authors.profile,transcripts.language,speakers,references,subjects,event,subsequent_lectures.event,subsequent_lectures.speakers,similar_lectures.event,similar_lectures.speakers`

The primary **Lecture** resource contains has many relationships for

- `chapters`
- `articles`
- `authors`
- `transcripts`
- `speakers`
- `subjects`
- `subsequent_lectures` (Lecture)
- `similar_lectures` (Lecture)

and some of their **nested** belongs_to or has many relationships as well

- `authors.profile`
- `transcripts.language`
- `subsequent_lectures.event`
- `subsequent_lectures.speakers` (has many)
- `similar_lectures.speakers` (has many).

The response of the mentioned request was 80KB big and took a full second to generate.
The database query count reached 241 due to the chain of has many relationships.
We shaved it down to 200ms and 15KB just by removing some of the nested includes.

Similar innocent looking requests with deep "hidden" nesting have ballooned to 500KB of JSON.
If you expose a has many relationship to the consumer it will be (ab)used in places where you don't expect, long after it's introduced.

This bloating of the returned collection is felt by the user since it slows all the steps in the process

1. Querying the database
2. Collection serialization
3. Download of the response
4. Deserialization of the response
5. Processing of the result on the consumer side

Users shouldn't wait seconds to see some actionable content in an application. Firing separate simpler requests is not only a performance win on the producer side, but also on the consumer side. The UI doesn't have to be blocked while the world is downloading. The most important parts of the UI can be loaded first, with the rest of the data coming later.

#### Endpoint Optimizations
The fact that any endpoint can include any directly or transiently connected resource means that there is no sane way for the API producer to optimize an endpoint.

There is no magic that can optimize both `/lectures` and `/lectures?include=chapters,articles,authors` and make them both fast and efficient at the same time.

If we use filters and separate endpoints

- `/lectures`
- `/chapters?filter[lecture_id]=1`
- `/articles?filter[lecture_id]=1`,`authors`

for fetching data we can optimise each resource call separately and fit them to each use case. Simple requests to different endpoints are much easier to optimise than 1 big request that fetches the whole world through includes.

#### Caching

The ability to fetch any type of resource from any endpoint means that the API producer has no good options for response caching. The fact that a **Comment** resource can be returned on multiple endpoints (e.g. `/posts?include=comments`, `/comments`) means that every resource change requires a cache clear on all the endpoints. The cache clearing can't be granular, which means the cache hit ratio plummets. Because of the excessive response sizes and response times each cache miss is even more costly.

### Migrating from has many relationship inclusions
The difficulty of migrating from relationship inclusions to filters, sorts and pagination varies by product, but it is usually very painful.

The move on the producer side is trivial, since filters are simple to implement. The producer just needs to keep exposing both the has many relationship and the filter until all the consumers migrate. After that the has many relationship can be removed.

The real pain comes from the consumer side. **All** usages of the has many relationships need to be evaluated and migrated. The migration is also very likely to expose hidden coupling of data if the consumer keeps any internal state between requests.

Consumers that expect to receive all the information in one request are usually hard to migrate over to filters. Handling state and displaying partial components of the page is not trivial and requires a conceptual shift. In some cases that might lead to an expensive rewrite.

#### Exceptions
Using has many relationship inclusions may be necessary in some cases. Some UI designs or technical requirements may require you to reach for this sharp knife.

When the time comes you need to make an informed decision. If a subset of the following conditions holds true for your situation then you should consider this pattern

- you don't have time to do the right thing on the producer/consumer side
- you will have the budget and or client support to move to filters later
- the parent resource is only going to be used on one page (e.g. a feature specific has many)
- you are absolutely sure you won't need different sorting/filtering or paginating of that resource elsewhere
- you (or your users) don't care about performance (shame!)
- you can count the number of existing exceptions in the project using one hand

#### Collections with sorted has many relationships
Some UI requirements might also warrant usage of has many serializer relationships as other options might be even more damaging.

Let's assume you need to show a list of 20 books per page, with each element containing the book title and it's authors sorted by their last name. The naive solution would be to use `/books` and `/authors=filter[book_id]=1,2,3&sort=last_name`, but that does not fit the requirement. That pair of endpoints would sort authors of all books on that page together. There are several possible solutions:

  - Fetching `/authors?filter[book_id]=1&sort=last_name` for each book individually. That would trigger 20 additional requests per page. The responses might be easily cachable but they will cause considerable load on the application, especially in usecases where users often scroll through the whole collection.
  - Fetching `/authors?filter[book_id]=1,2,3&sort=last_name` and grouping each books's authors in memory on the client side. This may not always be possible
  - Fetching authors through `/books?include=sorted_authors`. This solution might be acceptable if
      - the number of authors per book is guaranteed to be low (or can be aggressively limited)
      - the API producer can produce an efficient query
      - the has many relationship is exposed in a separate opt-in serializer

## TL;DR:
If you're working on a project that is actively developed then you will end up using filters sooner or later.
The has many relationship inclusion may be ok for the first resource page you implement and may even save you some time. The minute you get a new feature request that requires pagination, filtering or sorting of an existing resource you will need to migrate from inclusions to multiple requests anyway.

We know better, has manys are simply not adequate. Save yourself (and the client) the pain of migration from inclusions and design the producer and consumer with filters from the start. Don't take on this technical debt if you don't have to.
