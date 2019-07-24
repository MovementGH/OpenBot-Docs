# Methods

## DebugMessage

> Example: Log if an if statement returns something unexpected

```javascript
var channel=Message.guild.channels.find(channel=>channel.id===GetGuildStore(this,LogChannel));
if(channel) {
    //Log
}
else {
    DebugMessage(this,"Oi ur code is broken the logchannel is not valid");
}
```

The DebugMessage method can be used to DM yourself information for debugging why a command isnt working.

Parameter | Type | Description
--------- | --------- | -----------
Command | <a href="#Command">Command</a> | The command the log belongs to.
Message | String | The message you wish to log

<aside class="note">The Command parameter must always be "this", or the log will not be dmmed to you.</aside>

## GenerateImage

> Example: Get the link to the icon of your command for use in the thumbnail

```javascript
var Embed=new LibDiscord.RichEmbed();
Embed.setThumbnail(GenerateImage(this.Icon));
```
> Your thumbnail will now be something along the lines of this:

```output
https://twemoji.maxcdn.com/2/72x72/1f528.png
or
https://cdn.discordapp.com/emojis/539643411179896835.png
```

The GenerateImage method can be used to turn any discord emoji tag into a URL to a png that you can embed in something.

Parameter | Type | Description
--------- | --------- | -----------
Emoji | String | A discord emoji
### Return Value: String

<aside class="note">This will not work if the user typed a default emoji, as those get sent as unicode characters. To get a url for those you can directly interact with <a href="https://www.npmjs.com/package/twemoji">Twemoji's API</a> by using <a href="#twemoji">LibTwemoj</a>i.</aside>

## GetGuildData

> Example: Get the guild data for your current guild (Yes i know its already available in CurrentGuildData)

```javascript
var GuildData=GetGuildData(Message.guild.id);
```
> The Guild Data will now contain something along the lines of this

```json
{
"GuildID":"506869654493331456",
"GuildName":"OpenBot Development Hub",
"UserCount":"21",
"MessageCount":"6969",
"Prefix":"-Open ",
"AddedCommand": [Object object]
}
```

The GetGuildData method can be used to get the guild data for any guild using a discord.js Guild Object

The GuildData object returned by this method is editable, so you can edit a guild's data if you want to

Parameter | Type | Description
--------- | --------- | -----------
Guild | Guild | The guild whose data you are looking for
### Return Value: <a href="#guilddata">GuildData</a>, or -1 if none was found

## GetUserData

> Example: Get the user data for the sender of the message (Yes i know its already available in CurrentUserData)

```javascript
var UserData=GetUserData(Message.author.id)
```

> The User Data will now contain something along the lines of this

```json
{
"UserID":"473469567323078676",
"UserName":"Movement",
"AvatarURL":"https://cdn.discordapp.com/avatars/473469567323078676/1a679b6f2c447e33133440f1421eb1d0.png?size=2048"
"Locale":"en"
"MessageCount":"1336"
"CommandData": [Object object]
}
```

The GetUserData method can be used to get the user data for any user using a discord.js User Object

The UserData object returned by this method is editable, so you can edit a user's data if you want to

Parameter | Type | Description
--------- | --------- | -----------
User | User | The user whose data you are looking for
### Return Value: <a href="#userdata">UserData</a>, or -1 if none was found

## GetUserStore

> Example: Store a message in a user's data for future reference

```javascript
GetUserStore(this,CurrentUserData.UserID).secretMessage="Hello world!";
```

> Example: Read from a user's data

```javascript
Message.channel.send(GetUserStore(this,CurrentUserData.UserID).secretMessage);
```

The GetUserStore method gets a container that you can use to store data about a user for use in the future. The variable it returns is editable.

If you dont have any data stored, this method will return a blank object that you can edit.

The object returned by this method is owned by you, not your command, so it will be the same object regardless of which of your commands calls it. This makes it a convenient way to share data between your commands.

Parameter | Type | Description
--------- | --------- | -----------
Command | <a href="#command">Command</a> | The command accessing the data
UserID | Number | The ID of the user whos data you want to access.
### Return Value: Object

