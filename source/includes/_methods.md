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

The GenerateImage method can be used to turn any discord emoji tag into a png that you can embed in something.

Parameter | Type | Description
--------- | --------- | -----------
Emoji | String | A discord emoji

Return Type: String
Return Value: URL to image of emoji, or URL to discord icon if none is found

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

Parameter | Type | Description
--------- | --------- | -----------
GuildID | Number | The ID of the guild you are looking for

Return Type: Number or <a href="#guilddata">GuildData</a>
Return Value: Data of the guild, or -1 if no guild was found

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

Parameter | Type | Description
--------- | --------- | -----------
UserID | Number | The ID of the user you are looking for

Return Type: Number or <a href="#userdata">UserData</a>
Return Value: Data of the guild, or -1 if no guild was found
