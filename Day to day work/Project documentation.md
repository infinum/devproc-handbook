## Project Documentation

The documentation should be separated into a few levels of the project you are working on. That way, anyone can easily find the info they are looking for by searching specific files section.

Those levels are shown in the following diagram:
![](/img/project_documentation/documentation_chart.png)

### Base documentation - readme
The readme of the platform (i.e., Android, iOS, Flutter, etc.) should contain only chapters defined in the [mobile template readme](https://github.com/infinum/mobile-readme-template). The idea behind that readme is to have only crucial information regarding the project's platform.

You can find the template here: [Mobile readme template](https://github.com/infinum/mobile-readme-template)

### Platform wiki
If you need to add anything extra that is not covered by the readme template, you should create a wiki (e.g., repo wiki on GitHub). 

That wiki can contain topics such as:
- Security storage usage
- Project Specifics (e.g., Xcode, Android Studio)
- Third-party integrations
- Testing Setup
- Pentest preparation
- etc.

This wiki should only contain platform-specific documentation.

### Project documentation
In general, this documentation should be the largest one. Anything related to the project should be put in here. If you have to write the same thing on both readmes or platform wikis, that should be done here.

Some of the examples:
- General project info
- Onboarding & setup
- App activation
- VPN setup
- Illustrations and icon naming
- Feature flags
- Test users
- etc.

Anyone working on the project (i.e., Developers, Designers, QA, PM, etc.) should participate in creating this document. 
This is the only documentation that is not defined by technology. So feel free to write it on a separate Wiki (GitHub) repo, Confluence, Productive, Google Docs, etc.

---
*In case you need some examples on how each level of documentation looks like in real life projects, please contact a proejct team that has such level of documetnation that interests you. For example, a good reference point to see this for a particular mobile projects is to check the Mobile Project Health Score sheet.*