<aside class="warning">The command parameter must be 'this' or your command will be denied</aside>

## GetGuildStore

> Example: Store a message in a guild's data for future reference

```javascript
GetGuildStore(this,CurrentGuildData.GuildID).secretMessage="Hello world!";
```

> Example: Read from a guild's data

```javascript
Message.channel.send(GetGuildStore(this,CurrentGuildData.GuildID).secretMessage);
```

The GetGuildStore method gets a container that you can use to store data about a guild for use in the future. The variable it returns is editable.

If you dont have any data stored, this method will return a blank object that you can edit.

The object returned by this method is owned by you, not your command, so it will be the same object regardless of which of your commands calls it. This makes it a convenient way to share data between your commands.

Parameter | Type | Description
--------- | --------- | -----------
Command | <a href="#command">Command</a> | The command accessing the data
GuildID | Number | The ID of the guild whos data you want to access.
### Return Value: Object

<aside class="warning">The command parameter must be 'this' or your command will be denied</aside>

## GetTempUserStore

> Example: Store a message in a user's data for future reference

```javascript
GetUserStore(this,CurrentUserData.UserID).secretMessage="Hello world!";
```

> Example: Read from a user's data

```javascript
Message.channel.send(GetUserStore(this,CurrentUserData.UserID).secretMessage);
```

The GetUserStore method gets a container that you can use to store data about a user for use in the future. The variable it returns is editable.

If you dont have any data stored, this method will return a blank object that you can edit.

The object returned by this method is owned by you, not your command, so it will be the same object regardless of which of your commands calls it. This makes it a convenient way to share data between your commands.

Note: the data stored in GetTempUserStore isnt saved when the bot restarts.

Parameter | Type | Description
--------- | --------- | -----------
Command | <a href="#command">Command</a> | The command accessing the data
UserID | Number | The ID of the user whos data you want to access.
### Return Value: Object

<aside class="warning">The command parameter must be 'this' or your command will be denied</aside>

## GetTempGuildStore

> Example: Store a message in a guild's data for future reference

```javascript
GetGuildStore(this,CurrentGuildData.GuildID).secretMessage="Hello world!";
```

> Example: Read from a guild's data

```javascript
Message.channel.send(GetGuildStore(this,CurrentGuildData.GuildID).secretMessage);
```

The GetGuildStore method gets a container that you can use to store data about a guild for use in the future. The variable it returns is editable.

If you dont have any data stored, this method will return a blank object that you can edit.

The object returned by this method is owned by you, not your command, so it will be the same object regardless of which of your commands calls it. This makes it a convenient way to share data between your commands.

Note: the data stored in GetTempGuildStore isnt saved when the bot restarts.

Parameter | Type | Description
--------- | --------- | -----------
Command | <a href="#command">Command</a> | The command accessing the data
GuildID | Number | The ID of the guild whos data you want to access.
### Return Value: Object

<aside class="warning">The command parameter must be 'this' or your command will be denied</aside>

## GetPrivateStorage

> Example: Get an API key that you stored in private storage

```javascript
SomeYoutubeLib.Authenticate(GetPrivateStorage(this,'YoutubeAPIKey'));
```
The GetPrivateStorage method gets the private storage value of whatever key you provide. You can setup private storage in your user settings on the website.

Note: the data returned is readonly

Parameter | Type | Description
--------- | --------- | -----------
Command | <a href="#command">Command</a> | The command accessing the storage
Key | String | The key you registered the data under in user settings
### Return Value: String

<aside class="warning">The command parameter must be 'this' or your command will be denied</aside>

## GetUserVotes

> Example: Get the number of times a user has voted

```javascript
Message.channel.send(GetUserVotes(CurrentUserData.UserID,0).length);
```

> This could output something like this

```output
69
```

The GetUserVotes method gets an array of every vote a user has made that meets the type requirements

The Type parameter can be either -1, 0, or 1. -1 only returns downvotes, 0 returns all votes, 1 only returns upvotes.

