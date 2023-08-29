Rules from previous chapters should be the minimum for all platforms. Few more are specific and applicable only for mobile platforms. If you cannot apply some of the mentioned rules to your project, please talk with another platform and try to find a viable solution for both of you. I cannot emphasize enough how important it is to have both platforms in sync!

### Git Flow/Infinum Flow

We use a variant of the [Git Flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) workflow. There are some differences between our variant and the linked page, as described in this chapter.

![Git Flow](/img/using_git/git-flow.svg)

On most of our projects, we will use `main` as the main branch, and `develop` will not be used. All development will be done on the `main` branch. Each release is **tagged** with the version number described in [Using Git](/books/devproc/git/using-git) chapter.

We noticed that only one of them is used actively when having both `main` and `develop` branches. Since we have tags on release commits, having a branch that only contains published code seems unnecessary. That is why, for simplicity, we only keep the `main` branch as the main branch and track releases via tags.

#### Branches

The main branches in this flow are:

* `main`
    * it is the main branch
    * must be marked as protected on Github
    * anything in the main branch is deployable
    * is stable and it is always, always safe to deploy from it or create new branches off of it
    * feature and hotfix branches are merged into it only after pull request review is done

* `release`
    * used for parallel development (e.g. multiple versions of the app when version 1.0.0 is developed on main, version 1.1.0 can be a next `release/1.1.0` or for developing multiple features that should or shouldn’t be in the same version: `release/separate-cool-feature`)
    * same rules as for the main branch

* `feature`
    * used for developing new features/adding a new functionality to the app
    * branches off of `main`/`release`
    * has prefix `feature/`, e.g. `feature/123-add-followers-button`

* `fix`
    * used for fixing non-critical production bugs or bugs that occurred in the development phase
    * has prefix `fix/`, e.g. `fix/123-wrong-cards-sorting`

* `refactor`
    * used for codebase/project refactoring
    * has prefix `refactor/`, e.g. `refactor/123-alert-and-action-sheet`

* `hotfix`
    * used for fixing critical bugs in production
    * branched off from the corresponding tag and created PR to the main or to the latest release branch if one exists
    * has prefix `hotfix/`, e.g. `hotfix/1337-recipe-details-crash`
    * example usage: there is a bug on app version 1.2.0. In that case, checkout to a commit tagged with `v1.2.0`. Create the `release/1.2.1` branch from that tag, and create `hotfix/whatever` from that branch where you implement the fix and create PR back to the `release/1.2.1` branch

## Pull requests

Each pull request must have an automatic check - running tests or building the app if your project doesn’t have tests. Setup on GitHub is described in the general rules of this handbook. While setting up Bitrise Checks on projects, you have [Android](/books/android/ci-and-code-analysis/continuous-integration) and [iOS](/books/ios/bitrise-ci/pull-request-ci-check) handbook chapters.

## Deployment

Deployment is done via tags and Bitrise CI/CD. You can find the chapters on setting up Bitrise on your project here for: [Android](/books/android/bitrise) & [iOS](/books/ios/bitrise-ci/general-intro).

Again, sync with another platform as much as possible. Few stuff that should be defined and synced:

* **Environment names** - *staging*, *production*, *uat*, *beta*... whatever is the convention on the project, but should be the same. Exception probably will be iOS with its production and App Store environments due to technical limitations. If using TryOutApps please sync environment names.

* **Build number/code version** - must be numbers only value. For build number, you can use tag count or manually auto-increment number value (i.e., before creating a new build, the last build number should be fetched and increment by 1).

* **Tag names** - tags (used for tagging the TryOutApps version and/or triggering Bitrise CI) should be compromised of three parts: **environment**, **app version with v prefix** and **build number/code version**, e.g. `internal-staging/v1.2.3-1234`
    * Each project will have different environments so this will be project dependent, but some suggestions are: tags should have the prefix like `internal-staging/`, `internal-production/`, `appstore/`... Due to limitations on tag triggers on Bitrise, tags with multiple `/` are not permitted.
    * Use `internal-` prefix for all tags which will trigger internal builds (like TryOutApps). Since internal tags are not so relevant and one should clear them from time to time to keep the project clean.
    * You should tag all production versions published to the AppStore/PlayStore with one extra tag once the app is released to better overview released versions. The tag should look like this: `v1.2.3` (without build number).

There is an [app-deploy-script](https://github.com/infinum/app-deploy-script) which will come in handy in case of deployment. It already covers all of the mentioned cases above - it has support for multiple environments, generates and reads the last version, generates build number from tags count, has support for changelogs - pretty much everything it needs.
