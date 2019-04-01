# Classes

## UserData

> Example: Printing out a user's Username, ID, and Avatar

```javascript
Message.channel.send(CurrentUserData.UserName);
Message.channel.send(CurrentUserData.UserID);
Message.channel.send(CurrentUserData.AvatarURL);
```
> This will output something along the lines of this:

```output
Movement
473469567323078676
https://cdn.discordapp.com/avatars/473469567323078676/1a679b6f2c447e33133440f1421eb1d0.png?size=2048
```

Information about a user is stored in the UserData class.

Member | Type | Description
--------- | --------- | -----------
UserID | Number | The ID of the user
UserName | String | The Username of the user
AvatarURL | String | The URL of the user's discord avatar
MessageCount | Number | The number of message the user has sent
Locale | String | The locale the user is using
CommandData | Array (<a href="#commanddata">CommandData</a>) | Data stored by commands about this user

## GuildData

> Example: Printing out a guild's Name, ID, and UserCount

```javascript
Message.channel.send(CurrentGuildData.GuildName);
Message.channel.send(CurrentGuildData.GuildID);
Message.channel.send(CurrentGuildData.UserCount);
```

> This will output something along the lines of this:

```output
OpenBot Development Hub
506869654493331456
17
```

Information about a guild is stored in the GuildData class.

Member | Type | Description
--------- | --------- | -----------
GuildID | Number | The ID of the guild
GuildName | String | The Name of the guild
UserCount | Number | The number of users in the guild
MessageCount | Number | The number of messages processed in the guild
Prefix | String | The prefix OpenBot is using in the guild
AddedCommands | Array (Number) | An array of the IDs of commands added to the guild

## CommandData

If your command needs to store information, this is the object you use to store it.

You should use one CommandData per user, even if you have multiple commands. Command Data is meant to be found by looking for your User ID in the CommandData array of the User whos data you want to retreive.

Member | Type | Description
--------- | --------- | -----------
CommandAuthor | Number | The ID of the author storing the data
Data | Object | The data being stored

<aside class="warning">Do not attempt to access CommandData created by other command developers. Doing this will cause your command to get rejected.</aside>

## Command

> Example: Print the name and callname of the current command

```javascript
Message.channel.send(this.Names[CurrentLocale]);
Message.channel.send(this.Uses[CurrentLocale]);
```

> This will output something along the lines of this:

```output
Add Command
Add
```

The most important object in OpenBot. The Command. Stores the information about every command in OpenBot!

Member | Type | Description
--------- | --------- | -----------
ID | Number | The ID of the command
Author | Number | The ID of the author of the command
Names | Array (String) | The names of the command
Uses | Array (String) | The callnames of the command
Descriptions | Array (String) | The descriptions of the command
String | Array (String) | The translation strings of the command
Syntax | String | The syntax of the command
Icon | String | The Icon of the command
SupportLink | String | The link to the command's support server
Version | String | The version of the command
BotPerms | Permission | The permissions required for the bot to execute the command
ExecutePerms | Permission | The permissions required for a user to execute the command
AllowView | Bool | Whether the author allows people to view the source
AllowEdit | Bool | Whether the author allows people to make a pull request
onCall | Function | The function that gets called when the command is executed
Locked | Bool | Whether this function is part of OpenBot's core and cannot be removed
OnlyDevs | Bool | Whether this function can only be called by developers

<aside class='warning'>Do not attempt to edit any Commands. Doing so will cause your command to get rejected.</aside>