Parameter | Type | Description
--------- | --------- | -----------
UserID | Number | The ID of the user whose votes you want to access
Type | Number | The filter you want to apply

## GetCommandVotes

> Example: Get the number of upvotes your command has

```javascript
Message.channel.send(GetCommandVotes(this.ID,1).length);
```

> This could output something like this

```output
66
```

The GetCommandVotes method gets an array of every vote that has been submitted to a command

The Type parameter can be either -1, 0, or 1. -1 only returns downvotes, 0 returns all votes, 1 only returns upvotes.

Parameter | Type | Description
--------- | --------- | -----------
CommandID | Number | The id of the command whose votes you want to access
Type | Number | The filter you want to apply

## GetUserHasVoted

> Example: Find out if the person calling your command has voted on it

```javascript
Message.channel.send(GetUserHasVoted(CurrentUserData.UserID,this.ID))
```

> This could output something like this

```output
false
```

The GetUserHasVoted method returns a bool containing whether or not the user specified has voted on the command specified

Parameter | Type | Description
--------- | --------- | -----------
UserID | Number | The User whose vote you want to check
CommandID | Number | The Command you want to check on

## GetCommandInstalls

> Example: Get the number of servers your command is in

```javascript
Message.channel.send(GetCommandInstalls(this.ID));
```

> This could output something like this

```output
22
```

The GetCommandInstalls method returns the number of servers your command is installed in

Parameter | Type | Description
--------- | --------- | -----------
CommandID | Number | The ID of the command you wish to get the number of installs for

## FindLocale

> Example: Get the proper locale to use for printing out the command's name (Yes i know its already available in CurrentLocale)

```javascript
Message.channel.send(this.Names[FindLocale(this,CurrentUserData.Locale)]);
```

> This could output any of these things depending on the locale of the user

```output
Add Command
or
Agregar Comando
```
The FindLocale method can be used to get the ID of the locale you should be using to communicate with the user. If the command you pass to it does not support the locale of the user, it returns the commands first locale.

The locale you should be using for your command is already available under the variable CurrentLocale, but you can use FindLocale if you want to print the name of a different command (For example if you are writing a help command)

Parameter | Type | Description
--------- | --------- | -----------
Command | <a href="#command">Command</a> | The command you wish to find a locale for
Locale | String | The locale you wish to find
### Return Value: Number

## FindCommand

> Example: Find a cool command with the ID 66

```javascript
Message.channel.send(FindCommand(66).Names[0])
```

> This could output something like this

```output
Illuminati Command
```

The FindCommand method can be used to find a command using its ID.

Parameter | Type | Description
--------- | --------- | -----------
ID | Number | The id of the command you are looking for
### Return Value: <a href="#command">Command</a>, or -1 if none was found

## FindCommandIndex

> Example: Find out where your command is stored in the command mapping

```javascript
Message.channel.send(FindCommandIndex(this.ID));
```

>This could output something like this

```output
4
```

The FindCommandIndex method can be used to find the index of your command in the CacheCommands array

Parameter | Type | Description
--------- | --------- | -----------
ID | Number | The id of the command you are looking for
### Return Value: Number

## FindUser

> Example: Display the username of the caller of the command (Or you could just use CurrentUserData)

```javascript
Message.channel.send(FindUser(Message.author.id).UserName)
```
> This could output something like this

```output
Movement
```

The FindUser method can be used to get a User's Data using their ID

Parameter | Type | Description
--------- | --------- | -----------
ID | Number | The id of the user you are looking for
### Return Value: <a href="#userdata">UserData</a>

## FindGuild

> Example: Display the name of the guild the message was sent in (Or you could jsut use CurrentGuildData)

```javascript
Message.channel.send(FindGuild(Message.guild.id).GuildName)
```
> This could output something like this

```output
OpenBot Development Hub
```

The FindGuild method can be used to get a Guild's Data using its ID

Parameter | Type | Description
--------- | --------- | -----------
ID | Number | The id of the guild you are looking for
### Return Value: <a href="#guilddata">GuildData</a>
