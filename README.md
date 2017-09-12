# Build a Bot with Zero Coding

Most bot tutorials are for people who can code, so if you don’t have developers or staff with extra time on their hands your custom needs may not be met. Building a bot requires technical resources, such as servers to run the logic, storage to store data points and developers, well, to code. Until now. In this tutorial, we’ll show how you can build a survey bot right from a Google Sheet.

## Why?

Instead of using a server to run your bot logic (which is actually easy, but it requires maintenance), use Google as your hosting environment on your behalf and use Google Sheets to keep track of the survey answers!

![Animation flow](https://github.com/devrelv/blog/blob/master/google_sheet_flow.gif?raw=true)

### Code running on a spreadsheet?
Google Apps Script is a JavaScript-based scripting language that lets you add functionality to your Google Apps. It is a cloud‑based language that integrates with all other Google services, including Gmail, Google Drive, Calendar, Google Forms, Sheets and more. Apps Script is incredibly versatile. It allows you to:

- Add custom menus, dialogs, and sidebars to Google Docs, Sheets and Forms
- Write custom functions for Google Sheets. Like fetch extra data from external services or even plot some sophisticated charts
- Publish web apps — either standalone or embedded in Google Sites
- Interact with other Google services, including AdSense, Analytics, Calendar, Drive, Gmail and Maps

## Prerequisites
- Have a <a href="https://accounts.google.com/" target="_blank">Google Account</a>
- <a href="https://developers.viber.com/docs/general/getting-started-with-bots/" target="_blank">Get your Viber Public Account authentication token</a> 

## How?

### 1. Make a copy of the spreadsheet

>  <a href="https://docs.google.com/spreadsheets/d/187abmrkYlgoDZrYPChgQZiG2btfi98YPWrYYMF42UpQ/edit?usp=sharing" target="_blank">https://docs.google.com/spreadsheets/d/187abmrkYlgoDZrYPChgQZiG2btfi98YPWrYYMF42UpQ/edit?usp=sharing</a>

In Google Sheets, Click **`File`** > **`Make a copy`**...

![make-copy](https://github.com/devrelv/blog/blob/master/google_sheet_make_copy.jpg?raw=true)

This should give you something like this:

![copy-of-sheet](https://github.com/devrelv/blog/blob/master/google_sheet_edit_copy_name.jpg?raw=true)

> **Note:** Feel free to change the name of the `Copy` to anything you want, it will not affect the outcome.

### 2. Under the **`parameters`** sheet, edit the following fields:

- Access Token - Use the <a href="https://developers.viber.com/docs/faq/#authentication-tokens/" target="_blank">Access Token</a> which you got during the Public Account creation.
- Bot Name - Be creative!
- Bot Avatar URL - URL of the survey avatar. Avatar size should be no more than 100 kb. Recommended 720x720
- Welcome to survey message - This is the welcome message which the user will receive from the survey bot
- Welcome start button - Call on the user to begin interacting with the bot
- End survey message - This is the message the bot will send at the end of the survey. It is generally a “Thank you” message
- Do not understand message - This message will be sent if the user enters invalid input (a picture, sticker, etc.)
- Should keyboard use random colors - Should the bot use random colors for different survey answer options or not. Acceptable values are `true` or `false`
- Default keyboard option color - In case you choose not to use random color, you can set the default color here. Please use `Color Hex` <a href="http://www.color-hex.com//" target="_blank">format</a> only. For example `#999999`

![parameters-sheet](https://github.com/devrelv/blog/blob/master/google_sheet_parameters_edit.jpg?raw=true)

This is the difference between a keyboard with specific colors versus one generated with random colors:

![parameters-sheet](https://github.com/devrelv/blog/blob/master/google_sheet_solid_to_random.png?raw=true)


### 3. Under the **`questions`** sheet, edit your questions:

#### Question types
Our survey bot supports three (3) different types of questions: `range`, `keyboard` and `text`:

- `range` -  Asks the user to enter a valid value from a custom range. It makes sense to provide a range when the user needs to score something.

	![range-type-questions-sheet](https://github.com/devrelv/blog/blob/master/google_sheet_questions_example_range.jpg?raw=true)

- `keyboard` - Show case different selection options via the Viber's keyboard.

	![keyboard-type-questions-sheet](https://github.com/devrelv/blog/blob/master/google_sheet_questions_example_keyboard.jpg?raw=true)

- `text` - Free text input.

	![text-type-questions-sheet](https://github.com/devrelv/blog/blob/master/google_sheet_questions_example_text.jpg?raw=true)


#### Editing questions
Each row in the spreadsheet equals to a survey question and ordered by sequence. Hence the first row (after the header) will contain the first question, while the 7th row will contain the seventh question.

**Adding a `range` question**

- Under the `type` column write `range`
- Under the `question` column write your question. Best practice is to mention the actual valid range.
- Under the `extras` column write the acceptable values, separated by semicolons. For example `0;1;2;3`.

	![range-type-questions-sheet](https://github.com/devrelv/blog/blob/master/google_sheet_questions_range.jpg?raw=true)

**Adding a `keyboard` question**

- Under the `type` column write `keyboard`
- Under the `question` column write your question.
- Under the `extras` column write the options, separated by semicolons. For example `Yes;No`.

	![keyboard-type-questions-sheet](https://github.com/devrelv/blog/blob/master/google_sheet_questions_keyboard.jpg?raw=true)

**Adding a `text` question**

- Under the `type` column write `text`
- Under the `question` column write your question.

	![text-type-questions-sheet](https://github.com/devrelv/blog/blob/master/google_sheet_questions_text.jpg?raw=true)

### 4. Open the Script Editor

Open the **`Script editor...`** by clicking "**`Tools`**" > "**`Script editor...`**"

![script-editor](https://github.com/devrelv/blog/blob/master/google_sheet_open_script_editor.jpg?raw=true)

### 5. Publish the script as a Web App

![publish-script](https://github.com/devrelv/blog/blob/master/google_sheet_publish_web_app.jpg?raw=true)

Select the *latest* project version to deploy.

> **Note:** You **must** select the `Anyone, even anonymous` option for the "Who has access to the app" dropdown or form responses will not be added to the spreadsheet!

![deploy-new-version](https://github.com/devrelv/blog/blob/master/google_sheet_deploy_web_app.jpg?raw=true)

### 6. Authorize the script to access your Google Sheet data on Google

![auth-required](https://github.com/devrelv/blog/blob/master/google_sheet_deploy_auth.jpg?raw=true)

**Copy** the web app URL to your clipboard / note pad.
Then Click "OK".

![deploy-as-web-app](https://github.com/devrelv/blog/blob/master/google_sheet_deploy_url.jpg?raw=true)

### 7. Set the WebHook on Viber

<a href="https://viber-api-console.herokuapp.com/" target="_blank">Viber chat API console</a> is a helper site set up for this integration, specifically to help you set up a WebHook. This way Viber will know to communicate with your Sheet.

Select the **`Set a WebHook`** operation, paste your web app URL from the previous step and click the **`Apply`** button to make the change.

![set-web-hook-console](https://github.com/devrelv/blog/blob/master/google_sheet_console.jpg?raw=true)

**Done**. That's it. You just created your very own survey chat bot! Your survey answers will populate on the **`answers`** sheet.

![deploy-as-web-app](https://github.com/devrelv/blog/blob/master/google_sheet_answers.jpg?raw=true)

## Want more?
Feel free to customize the code, add more question types, improve the flow or even accept pictures as valid input!

## How to report bugs
If you find any issues with this sample, please open an [issue on GitHub](https://github.com/Viber/build-a-bot-with-zero-coding/issues/new).

## Background reading

+ <a href="https://developers.google.com/apps-script" target="_blank">Google Apps Scripts Basics</a>
+ <a href="https://developers.google.com/apps-script/articles/mail_merge" target="_blank">Simple Mail Merge using Google Sheets</a>

