# Josh Bot

This is a simple guide on how the Josh Bot works and is structured. Down below, you'll find exactly how to set up the bot for tickets and ticket management as well as other commands of the bot.

## Disclaimer
The source code for this bot is not to be resold, redistributed or modified and claimed as your own. You may remodify the source code as you wish, but I will not be held liable for anything that breaks due to a change you made.

If you find any issues with the bot, please let me know within **72 hours** so they may be fixed at no charge at all. Anything afterward will be charged accordingly.

Any new updates regarding the core functionality of the bot will be made at no charge if requested. However, any new features will be charged based on the requested features.

## Bot Permissions
By default, the bot is assigned the `Administrator [ADMINISTRATOR]` permission. Reason being, some functionality, such as bulk deleting messages using the `-embed` command and proper channel management with the ticket system. The bot only will have the permissions it needs for full functionality. It is recommended to keep the permission unchanged.

- Administrator `ADMINISTRATOR`

## Embed Command
With this bot, you have the ability to create embeds and post them a channel of your choice. Simply type in the `-embed` command and follow the process.

For colors, you may refer to the list below. You may type in the color in whatever fashion you want, but make sure it's on this list and you include an `_` in the color, or it's a valid [hexidecimal color](https://www.mathsisfun.com/hexadecimal-decimal-colors.html).
```
[
  'DEFAULT',
  'AQUA',
  'GREEN',
  'BLUE',
  'PURPLE',
  'LUMINOUS_VIVID_PINK',
  'GOLD',
  'ORANGE',
  'RED',
  'GREY',
  'DARKER_GREY',
  'NAVY',
  'DARK_AQUA',
  'DARK_GREEN',
  'DARK_BLUE',
  'DARK_PURPLE',
  'DARK_VIVID_PINK',
  'DARK_GOLD',
  'DARK_ORANGE',
  'DARK_RED',
  'DARK_GREY',
  'LIGHT_GREY',
  'DARK_NAVY',
  'RANDOM',
]
```

## Setup
When you invite the bot to your server, you will need to set up a few things
- Your desired prefix
- The category will ticket channels will go
- The channel where ticket logs will be posted
- The role that will be added to a ticket upon creation

### The prefix
The default bot prefix is `-`. But you may change it at any time by using the `setprefix` command. Usage is below:
```
-setprefix <prefix>
```
The bot's mention `(@Josh Bot#8286)` may also be used as a prefix for commands:
```
@Josh Bot#8286 ping
```
If you ever forget the bot's prefix, simply mention it to see what it is.

### Tickets category
All new tickets will be posted under a category at your choosing. By default, the category the bot will search for is `Tickets`. You may set a new tickets category by using the `setcategory` command.
```
-setcategory <category>
```

### Tickets logs
When a ticket is created or closed, it will be logged to a set ticket logs channel. By default, the channel the bot will search for is `ticket-logs`. You may set a new tickets logs channel by using the `setlogs` command.
```
-setlogs <channel>
```

### Tickets staff role
A staff role is to be set when using tickets. This role will automatically be added to the ticket when it's created. However, server admins (users who have the `Manage Server [MANAGE_GUILD]`) will be added automatically. You may add or remove the tickets staff role by using the `role` command.
```
-role <add/remove> <role>
```
If you wish to view all server admins and the staff role, you may run the `roles` command. It'll display an embedded message of said information.