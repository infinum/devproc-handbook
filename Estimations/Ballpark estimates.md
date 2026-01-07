We use this term for scenarios when the business development team negotiates with a potential client and needs to provide a rough estimate on how long the development will take.

To help you jumpstart this task, we prepared:

* our official [Estimates detailed template](https://docs.google.com/spreadsheets/d/1SHeL-7NNmobVgEbNAY5ggLrEHh2iclG-G5u1BF53SH4/edit#gid=238358947) - check with the people involved in the potential project if someone already duplicated this template

Before you begin plotting the major aspects of the project, read the documentation provided by the client or the product owner. In case there is no documentation, contact anyone who might be relevant and ask for it. Talk with people who have some experience on the project until you can visualize the requirements and gain enough confidence to make estimations.

It's essential that you state all the assumptions in the estimation, as those might prove wrong which will change the implementation strategy, as well as the time to grow the project.

Here are some additional insights that might help you in this endeavour.

### Comparison-based estimation

Sometimes new projects are amazingly similar to what we've done in the past. Other times, they're startlingly different. More often they're somewhere in the middle. The simplest way of getting to a somewhat optimistic estimation is to compare those projects.

Once we've chosen a piece of work that's comparable to the one we're estimating, we can ask ourselves questions about how it compares:

* How does that work compare to this work?
* How does this work differ from that work?
* How many of those bits of work would it take to make up this work?

### Memory vs. recorded Data

Estimating based on remembered data is fraught with inaccuracies.

If you or one of your colleagues worked on a similar project, a good starting point is talking about it, but it's also prudent to get access to Productive's Insights and query the relevant data. Group it and categorize by the required service (e.g., Backend, Rails). How similar were the requirements of a feature to the one we're contemplating? How many people worked on it, in what role, and for how long? Were there a lot of meetings and why?

### Noting your assumptions

Ballpark estimates are often based on vaguely explained feature requests. This inevitably leads to you making assumptions on what the feature will actually look like. It is important to list all these assumptions in the estimation table. These notes are important for both the Solution architects and Business development teams and for you to recall why you estimated a feature the way you did. It is hard to overdo assumption notes and a good rule of thumb is to have notes for every estimated feature.

Your assumptions might look like:

* Search is assumed to be lexical (exact word) instead of fuzzy
* Filtering is implemented on the client side and the dataset is of a moderate enough size (hundreds of elements)
* It is acceptable if search results sometimes show slightly out‑of‑date information, as long as they update after a refresh.
* The navigation bar has a dedicated mobile 'drawer' version

### Implied and related features

#### Implied features

You will often need to include features which were not explicitly stated by the client but should reasonably be a part of the solution. One example of such related features are search empty and error states. Without these functionalities the search feature could be considered incomplete and broken. These features should be included in the estimate and properly noted down.

#### Related features

You could also encounter features that you believe can be improved with additional functionality, but where that functionality is not strictly necessary for the feature to work. For example, if you are estimating a "map" feature where you show search results on a map, the feature could be improved by implementing map-based search ("Find results in this area"). Since this functionality is not necessary for the original feature to work, it should not be included in the original estimate, but rather noted down as an additional feature and estimated as additional work. This is useful for expanding and aligning the agreed scope of work before development starts.

### Ideal, Expected and Worst case estimations

The difference between ideal, expected, and worst case estimations should not be based on differences in scope. As mentioned in the `Related features` section, scope differences should be included as additional rows in the table. What the difference should be based on is things possibly taking longer because of known and unknown risks:

* You expect challenges integrating with a poorly documented API, or a system developed by a third party.
* The final design could be significantly more complicated than the wireframe you are basing the estimate on.
* You know from experience that a feature could be tricky to implement.
* There are other unknowns in the feature.

### Including overhead time

Take into account the 'overhead' time for each task. Try to estimate the time required for proper task hygiene, repository hygiene and task syncs. This will be hard to estimate before the project starts, but do your best to reserve some time for it. Take care not to go overboard and risk estimate bloat. This time should be included in each specific feature, not as a single, accumulated number in the estimations table.

### Successful negotiation

Once a project start it's crucial not to take the ballpark estimation
