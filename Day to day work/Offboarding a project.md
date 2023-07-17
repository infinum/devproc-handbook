## Leaving a project

The time will eventually come when you have to leave a project because you're moving on to new responsibilities. You must take good care that you leave the project in a better state than you found it, just like the boy-scout rule: 

> “Always leave the campground cleaner than you found it”.

### Finish ongoing tasks

Try to finish any tasks that you're assigned to and have made any progress on. The closer you are to completing the task, the more certain you should be the one to finish it. For example, suppose you have started developing and have gotten to the point of a Pull Request review. In that case, you're almost certainly the person to finish that task. If you really have to leave the task unfinished, then write down the specifics of what still needs to be done, the task description on Productive (or any other PM tool the team is using), and the PR itself.

On the other hand, if the task is only in the conceptual stage, and at most, you have just ideas on how to proceed, write those ideas down in the task description.

If you think you'll need a non-trivial amount of time to finish these tasks, make it clear to the appropriate people that there are still things that you need to complete on the old project. But please announce that before you make a switch over to your new project and responsibilities so that you can get the proper amount of time.

### Onboarding new colleagues

Suppose you were the only developer on the project, and the new person will take your place. In that case, you'll need to onboard them to the technical side of the project so that they can have an easier start. Try and organize a meeting, where the two of you will sit down and go over the project. Here are some things that you'd want to cover:

 1. General overview of the project and architecture.
 2. How to navigate the project files.
 3. Components that are difficult to understand or use, or just confusing.
 4. If the project is based on the standard team architecture, which version of it is it on, and how/why it deviates from it, if it does.
 5. External dependencies like libraries, APIs, content providers, etc.
 6. Internal dependencies/dependents, for example, mobile or web applications, API endpoints, etc. 
 7. Team members and structure, project workflow.
 8. Anything else you think will be useful.

Do not rely on onboarding meetings as a means for knowledge transfer. You might not be available for a meeting for a multitude of reasons, making the lives of your successor much more difficult. Even if you do hold an onboarding meeting, you are dumping a ton of information on your colleague in a short time. They will not be able to absorb everything at once and probably forget many details in time. Think about a Friday meeting, scheduled then because you stop this week and they start the next, the weekend will wipe away most of what you discuss (especially if it's a good weekend). That is why it [**absolutely pays to have written documentation**](#write-documentation).

### Write Documentation

You have probably been working on the project for quite some time. In that time, you have learned a lot of stuff. Quirks in the projects that arise from some technical limitations, issues with the integrations: mobile, web or backend, location of documentation files, test accounts and how to access them, who does what, etc. **Write it all down**, write down **everything** you can think of. The minimum you can do is **create or update** the standard readme file, as defined in your teams' handbook.

If the project readme file is not sufficient for the information you need to store, feel free to use additional markdown files in the project repository, Productive Notes, Confluence pages, or whatever tool the team uses to share information. In case you're doing it outside the project repositories, make sure you link to all the locations that contain this documentation in the readme.

Do not wait for this moment to start writing the documentation. It would be best if you started sooner. You should create and update the documentation as you work on the project. Make writing documentation a habit or schedule a time to write it (every few days, weeks, sprints).

### Do not immediately disappear from the project

Keep in touch with the project members after you leave the project. Stay in the important Slack channels since there might be questions that only you have the answer to. Check it regularly in the beginning, and try to fade away gradually, depending on how quickly your successor can take on all the responsibilities.

Be available to your successor for any questions or help. In case you need a significant amount of time for this assistance, talk to your new PM, team, and operations to schedule time for it.
