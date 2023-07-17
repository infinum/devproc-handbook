Pull requests are an essential part of our workflow. The preferred way of merging a branch back into the main one is by creating a pull request and assigning it to a colleague for review. 

At least one person should review any code that is going to be merged (reviewer on a PR).

It's essential to write a good pull request description. Reviewers will usually read it before looking at the diff, so make sure it gives them enough context to know what they are looking at.

Another purpose of a good description is to provide the documentation for future reference. A new developer might join the project in the future. The description will help them understand the motivation behind the implementation of a specific feature. Please note that any important information from the description should also be added to the main documentation in the project as a central reference point where the latest state of the project is documented.

### General rules

- You cannot merge a pull request until the CI build passes.
- The `main` branch should be set as protected, which means no one can force push into it, and you can't delete it. If you are not sure how to set it as protected or don't have access, ask one of the TLs/LEs to do it.

### Creating a pull request

1. A good pull request includes only one feature or a bugfix. Fixing multiple issues or adding several features in a pull request is not good practice, and it should be avoided whenever possible.
2. When creating a pull request, make sure you write a good description. It doesn't have to be long, but it has to provide context to the reviewer. Commit messages will not be considered a description of what has been done in the pull request.
3. If possible, provide the URL of the task which describes the feature or the issue.
4. Review your pull request before creating it. By reviewing your own pull request, you get a chance to notice some obvious stuff before assigning it to a reviewer.

### Reviewing a pull request

1. When reviewing a pull request, make sure to check how the changes fit the current code base and architecture. Do not approve the pull request if the changes are not aligned with the rest of the codebase for no obvious reason.
2. In addition to code inspection, check out the branch on your machine and test it on your mobile phone/browser. Use common sense for this. Maybe it is unnecessary to test the changes if a pull request changes only one file, but you should test the implementation in case of some bigger features or fixes. The idea behind this is to catch some obvious issues (paddings, margins, user-specific bugs, etc.) before they reach our testers.

These are guidelines, not rules, so use common sense when creating or reviewing a pull request.
