The DevOps team is responsible for creating all new repositories and managing their permissions. This ensures consistency, security, and clear ownership across all projects.

## Repository Ownership and Metadata

Every repository must include [cusotm properties](https://docs.github.com/en/organizations/managing-organization-settings/managing-custom-properties-for-repositories-in-your-organization)  that define:

* __Responsible Team__ – the name of the team or department maintaining the repository.
* __Production__ – indicates whether the repository contains code used in production (true or false).

These properties must be set at repository creation and updated whenever ownership or usage changes.

## Production Repository Rules

If the custom property __Production__ is set to `true`, the following policies apply:

* Pull requests require a minimum of __one approval__ before merging.
* Administrative accounts __cannot bypass pull request rules.__
* These restrictions are enforced to maintain production stability.
* Dependabot must be enabled to automatically monitor dependencies for vulnerabilities and outdated packages. All detected vulnerabilities must be addressed according to their severity, following these timelines: __critical and high__ severity issues must be resolved within __30 days__, __medium__ severity issues within __60 days__, and __low__ severity issues within __90 days__.

## Rule Overrides

If an exception or temporary relaxation of these rules is required please contact DevOps team in `#devops-hotline` slack channel
