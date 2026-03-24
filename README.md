BIG PINK
UpStart Collective — Member Hub
README & Operations Guide
Last updated: March 2026

Overview
The UpStart Collective Member Hub is a single-page web application for managing the full lifecycle of UpStart members — from onboarding to offboarding. It lives at:

https://joshcarterpdx.github.io/upstart-hub/


The app is password-protected and runs entirely in the browser. All member data is stored locally in your browser's storage. No server required.

The app handles six sections:
Onboard Member — run the full onboarding workflow for a new member
Member Roster — view, search, filter, and edit all members
Offboard Member — run the full offboarding workflow
API Settings — store API keys to automate each step
Email Templates — customize the welcome and Unico emails

Deploying & Updating the App
First-time deploy
The app is hosted on GitHub Pages as a single HTML file. To deploy for the first time:

1
Create a GitHub account
Go to github.com and sign up for a free account if you don't already have one.
2
Create a new repository
Click "New repository", name it upstart-hub, set it to Public, and click Create.
3
Upload the file
Click "Add file → Upload files", drag in index.html, and click Commit changes.
4
Enable GitHub Pages
Go to Settings → Pages → Source: Deploy from a branch → select main → Save.
5
Access the app
Your app will be live at joshcarterpdx.github.io/upstart-hub within about 60 seconds.


Updating the app
Whenever you receive an updated index.html file:

Go to github.com/joshcarterpdx/upstart-hub
Click on index.html in the file list
Click the pencil icon (Edit file) in the top right
Click the … menu → Delete file — or simply use "Upload files" to drag the new version in
Click Commit changes
Wait about 60 seconds, then hard-refresh the app (Cmd+Shift+R on Mac, Ctrl+Shift+R on Windows)

ℹ️  Member data is stored in your browser's localStorage, not in the HTML file itself. Updating the file will NOT erase your member roster.


Login & Password
The app is protected by a password. The default password is:

XXXXXXXX


After changing it, re-upload the file to GitHub following the update steps above.

ℹ️  The password is stored in plain text in the HTML file. This is appropriate for a personal internal tool. Do not use a password you use elsewhere.


Onboarding a New Member
From the sidebar, click Onboard Member. Fill in the member's details and click Run Onboarding. The app will run all eight steps in sequence and show you live status for each one.

The 8 Onboarding Steps
1
Send Slack Invite
Manual step — the app will display a pre-filled mailto link to open a draft invite email.
2
Send Circle Invite
Manual step — same as Slack, opens a mailto draft for the Circle platform.
3
Add to Stripe
Creates a customer in Stripe and assigns the correct subscription (Floating or Dedicated Desk). Requires Stripe API key.
4
Send Welcome Email
Sends the welcome email with space instructions, Unico app info, and Stripe payment link. Uses your Gmail when configured.
5
Add to HubSpot
Adds the member as a contact in HubSpot for the newsletter. Requires HubSpot API token.
6
Send Handbook via SignRequest
Sends the member handbook and pledge for e-signature. Requires SignRequest API token and document URL.
7
Add to Master Google Sheet
Appends the member's row to the MASTER Google Sheet. Requires Google Sheets credentials.
8
Email Unico for Building Access
Sends a pre-filled email to the Unico team requesting the member be added to the building access database.


Step status indicators
Each step will show one of the following statuses as it runs:
✓ Done — completed successfully via API
! Manual — requires you to complete the step manually (opens a mailto link where applicable)
✕ Error — the API call failed; check the error note for details

Offboarding a Member
From the sidebar, click Offboard Member. Select the member from the dropdown and click Run Offboarding. The app runs six steps in reverse:

1
Cancel Stripe Subscription
Cancels the member's billing at the end of the current period.
2
Email Unico to Remove Access
Sends a pre-filled email to Unico requesting building access be deactivated.
3
Update Master Google Sheet
Marks the member as inactive in the MASTER roster.
4
Unsubscribe from HubSpot
Removes the member from the active marketing list.
5
Remove from Slack
Manual step — reminder to deactivate the member's Slack account.
6
Remove from Circle
Manual step — reminder to remove from the Circle community.


ℹ️  You can also offboard a member directly from the Member Roster by clicking the Offboard button on their row.


