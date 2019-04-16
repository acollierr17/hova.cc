# Streamer Bot

This document is an overview of the Streamer Bot and its features. Down below, you will find out how to configure the bot's feature such as creating a bot account, setting up the bot with the Twitch API and configuring the bot for usage in your guild.

## Disclaimer
The source code for this bot is not to be resold, redistributed or modified and claimed as your own. You may remodify the source code as you wish, but I will not be held liable for anything that breaks due to a change you made.

If you find any issues with the bot, please let me know within **72 hours** so they may be fixed at no charge at all. Anything afterward will be charged accordingly.

Any new updates regarding the core functionality of the bot will be made at no charge if requested (ex. updating the code's library or a security patch). However, any new features will be charged based on the requested features.

## Bot Permissions
Down below the permissions the bot will be assigned by default. The bot will only be assigned (by default) the features it needs for full functionality. It is recommended to keep the permission(s) unchanged.

- Send Messages `SEND MESSAGES`
- Read Text Channels & See Voice Channels `VIEW_CHANNELS`
- Embed Links `EMBED_LINKS`

## Setup
To set up the bot, there are a few thnigs you must do.

### Creating A Discord Bot Application
You will need to create a bot application to use this bot. If you are unfamiliar on how to do so, please read this [Step #1 of this article](https://anidiots.guide/getting-started/getting-started-long-version#step-1-creating-your-app-and-bot-account).

### Creating A Twitch Application
For stream data, you will need to set up a Twitch application to use the Twitch API. Please refer to [this page](https://dev.twitch.tv/docs/api/) on how to do so.

### Setting Up & Running The Bot
You will need to make sure you have Node installed. Head to [this website](https://nodejs.org/en/) and downloaded the `LTS` version. Once that process has been completed, you may continue on.

Once you have completed the steps above, you will need to run the command `npm install` in command prompt/terminal depending on your operating system. Make sure you're in the folder where the `package.json` file exists before doing anything else.

Next, rename/copy the file from `config.js.example` to `config.js`. The `config.js` file is where you will be changing your bot's configuration. Fill in these three settings with the information above as well as any other default settings you wish to change.
```js
module.exports = {
    ...
    // The Discord bot token from above
    token: '',
    // The Twitch Client ID from above
    twitch: ''
    ...
};
```

To start the bot, simply run the command `pm2 start streamer.json`. Here are some general commands:
- `pm2 stop streamer-bot` to stop the bot
- `pm2 restart streamer-bot` to restart the bot

## Configuration
You can configure various aspects of the bot such as:
- The channel for live notifications to be sent to
- An optional tag for notifications (a specific role, `@everyone` or `@here`)
- The message for live notifications

### Commands
Here is the `help` menu where you can see overall information about the bot:
![`help` Command](https://i.imgur.com/j3W78l0.png)

### Adding/Removing Streamers
You can add/remove streamers via the `streamer` command. Usage goes as `streamer <url>` where `<url>` is the link to the channel of the streamer. The bot will automatically add/remove the streamer from the database depending on if they exist in the database or not.

If the channel does not exist whatsoever, then the bot will respond letting you know. Otherwise, the bot will send a message to let you know that the streamer either has been added or removed.

![Streamer Added](https://i.imgur.com/DoyW78l.png)

![Streamer Removed](https://i.imgur.com/2yCAufm.png)

### Notification Channel
You can set the channel where you wish for notifications to be posted. By default, the bot searches for a `#notifications` channel. But you can easily change this by doing `channel <channel>`.

How notification will work is every 5 seconds, the bot will check the status of all streamers. If a user has gone live within last 2 minutes, a notification will be posted in notifications channel. Otherwise, the bot will not post the user is live if they're already live or not live at all.

### Custom Message
You can set a custom message to be used when a streamer goes live. When setting a message, you must include these 2 parameters:

- `{{user}}` this will be replaced with the username of the streamer
- `{{channel}}` this will be replaced with the URL of the streamer's channel

You can view the current message by doing `message` or set a new one doing `message <message>`.

### Toggle Notifications
If you wish to toggle notifications, you can use `toggle`. This will not post any notifications going forward until you run the command again.

### View All Streamers
You can view a list of all streamers and their channel links via the `streamers` command.

![`streamers` command](https://i.imgur.com/qrRZPVX.png)

### Prefix
If you forget the prefix of the bot, you can simply mention your bot (ex. `@Streamer Bot`) and it will return a message telling you the prefix.

![Get the prefix if you forgot it](https://i.imgur.com/PubVAE3.png)

You can also view the bot's prefix via the `prefix` command.

If you wish to change the bot's prefix, do `prefix <prefix>`.