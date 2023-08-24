> *If it hurts, do it more often*

In our day-to-day work, we'll probably face a challenge or a problem that will be tedious to solve on our own. That's where dependencies come into the equation. Even though they solve our problem at hand, they create a new, subtle one, future maintenance. Even though we didn't develop those dependencies, it becomes __our responsibility to maintain them and ensure our product works in accordance.__

## Updates

It is our responsibility as engineers to watch out for new updates, improvements, changes, and bug fixes. In most cases, our clients or PMs don't know which exact plugin, database, or external libraries we are using so update initiative if needed, should come from us. We should check for updates regularly, otherwise, we can end up in a state where our product malfunctions, gets hard to maintain, or even worse impossible to build.

__Updating dependencies should be a regular part of our job.__ [According to Martin Fowler](https://martinfowler.com/bliki/FrequencyReducesDifficulty.html) frequency reduces the difficulty, which is the main principle of the Continuous Integration practice:

- Smaller changes - postponing the updates makes them much more difficult as the amount of changes increases, but when broken into smaller chunks they compose easily.
- Feedback - we'll get faster feedback for smaller updates, rather than waiting on the QA team to do the whole regression or smoke test of the app.
- Practice - the more often you do it, the easier it gets.

## How often?

Depending on the technology you are using, the project you are working on, or the team you are in there will be various approaches to how dependency updates will be tracked. If there is a possibility, some teams will use automated tools like [Dependabot](https://github.com/dependabot), [Snyk](https://snyk.io), or any other similar tool. Other teams, due to technical limitations, will have to fall back to some manual tracking, either through Productive, Jira, or some project status sheets.

But the update cadence shouldn't differ so much, regardless of how updates are tracked or done. Checks and updates for dependencies should happen regularly, __at least once a month__. If, for any reason, a dependency update is not possible for a longer period, talk to your LEs or TLs and they will try to help you organize the time/project/client so that the problem gets resolved.

## Common practice

Before updating any dependency, check the release notes and explore possible changes - through PRs, issues, or code changes if the library is open-sourced. It's hard to define an extensive process that will cover all possible edge cases for this part, but take into consideration a few things before updating:

- If there are breaking changes in the new version and you cannot fix it in a reasonable timeframe - don't update it, leave it as is, open the task on Productive/Jira and notify your PM about it to find some time to update it in the future.
- If you can see from the release notes/changes in code that the update contains only minor changes and bug fixes, update it and smoke test it.
- Please don't update dependencies a day before the release - you won't have time to test it out, nor will our QA, and you are risking new issues popping out.
- Inform your QA if you have done some major updates to look out for possible issues, especially if you cannot check all possible cases. For example, you have updated a few UI-related libraries and you cannot quickly test all possible use cases.

**If you have the slightest doubt or you are not sure what to do, **please talk with LEs, TLs, or someone more senior.**
