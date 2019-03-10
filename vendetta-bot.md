# Vendetta Management

This document is an overview of the Vendetta Management bot and its features. Down below, you will find out how to configure and customize the bot regarding moderation, applications, etc.

## Disclaimer
The source code for this bot is not to be resold, redistributed or modified and claimed as your own. You may remodify the source code as you wish, but I will not be held liable for anything that breaks due to a change you made.

If you find any issues with the bot, please let me know within **72 hours** so they may be fixed at no charge at all. Anything afterward will be charged accordingly.

Any new updates regarding the core functionality of the bot will be made at no charge if requested (ex. updating the code's library or a security patch). However, any new features will be charged based on the requested features.

## Bot Permissions
By default, the bot is assigned the `Administrator [Administrator]` permission. Reason being, some of the functionality (moving tickets, deleting channels, etc) requires unhindered permission access. The bot will only have the permissions it needs for full functionality. It is recommended to keep the permission(s) unchanged.

- Administrator `ADMINISTRATOR`

## Setup
To set up the bot, there are a few things you must do.

### Setting Up & Running The Bot (Read the sections below this first)
You will need to make sure you have Node installed. Head to this website and downloaded the `LTS` version. Once that process has been completed, you may continue on.

To build the bot's database and run the bot, you will need to run the commands below (the same folder as the `package.json` file)
```bash
npm install --global pm2 # pm2 is a process management tool
npm install # wait until install is finished
node db/dbInit -f # this will build the database and its tables
pm2 start vendetta.json # this is to start the bot's process
```
You can stop the bot at anytime by running `pm2 stop vendetta.json`.

### Environment File
Included in the file is a `.env.example` file. This file contains the bot's token and the database information. Add in the bot token you created in the Developer Portal after `CLIENT_TOKEN=` and the bot owner account's ID after `OWNER=`.

After that, save the file. From here, you will have to rename the file to `.env`. Natively, you cannot do this in Windows (I believe you can on Mac). To rename the file, do this:

In the bot's folder, shift + right-click inside the folder and click "Open PowerShell window here". Then type in the command below.
```bash
mv .env.example .env
```
This will properly rename the file so the bot's process can use the variables inside of that file. Once you have that setup, proceed to the `config.js` file.

### Config File
Included is a `config.js` file where you can customize the main parts of the bot:

- Embed colors
- Prefix, log channels, mod roles, etc

Make sure to go through this file and update the values as you wish. Make sure the roles, channels, etc. are already created when you do update these variables.

**Parameters**  
Some of the messages have parameters. If these parameters are included in a message, they'll be replaced by the bot with the proper information. For example:
```md
# Input
Hello, {{user}}. Welcome to {{guild}}!

# Output
Hello, anthony#8577! Welcome to Vendetta Official Discord!
```
The current parameters are this
- `{{user}}` will be replaced with the user mention
- `{{guild}}` will be replaced with the name of the guild

**Application Emojis**  
There's a section where you can list the approve/reject emojis for applications. These emojis are displayed in a list of objects. Here's all you need to know:

The name is where the name of the emoji (Ex. `nerd`) or the Unicode format (Ex. `🤓`) should go. If the emoji is custom, just provide the name of the emoji.

**Moderation Roles**  
You can provide a list of roles that have access to moderation commands such as banning users, purging channel messages and closing applications. All you need to do is provide the name of the roles in a comma-separated list as shown in the `modRoles` section.

**Applications**  
You can customize various application-related messages. Such as the messages a user should receive when their application has been submitted or approved for an interview. You can also make use of the parameters listed above.

**User Logging**  
There is a section where you can customize the message for the `userLogs` channel. Using the parameters above (or not) the set join message or leave message will be displayed as users join/leave your guild.

### Moderation
The bot comes with a few moderation commands. Moderation commands can only be accessed by users who have the `Administrator [ADMINISTRATOR]` permission or have a role that's configured in the `modLogs` list in the `config.js` file.

- `ban <user> [time] [reason]` Ban a user with an optional timeframe and reason
- `mute <user> [time] [reason]` Mute a user with an optional timeframe and reason
- `kick <user> [reason]` Kick a user with an optional reason
- `unmute <user> [reason]` Unmute a muted user with an optional reason
- `unban <user> [reason]` Unban a user with an optional reason
- `lock <time> [reason]` Lock the channel the command was ran in with a timeframe with an optional reason (moderators bypass this)
- `unlock [reason]` Unlock the channel the command was ran in with an optional reason
- `prune <amount> [type]` Prune a number of messages0 in the channel (max. 200) the command was ran in with an optional filter

![Example of a moderation action with a thumbnail](https://i.imgur.com/TyKWfbp.gif)

![Example of a channel lock and unlock](https://i.imgur.com/DXloNmC.png)

Bans, kick, mutes, unmutes and unbans are all logged in the set mod logs (`modLogs`) channel.

### Applications
Users are able to apply for a position in the faction using the `apply` command. When they run this command in a channel in the guild, the bot will send them a DM with information and the first question. After that, the user will proceed to answer each question.

When they finish all the questions, they will have to confirm their application. The bot will send them back a message with an overview of their application. From there, they can type `confirm` to confirm their application. If they type the `cancel` command or anything other than `confirm`, then the bot will ultimately cancel the application and the user will have to start the process all over again.

When an application is successfully posted, the log message will be sent to the set `appsLogs` channel with an attachment of the application's questions + answers and the actual application will be sent to the `appsChannel` for review by faction officers and leader (aka the roles you added in the `modRoles` list).

![Application confirmation example](https://i.imgur.com/nj9uMMA.png)

From there, faction officers can react to the application to instantly approve the application (this adds the user to the `acceptedRole` role) or instantly reject the application. From there, the applicant will receive a DM from the bot with the status of their application and the status will be logged in the `appsLogs` channel.

![Application log example](https://i.imgur.com/BGVr9yH.png)

Applications can be closed at any time by a user in any of the `modRoles` roles using `applications <open/close>`.


### Assets Files
In the `assets/` folder, there are a few files which are available for customization.

- `applications.json` The status of applications (if users can submit new ones or not) as well as the application questions
- `memes.json` - A list of images to be used for random selection via the `memes` command
- `8ball.json` - Answers for the `8ball` command. 

#### Applications
Used with the `apply` and `applications` commands.

In the `assets/applications.json` file, there are a few sections which you will see:

- `_comment` An internal comment to help you understand the file
- `status` Designates if applications are closed or not via a `true` or `false` value (this is updated via the `applications` command)
- `questions` A list of questions that can be used

In the `questions` list, just make sure each question object is formatted like this:
```json
{
    "question": "Here is your question!"
}
```
And that you add a comma after each question object.

#### Memes
![Example of the `memes` command](https://i.imgur.com/MFgqbfg.png)

Used with the `memes` command.

In the `assets/memes.json` file, there are these sections:

- `_comment` An internal comment to help you understand the file
- `images` A list of images that can be used

To add a new image, all you have to do is put the link to the image in a pair of **double** quotes:
```json
"images": [
    "https://example.com/image-1.png",
    "https://example.com/image-2.png",
    "https://example.com/image-3.png"
]
```
There are a few default images provided, however, feel free to entirely remove them and add your own.

#### 8Ball
![Example of the `8ball` command](https://i.imgur.com/dSfmEvG.png)

Used with the `8ball` command.

In the `assets/8ball.json` file, there are these sections:

- `_comment` An internal comment to help you understand the file
- `answers` A list of answers that can be used

You can add/remove from this list at your will. Just make sure the answer you choose is wrapped in **double** quotes and you add a comma after each new entry.