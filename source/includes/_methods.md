# Methods

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

<aside class="note">This will not work if the user typed a default emoji, as those get sent as unicode characters. To get a url for those you can directly interact with <a href="https://www.npmjs.com/package/twemoji">Twemoji's API</a> by using LibTwemoji.</aside>

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

The GetGuildData method can be used to get the guild data for any guild by searching for that guild's ID.

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

The GetUserData method can be used to get the user data for any user by searching for that user's ID.

The UserData object returned by this method is editable, so you can edit a user's data if you want to

Parameter | Type | Description
--------- | --------- | -----------
User | User | The user whose data you are looking for

### Return Value: <a href="#userdata">UserData</a>, or -1 if none was found

## FindLocale

> Example: Get the proper locale to use for printing out the command's name (Yes i know its already available in CurrentLocale)

```javascript
console.log(this.Names[FindLocale(this,CurrentUserLocale)]);
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
console.log(FindCommand(66).Names[0])
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
console.log(FindCommandIndex(this.ID));
```

>This could output something like this

```output
4
```

The FindCommandIndex method can be used to find the index of your command in the CacheCommands array

Parameter | Type | Description
--------- | --------- | -----------
ID | Number | The id of the command you are looking for