Managing the Member Roster
Viewing members
Click Member Roster in the sidebar. The roster defaults to showing active members. Use the filter dropdown to switch between Active, Inactive, and All. Use the search bar to find any member by name, email, or membership type.

Editing a member
Click the Edit button on any member's row to open the edit modal. You can update:
First and last name
Email address
Company / startup
Membership type (Floating Desk, Dedicated Desk, Partner, Community Member)
Start date
Pledge / handbook signed status
Active or inactive status

Click Save Changes to apply. Changes are saved immediately to your browser's storage.

Importing from Google Sheets
To refresh the roster from your Google Sheet:
In Google Sheets, go to File → Download → Comma Separated Values (.csv)
In the app, go to Member Roster and click Import CSV
Select the downloaded CSV file

ℹ️  The import skips any members already in the roster (matched by email address) to avoid duplicates. Only new members are added.


API Settings
Go to API Settings in the sidebar to enter your credentials. Keys are stored locally in your browser and are never sent anywhere except the respective API endpoints.

ℹ️  Steps without API keys configured will show as manual with instructions for completing them yourself. The app works fully without any API keys — you just complete those steps outside the app.


Where to find each credential
Service
Where to find it
Setting name in app
Stripe Secret Key
Stripe Dashboard → Developers → API keys
stripe_key
Stripe Floating Desk Price ID
Stripe Dashboard → Products → Big Pink Floating Desk
stripe_price_floating
Stripe Dedicated Desk Price ID
Stripe Dashboard → Products → Big Pink Dedicated Desk
stripe_price_dedicated
HubSpot Private App Token
HubSpot → Settings → Integrations → Private Apps → Create app
hubspot_key
Google Spreadsheet ID
Found in the URL of your MASTER Google Sheet between /d/ and /edit
sheets_id
Google OAuth Access Token
Use Google OAuth Playground at developers.google.com/oauthplayground
google_key
SignRequest API Token
SignRequest → Settings → API → Token auth
signrequest_key
SignRequest Document URL
URL of the handbook template inside SignRequest
signrequest_doc_url
Unico Email Address
The support email for your Unico building access contact
unico_email
Your Send-From Email
Your own email address (used as the sender on outgoing emails)
from_email


Email Templates
Go to Email Templates in the sidebar to customize the three email templates the app uses. Each template supports the following variables which are automatically filled in when the email is sent:

{{first_name}} — member's first name
{{last_name}} — member's last name
{{full_name}} — member's full name
{{email}} — member's email address
{{desk_type}} — their membership type (e.g. Big Pink Floating Desk)
{{date}} — the start or end date

The three templates
Welcome Email — sent to the new member with space instructions and next steps
Unico Building Access Request — sent to Unico to add the member to the building database
Offboarding — Unico Removal Request — sent to Unico to deactivate building access

Click Save Templates after making changes. Click Reset to Default to restore the original text.

Troubleshooting
My member data disappeared
Member data is stored in your browser's localStorage. It can be lost if you clear your browser's site data, use a different browser or device, or open the app in a private/incognito window. To protect against data loss, regularly export your Google Sheet and use the Import CSV button to re-sync.

An API step shows an error
Check the error message displayed under the step. Common causes:
Incorrect or expired API key — go to API Settings and re-enter the credential
Stripe Price ID is wrong — make sure you're using the Price ID (price_...) not the Product ID (prod_...)
Google OAuth token expired — these tokens expire after 1 hour; generate a new one at developers.google.com/oauthplayground

The app won't load after re-deploying
Hard-refresh the page after any update: Cmd+Shift+R on Mac, Ctrl+Shift+R on Windows. GitHub Pages can take up to 2 minutes to propagate a new file.

I forgot the password
Open index.html in a text editor, find const APP_PASSWORD = '...', and read or change the value. Re-upload the file to GitHub.

Quick Reference
Item
Detail
App URL
joshcarterpdx.github.io/upstart-hub/
GitHub repo
github.com/joshcarterpdx/upstart-hub
Default password
upstart2024
Password location in file
const APP_PASSWORD = '...'
Member data storage
Browser localStorage (local to your device)
Import members
Roster → Import CSV
Edit a member
Roster → Edit button on their row
Change email templates
Email Templates in sidebar
Add API keys
API Settings in sidebar


UpStart Collective — Big Pink, Portland OR
