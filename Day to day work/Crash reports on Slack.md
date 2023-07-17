As people switch from project to project, tracking crashes might get forgotten. If we lose track of crashes, we might not be aware of issues in production. That's why we integrate crash reports with Slack, and new or repeating issues are posted to the notifications Slack channel of a project. That way, the whole team is aware of the issues and can react if needed.

To avoid confusing our clients, we always integrate crash reports into the project notifications channel unless agreed otherwise.

## How to integrate crash reports with Slack

Android and iOS teams use [Firebase](https://firebase.google.com/) to integrate crash reports, while Flutter uses [sentry.io](https://sentry.io/welcome/). 

### Android & iOS & Flutter - Firebase
To set up the Slack integration, you need to be the owner of a project on Firebase. Go through steps 1 and 2, and if you see a message "Project owner required," contact your TL or project manager to give you access or do the integration for you.

1. Ask your PM to open a new `#projectName-notifications` channel
2. Select your project on [console.firebase.google.com](https://console.firebase.google.com/)
3. In the upper left corner select the gear icon and click on project settings ![](/img/firebase/firebase3.png/)
4. Go to the Integrations tab and click install in the Slack card ![](/img/firebase/firebase4.png/)
5. Go to the Firebase app on Slack and create a new webhook. You need to select the channel where the app will post issues. Click on this [link](https://api.slack.com/apps/A01F7NKPG2H/incoming-webhooks) instead of trying to find the app in Slack. If you don't have access to the Slack app, contact your TL
6. Copy the webhook and set it on Firebase in the Slack integration. Write down again the channel where messages will be shown and click on save. ![](/img/firebase/firebase6.png/)
7. If the integration is successful, you will get a message on the channel you selected ![](/img/firebase/firebase7.png/)
8. Go back to the Slack integration in the integrations tab and make sure all triggers are on ![](/img/firebase/firebase8.png/)
