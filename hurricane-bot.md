# Hurricane Bot

This document is an overview of the Hurricane bot and its features. Down below, you will find out how to configure the bots core features such as invoicing (provided by PayPal) and ticket management (which is what this bot is specialized in).

## Disclaimer
The source code for this bot is not to be resold, redistributed or modified and claimed as your own. You may remodify the source code as you wish, but I will not be held liable for anything that breaks due to a change you made.

If you find any issues with the bot, please let me know within **72 hours** so they may be fixed at no charge at all. Anything afterward will be charged accordingly.

Any new updates regarding the core functionality of the bot will be made at no charge if requested (ex. updating the code's library or a security patch). However, any new features will be charged based on the requested features.

## Bot Permissions
By default, the bot is assigned the `Administrator [Administrator]` permission. Reason being, some of the functionality (moving tickets, deleting channels, etc) requires unhindered permission access. The bot will only have the permissions it needs for full functionality. It is recommended to keep the permission(s) unchanged.

- Administrator `ADMINISTRATOR`

## Invoicing + the PayPal API
Freelancers and Managers have the ability to create invoices and track them within the bot. Creating invoices is as simple as using the `invoice` command. The usage is:
```
-invoice <client email> <price> <the item>
```
Once this command is executed, it will go through the process to create a draft of the invoice and then send it. In return, a bot will post a message with a link to the invoice and its status.

When the invoice is paid, the bot will update the message to reflect the invoice status. This feature makes it so managers don't specifically have to preside over the creation of an invoice.

To use this feature, a Developer Application will have to be created via the Paypal Developer Dashboard. Continue on in this section to find out more on how to do this.

To create a new Application, proceed over to the [Developer Dashboard](https://developer.paypal.com/developer/applications). Once you are there, scroll down to the *REST API apps* section. You will need to create this application as this is how the bot interacts with PayPal. From there, click *Create App*

![](https://i.imgur.com/amj0Smp.png)

In the *Create New App* box, enter the name for an app. Then click *Create App*.

![](https://i.imgur.com/xLiInYk.png)

Now you will be on the page for the REST API application you have created. Click the *Live* tab. You **must** click this tab and use the credentials associated with it for invoicing to properly work.

Once you are on the *Live* tab, you will see the Client ID and Secret. Click *Show* below the Secret section to expose the Secret. You will need both of these to set up invoicing in the bot.

*Note: Please keep these credentials secured. When you do setup up the bot, make sure to run these commands in a secured channel so users who don't need to see these credentials don't see them.*

![](https://i.imgur.com/fR0yMJo.png)

Now that you have these credentials, run the `paypalconfig` command in a channel on Discord. A wizard will begin where you will enter the Client ID and Secret. Once they have been successfully entered, you should be almost good to go.

The last step is to set up the merchant email/PayPal account that will be associated with invoicing. The account that you set **must** be the same as the one displayed when you created the REST API app above. To set the email, run this command:
```
-setemail <email>
```
Now you should be in the clear for invoicing!

## Ticket Management
This bot is set up for extensive ticket management. This meaning, you can set up specific roles to be assigned to a specific ticket and change the different categories that tickets will be assigned to.

For example, if you want to set up a role that will only be able to view HR tickets, you would do `setrole 2 <role>`. Where `2` represents `HR` and `role` represents what role.

If you want to change the default Tickets category, you can do `setcategory tickets <category>`.

Managers can also manually create commissions using `commission`. Once posted, a freelancer will be able to claim that commission. Upon claiming the commission, a new ticket channel will be created, just like if a client were to open a ticket using the `ticket` command.

Other commands that can be used is `add` and `remove`. These commands are self-explanatory. They simple add or remove a user from a ticket channel.

## Freelancer Portfolio
Clients can view the portfolio of a freelancer using the `portfolio` command. This simply displays a link that the freelancer can set using the `setportfolio` command. The portfolio can be updated and changed at anytime by the freelancer. As the `portfolio` command can be used by anyone, only freelancers can use the `setportfolio` command.

## Ticket Functionality
When a new ticket is created, multiple things happen at once:
- A channel is created
- The channel is moved to the category associated with the ticket
- All roles are added associated with the ticket type as well as users in the `Management 💼` role by default and the configured global role
- A wizard begins where the client can proceed with their ticket

At anytime during the wizard, the client can cancel the ticket by typing `cancel`. However, for efficiency of the database, the ticket *won't* be submitted to the database until *after* the user types `finish` (or any further notes) at the end of the wizard.

If a user types in `cancel`, the ticket will automatically be deleted after 10 seconds. However, when closing a ticket (tickets can only be closed if they exist in the database) there are two options:

- Graceful closing of the ticket using the `close` command*
- Forceful closing of the ticket using the `fclose` command*

**A reason must be provided*

When doing a graceful closing of the ticket, a 3-minute timer will begin. If now messages are sent 3 minutes after the `close` command was initiated, the ticket will close. However, if a message was sent afterward, the ticket will not continue to close and it will remain open.

## Other configuration
Not only can the ticket roles and ticket channels be configured, the ticket logs channel and bot prefix can be changed as well with the `setlogs` and `setprefix` command. Keep in mind that configuring the bot can only be done by users who are in the `Management 💼` role. To view all accessible bot commands, run the `help` command. You can see the information for a specific command using `help <command>`.
