Projects with a well defined strategy and workflow often come with a set of wireframes, or even design pages prepared in [Figma](www.figma.com). These give client-side developers easy access and insight into the properties of frontend components that are rendered on the page, as well as their style.

### Think outside the box
More often than not, the design focuses on these aspects of the data represented on the page:

* style - colors, font, size, position, etc...
* information - what data is relevant for the user

Even though the design may showcase mocked data that's relevant for the project's domain, there is usually plenty of cases left to uncover, which potentially lead to changes of the acceptance criteria and therefore the estimation.

Our job is to carefully analyse the pages and think about the real-world cases that can occur in production:

* **available data** - first of all, check if the data is available in our database. Do we need to add a new column, or a completely new table (or sets thereof)? Where will that data come from (admin dashboard, external API, Excel sheets, visitors of the app)?
* **performance** - caching, pagination, custom indexes, need for database views etc...
* **HTTP method ratio** - will the page mostly dispatch GET requests, or also POST requests? The answer might change your way of thinking and how to implement the API endpoints
* **different users, various data** - there's usually a lot of duplicated data in the design, imagine that it's not, how would the page behave with more data, or less, or when there's no data at all?
* **roles and permissions** - does this page work for all users the same way? Think about the app's policies and if some users have a higher permission level than the one used during the design phase
* **related data behaviour** - can a user delete something from the page? How will that action affect associated data in the database?

### Go step by step
Keep in mind that developing small functional slices needed now, and then enhancing that functionality later is less risky than designing and developing the more complex functionality all at once. Don't be afraid of a large number of PRs. If your task entails creating a new table, with its models, controllers and units that do some work, separate your PRs into small chunks that are extremely easy to code review and maintain separately, and deploy these small units when they are confirmed as functional. That way you also gain the benefit of working simultaneously on a user story, but on different aspects (e.g.: API, admin dashboard, external API, background jobs).

There will be times when you start developing and stumble upon something that hasn't been anticipated by the framework. Watch out for painting yourself into a corner. If possible, experiment to identify such technical risks as early as possible. The wireframes help in preventing this scenario, but to maximize your odds, you can contact the client-side developers and do an API design-first approach, also called a walking skeleton.

### Walking skeleton
In cases a user story is complex in nature, or a bunch of data is represented on the page, doing API design-first results in a framework that defines a subset of usages from inputs to outputs. This framework is often represented as a collection of:

1. **API endpoints** - URLs, the HTTP methods, some custom headers
2. **Response payloads** - JSON files containing the required objects represented as hashes of key-value pairs or more complex objects that have the data shown on the pages (__outputs__)
3. **Request payloads** - same as response payloads, but these are aimed to be sent from the client applications to the server, often doing a change in the database or triggering an additional process, such as dispatching emails, generating files etc (__inputs__)

It's best to start with the output of the system. Elaborations can be hung on this framework to expand the range of usage. If there is a hard deadline, then prioritization of the most common and most critical use cases can reduce the risks of missing it.

Contact your fellow client-side developer and tackle this task together. Expect the first meeting to spawn dozens of questions for the client, as well as the design team.
