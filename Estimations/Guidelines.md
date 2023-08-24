This chapter provides some general guidelines that can be used when estimating any scope of work.

## Aspects to compare
When comparing future work to past experience, if you neglect some aspect that is roughly the same in both cases, no harm done. But if you neglect some aspect that differs in a way that affects the pace of accomplishment, it can have a major impact on the accuracy of your estimate. Let's look at what aspects might differ.

### Aspects of the system
Look at the actual requirements:

* **Quantitative aspects of the system**<br>
Ask yourself how big is the code being developed, and how much functionality is being added. Notice the things that you can count, such as the following examples:
  * How many user workflows are needed?
  * How many screens will that take?
  * How many "logical items" will need to be stored?
  * With how many other systems does this one communicate?
  * How many interfaces does this system provide to others, and how many functions per interface?
* **Qualitative aspects of the system**<br>
Dig into the qualitative aspects of the system:
  * How complex is the functionality being developed?
  * Has something like this been implemented before?
  * Are there significant interactions between the parts, or are they relatively independent of each other?
* **Quality aspects of the system**<br>
Consider the quality of implementation:
  * How much emphasis should be given to the maintainability of the system and to future extensibility?
  * How good is the development team at writing maintainable, extensible code?

### Aspect of the development context
The details of the development process have a huge impact on development speed. Rushing into development without proper preparation is a major cause of systems development taking much longer than anticipated. Setting things up for success is the prudent plan.

* **Familiarity of the development context**
  * How much of the scope is well understood and how much is vague or new?
  * Do you have a solid background in the business domain?
  * Are you fluent in the implementation technology?
  * Do you even know yet who will be doing the implementation?
* **Relationships surrounding the development context (client, manager)**
  * Are they congenial and easy to please, or nitpicky and opinionated?
  * Are they willing to engage throughout the project to clarify the requirements as they are addressed or as new questions come up?
  * Are they likely to want to implement all presented options?

Effort also depends on duration. It takes effort to get back up to speed after an interruption or delay. Consider work on other projects and the rate at which you can do the work on the main one:

* Will the work be interrupted?
* What else will be going on at the same time?
* Will there be task switching between projects vying for attention?

## Progress checks
During a project lifecycle, the PMs will require some way to verify that the rate of progress is sufficient. They need to know how things are going so they can make plans and decisions at a macro level.

Give them the honest information they need. If they need more detail, or the data worries them, then you can share a more detailed perspective with them. Most of the time, that more detailed data requires some tacit knowledge of the project to understand it. They probably don't have the time to stay up-to-date on the tacit knowledge of the project, hence the recommendation to give them a useful summary.

If they need a more detailed understanding, it will probably be best to go over your progress indicators with them, helping them understand the context within the project as they help you understand the context surrounding it. Don't just give them numbers - tell them the story.

Don't rely on a percentage of completion as a measurement. Those are very dangerous. When you say it's 50% complete, people will expect the next 50% to take the same amount of time. That's often a bad assumption. Measure slices of usable functionality as units of progress, confirmed by automated tests that check examples of the desired behaviour. A unit of progress can be anything here, how close we are to completing a feature, milestone, or production release deadline. It is usually defined by the tech lead, PM, PO, client. As a developer, ask yourself:

* Is the feature ready for testing?
* Does it work in an environment that mimics production?
* How well does it mimic it?
* Have you written tests as you created classes or are you writing tests at the end?
* How is your reviewer usually during code reviews?
* Is there always a lot of conversation in the PRs?

When the conversation resolves around speed and efficiency, you might feel an implicit pressure to go faster, intended or not. If you are trying to improve your performance, never focus solely on speed. Pushing harder often means arriving later at the destination. The more schedule pressure, the less time you can take to look around at factors other than speed. Waste creeps in as:

* Deferring attention to quality, and having to do work over again
* Duplicating processes before we get them working well
* Accomplishing less with more work, often the result of team burnout

If you notice that your work is being slower than usual on a project, look for bottlenecks in the code and process:

* The code diverges from clearly expressing the problem domain
* Small messes get left behind for "some day" when there will be time to clean them up
* Code gets more and more complex, and therefore harder and harder to expand and enhance
* Duplication grows when there are areas that people are afraid to touch, or can't easily know about as they're writing code
* Code gets harder to read, and therefore it takes longer to find where to change it and how the change should happen

## Diverging estimations and actuals
It's just a matter of time when you'll have a streak of "bad" estimations, where the cause originates from various factors. It's important to look at the silver-lining in these cases:

* **Learn from it**<br>
There's often something that can be learned and improved. "Incorrect estimates" are not useful when considered as failures, but are a goldmine of potential information and insight. It's instructive to examine in what ways they are wrong and how they came to be wrong. The questions you might ask yourself include:
  * when we made this estimate, what did we assume that turned out not be true?
  * what has changed since we made this estimate?
  * have we seen similar issues with prior missed estimates?
  * when could we have noticed this if we'd been checking our estimates periodically?
  * if we account for these changes in estimates of future work, how does that change our plans?
  * does our new plan have enough safety margin for severe risks?
* **Don't stress**
* **Be transparent**<br>
  Honesty is the best policy! Your estimates weren't really wrong. They were made in good faith based on the information available at the time. Now that you have more information, the estimate has become obsolete. Explain this and analyse how much work is needed to finish the task.
* **Don't hurry**
* **No blame games**<br>
  It's easy for people to shift from blaming the estimate to blaming the estimator. "They should have known better." Perhaps they could have made a better estimate and perhaps not. And perhaps they made a perfectly good estimate for some other requirement than the one for which it was found wanting. In any event, there's little you can do now to improve a past estimate.
