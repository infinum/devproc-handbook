In agile software development, **user stories** are the most used form of delivering a feature request.
A user story is a small slice of functionality that's described in terms of the user's goals and capabilities. It's so named because it involves an interaction with a user of the system, either accepting input or providing some observable result, and usually both.

### Size matters
You might have encountered the term **"epic"**, which suggests that the story is intended to be further split before implementation. A good rule of thumb is to split your stories into slices that can be implemented in two days at most, or 1 hour at least. Round your results! There is no gain in estimating a feature in minutes, which just turns the additional numerical precision into noise. Filter it out.

**Acceptance criteria** should be added to story splits to indicate when that user story is considered to be sastisfactorily completed.

### Ignorant optimist
During our careers, we'll encounter various projects with unique functionalities or features that feel familiar, but hide an unknown amount of complexity. It may be tempting to undertake the request by yourself, but more often than not you'll oversee an important aspect of the task and put yourself into a corner and be the sole responsible person. Remember you have colleagues that are doing the same job you do and there might be a chance some of them have knowledge that you could benefit from now. Ask them!

It's important to know how to form your sentences. Be expressive and focus on the bigger picture of the task at hand. Explain the specific models of your domain, the inputs, outputs and what concerns you have. Also, be mindful of the amount of information you'll relay, because it tends to confuse the reader.

### Mastering decomposition
Oftentimes, we'll have enough experience and knowledge about a new requirement, but a very important step in the estimation process is decomposing the user story. If you break it down into pieces, then there's a higher likelihood of those pieces being even more similar to pieces of your other projects.

If some of the parts are still too big to estimate, take the first (in the development order) of those parts and break it down again.
Can you estimate the first item? If not, you can decompose that first item in a similar fashion. Now you've got smaller items that can be more easily estimated. If they're still too big, you can repeat this process.
Realize that each time you reach a new level you're increasing your uncertainty. That's to be expected. The longer the time horizon, the more uncertain you are. For longer term estimates (e.g., longer than a few weeks), decompose into a half-dozen to three dozen parts, not hundreds.

Decomposition should be the primary estimation tool. Write down the components of the domain, how they'll interact with each other and the current system and whether they might affect the system to its core. When you make the components small enough, you can imagine how long it might take you to accomplish each of them. Then it's just a simple matter of adding them up to get a larger chunk of the estimation (don't forget about the safety margin). This will give you a number to report, but the decomposition work itself will also be beneficial because you'll get more familiar with the individual chunks of work, and it will provide you with a good foundation for opening tasks with acceptance criteria. This enables you to do work faster in case you have more developers, because each of them may work on a separate component. If you find yourself doing this, congratulations, you're unofficially a tech lead on the project :)

#### Decomposition gotchas
Bear in mind that if you've put more effort into planning, you'll find it more difficult to change the plans when it becomes apparent they're obsolete.

Errors are more likely to reinforce each other than to cancel each other out. If you're adding up a large number of small estimates and the errors all tend in the same direction, the resulting error will be large.

You may consistently imagine the pieces as larger or smaller than they are. When you estimate a lot of small pieces, you don't expect to get each estimate "right". It's perfectly fine if you've estimated two tasks at 3 hours each, but one ends up taking 2 hours and the other 4. The errors cancel each other out and your overall estimate is useful to you.

Don't decompose your big picture into lots of tiny details, because you'll lose sight of the original intent. It becomes hard to remember which aspects are essential and which are elaboration. It's even harder to communicate the focus to someone else. They see an undifferentiated sea of details, not a clear picture of the important goals.

As you break down the anticipated work to estimate the pieces, consider the following:

* Am I creating too much detail?
* Am I creating the illusion of knowledge? Could I be overlooking some of the pieces, or the work that joins the pieces?
* Am I making the whole look bigger than it actually is?
* Am I breaking things down in a way that will be useful during implementation? Or will it be a hindrance?
* Am I concentrating too much on the mechanics of estimation and losing focus on my actual goals?

Don't overly focus on the core of the work and neglect the periphery:

* getting the local environment ready
* reading the code to understand the details of the needed change
* writing tests
* code reviews
* potential changes during code review
* deploying to live environments
* reporting
* verifying that the change is correct
* verifying it hasn't broken existing functionality

**Rule of thumb:** Never estimate a programming task at under 1 hour, unless you're certain from past experience and current project state that it will go without problems. In the latter case, you should be on the project long enough to know its state.

### Perform a spike
Sometimes you'll find yourself in situations when you or your teammates don't have enough reasonable historical data to make an estimate.

Information can be obtained by running your own experiments. You may not know how long something might take if you don't know whether it can be done at all. When you need some information, consider how you could acquire it. There is often a small but critical piece of information that you need. Articulate what that critical bit is. Devise the most inexpensive way that might possibly give you that information.

This is often called a **spike solution**, or just spike, evoking an image of a very slender solution driven through the heart of the problem. We recommend the following procedure for spikes:

1. Articulate the question to be answered. If it's vague, it's hard to tell whether you've answered it or not.
2. Decide how long you're willing to work on it. Setting a budget is important to prevent a research project that dwarfs the importance of the question.
3. Work on a solution until either the question is answered or the time budget has been expended. If you still don't have your answer, start over and think about it again. Is it worth spending a little more time? Would it perhaps be more fruitful to try a different approach? Is there a way to bypass the need for this answer, at least for now?

A spike is a handy tool for answering many questions:

* Can this library do the job we need?
* Can we develop an algorithm to do the job we need?
* Can we calculate this to the needed precision?
* If we have a data stream that looks like this, can we process it to extract that information?
* If we offer users a way to do something, will they be interested in it?
