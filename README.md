Pocket Chat
A small, installable AI chat app for Android that runs on your own OpenRouter API key. It is a static website (no backend, no build step) that can be hosted for free and packaged into an APK.
Features
Chat with any OpenRouter text model
Automatic fallback: list several models in order and the app tries the next one if a model fails (rate limit, no credits, outage)
Video mode for video generation models (for example Gemini Omni)
Reply labels: each answer shows which model actually responded
Installable: works as a home-screen app and can be packaged as an APK
Private: your API key is stored only in your device's browser storage and is sent only to OpenRouter
Files
File
Purpose
index.html
The whole app (UI, chat, fallback, video mode)
manifest.json
Web app manifest (name, icons, install settings)
sw.js
Service worker (needed for installability)
icon-192.png, icon-512.png
App icons
Deploy
The app is plain static files, so any static host works. With Netlify:
Go to app.netlify.com/drop.
Drag in the project folder (or a zip containing these five files at the top level).
Open the *.netlify.app link it gives you.
To update later, open the site's Deploys page and drop the new folder or zip into the upload box at the bottom.
Set up
Create a key at openrouter.ai/settings/keys.
Open the app, tap Settings, and paste the full key. Truncated keys (with ... in them) will be rejected.
Under Chat models, enter one model ID per line, in the order to try them. Default:
openrouter/free
anthropic/claude-haiku-5.5
Optional: set a Video model, for example google/gemini-omni-1.2-flash.
Tap Save.
Use exact model IDs from openrouter.ai/models, including the part before the slash. Embedding and rerank models cannot chat.
Build an Android APK
Deploy the site and make sure https://YOUR-SITE.netlify.app/manifest.json loads.
Go to pwabuilder.com and enter your site URL.
Choose Package for stores, then Android, then the APK option.
Download the zip, extract it, and install the .apk on your phone.
Keep the signing key file and its password somewhere safe. You need them to publish updates to the APK.
The APK loads your hosted site, so updating the website updates the app. You only need a new APK if you change the app name, icon, or URL.
Note: the installed app has its own storage, separate from the Chrome tab. Enter your API key again in Settings the first time you open it.
Costs and limits
Paid models are billed per token from your OpenRouter credit balance. With a $0 balance, paid models return a credits error.
Free models (IDs ending in :free, or openrouter/free) cost nothing but are rate limited per account: 20 requests per minute, and 50 requests per day until you have bought $10 of credits in total, then 1,000 per day. The limit is shared across all free models, so adding more free models to the list does not raise it.
Video generation costs much more than text. Set a small spending limit on your key.
You can set a monthly limit on a key at openrouter.ai/settings/keys.
Security
Never commit an API key to this repository. The app asks for the key at runtime and does not contain one.
Anyone with your key can spend your credits. If a key is exposed, revoke it and create a new one.
Messages are processed by OpenRouter and the model provider, so avoid sending private information.
Troubleshooting
Problem
Fix
"API key was rejected"
Paste the full key, or create a new one.
"Key limit exceeded"
Raise the key's monthly limit in OpenRouter.
Credits error on a paid model
Add credits, or use a :free model.
"Not a valid model ID"
Copy the exact ID from openrouter.ai/models.
Key not remembered
The app and the Chrome tab store data separately. Enter the key in the app you are using and avoid clearing site data.
Old version still showing
Fully close the app from recent apps and reopen it.
License
Choose a license for your repository (for example MIT) and add a LICENSE file.
