
# Event Variables

Every OpenBot event is actually a function which gets passed several variables. Those variables belong to the function, so editing them does nothing.

## onCall

### Message

**Type:** Message

**Description:** The message that was sent to activate the command.

### FilteredMessage

**Type:** String

**Description:** The content of the message, excluding the bot prefix and the callname of your command. For example, if Message.content is `-Open Add SomeCommand`, FilteredMessage will be `SomeCommand`

### CurrentLocale

**Type:** Number

**Description:** The index of the locale the user is using, relative to your command. For example, to get the name of your command in the users native language you would put `this.Names[CurrentLocale]`

## onReactAdd / onReactRem

### Reaction

**Type:** MessageReaction

**Description:** The reaction that was added/removed.

### User

**Type:** User

**Description:** The user that added/removed the reaction

## onMemberJoin / onMemberLeave

### Member

**Type:** Member

**Description:** The guild member that joined or left.

## onMemberUpdate / onVoiceUpdate

### OldMember

**Type:** Member

**Description:** The old properties of the member

### NewMember

**Type:** Member

**Description:** The new properties of the member

## onMemberBan / onMemberUnban

### Guild

**Type:** Guild

**Description:** The guild the user was banned/unbanned from

### User

**Type:** User

**Description:** The user that was banned/unbanned

## onBotJoin / onBotLeave

### Guild

**Type:** Guild

**Description:** The guild the bot/command joined/left.

## onChannelCreate / onChannelDelete

### Channel

**Type:** Channel

**Description:** The channel that was created/deleted

## onChannelUpdate

### OldChannel

**Type:** Channel

**Description:** The old properties of the channel

### NewChannel

**Type:** Channel

**Description:** The new properties of the channel

## onMessageDelete / onMessage

### Message

**Type:** Message

**Description:** The message that was deleted or sent

## onPinsUpdate

### Channel

**Type:** Channel

**Description:** The channel whose pins were updated

### Time

**Type:** Time

**Description:** The time of the update

## onEmojiCreate / onEmojiDelete

### Emoji

**Type:** Emoji

**Description:** The emoji that was created/deleted

## onEmojiUpdate

### OldEmoji

**Type:** Emoji

**Description:** The old emoji

### NewEmoji

**Type:** Emoji

**Description:** The new emoji

## onMessageUpdate

### OldMessage

**Type:** Message

**Description:** The old message

### NewMessage

**Type:** Message

**Description:** The new message

## onRoleCreate / onRoleDelete

### Role

**Type:** Role

**Description:** The role that was created/deleted

## onUserUpdate

### OldUser

**Type:** User

**Description:** The old details of the user

### NewUser

**Type:** User

**Description:** The new details of the user

## onGuildUpdate

### OldGuild

**Type:** Guild

**Description:** The old details of the guild

### NewGuild

**Type:** Guild

**Description:** The new details of the guild


# Editable Variables

In addition to function variables, there are some variables accessible to every event that can be edited.


### CurrentUserData

**Type:** <a href="#userdata">UserData</a>

**Description:** The CurrentUserData variable will always contain the UserData of the user who sent the message. Basically it is the result of GetUserData(Message.author). It is also editable, so if you are writing a command like Change Locale, you can just edit the CurrentUserData variable and their locale will be changed

### CurrentGuildData

**Type:** <a href="#guilddata">GuildData</a>

**Description:** The CurrentGuildData variable will always contain the GuildData of the guild which the message is in. Basically it is the result of GetGuildData(Message.guild). It is also editable, so if you are writing a command that needs to change a setting in the guild data, you can just edit the CurrentGuildData variable and their locale will be changed.

# Const Variables

Finally, there are some variables which provide information about OpenBot but cannot be edited.

### GlobInvite

**Type:** String

**Description:** The GlobInvite variable contains the invite link to OpenBot (mainly so i dont forget it) but if you want, make a command to print it out and promote OpenBot

### GlobDiscordClient

**Type:** Client

**Description:** The GlobDiscordClient is the discord.js Client class used to login to OpenBot. You can use it to find out information like how many servers OpenBot is in.

<aside class="warning">Do not attempt to do malicious stuff like grabbing OpenBot's token or anything. Your command will get rejected by the mods. Banne!</aside>

### Analytics

**Type:** <a href="#analytics">Analytics</a>

**Description:** The Analytics object contains information about the bot, its environment, the website, and other random stuff that didnt fit somewhere else.

<aside class="warning">Do not attempt to edit the Analytics object</aside>
