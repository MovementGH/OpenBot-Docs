---
title: OpenBot API

language_tabs:
  - javascript

toc_footers:
  - <a href='../'>Start Using OpenBot</a>
  - <a href='https://github.com/lord/slate'>Powered by Slate</a>

includes:

search: true
---

# Getting Started

## Welcome

Welcome to the OpenBot API Documentation. We hope everything on this page is clear, but if you dont understand something, want to suggest a change, addition, etc, you can go to the <a href="https://discord.gg/CdpzgFX/">OpenBot Support</a> discord server and talk us.

## Prerequirements

OpenBot and its API use quite a few technologies in order to work. You don't need to know all of them in order to make commands, but there are some which you do need to know.

### Required Knowledge: 
- node.js
- discord.js

### Helpful Knowledge:
- rethinkdb

### Things OpenBot uses that you don't need to know
- express.js
- php
- html5/css3
- child_process

We are happy to help you with problems you have while using OpenBot, but if your problems are from lack of required knowledge we will send you to other documentation/tutorials relating to that framework/language, we won't write your commands for you. It is up to you to learn what you need to learn.

## Creating a command

Here are the steps to create a command on the OpenBot website that you can start writing code for.

 - Login
 - Click "Profile" in the upper right corner
 - Click "Settings" under your avatar
 - Enable the slider labeled "Developer Mode"
 - Click "Commands" under your avatar
 - Click "Create Command"
 - Click "Edit" on the command that appears in the list.
 
 
# Command Editor

## MetaData Box

In the top left of the command editor, there is a box which contains the metadata of your command,  including its Icon, Permissions, and Support link. These control how people can see and interact with your command.

### Icon

Your command's icon is displayed next to it in help menus, searches and more. It should relate to your command so that people can tell what it does at a glance. The icon can be any discord emoji. If it is a default emoji, it must be entered into the editor like `:smile:`. If it is a custom emoji, it must be entered in like `<:AddCommand:634475978000695316>` To find the ID of a custom emoji, richt click it in discord and click copy link. The number in the link is the ID of your emoji.

### Support Link

The support link is displayed under your command in information menus. You can set it to a link to the discord server you want people to go to when your command breaks.

The support link must be formatted `https://discordapp.com/invite/abcdef` where abcdef is the invite code.

### Bot Perms

The Bot Perms are the permissions that OpenBot needs in order to run your command. It will prevent your command from running when permissions aren't met, so that you dont need to handle it inside your command. You can calculate the permissions number at the <a href="https://discordapi.com/permissions.html">Discord Permissions Calculator</a>

### User Perms

The User Perms are the permissions that a user needs in order to run your command. It will prevent your command from being used by the wrong people. You can calculate the permissions number at the <a href="https://discordapi.com/permissions.html">Discord Permissions Calculator</a>

### Open Source

If your command is marked as open source, other users will be able to view its code on the website and see how you work your magic.

### Pull Requests

If your command is marked as allowing pull requests, other users will be able to edit its code on the website. You will be notified of all edits, with the option to accept or deny them.

## Language Support Box

In the top right of the command editor, there is a box which contains the language data of your command, including its Names, Callnames, Descriptions, and more. These let you translate your command into multiple languages!

<aside type="note">If you are having difficulties scrolling sideways through the tabs, you can hold shift and scoll up/down and it will scroll sideways</aside>

### Name

The name of your command is... well... its name. It defines how users search for your command, and how it appears in the help menu.

### Callname

The callname of your command is what people use to execute it. For example, a command with a callname of "Help" is executed using `-Open Help`. Your callname should generally be pretty short, to make typing it easy.

### Command Description

The description is a place to let your inner author roam free, and tell the world the intracies of your command.

### Command Syntax

The syntax of your command is displayed after its name in help menus, searches, etc. It should tell users what arguments your command accepts. For example, the syntax for a kick command would be similar to `[@Mention]`. The square brackets indicate a required parameter which is a mention of a user.

Formatting:

**[Param]** - Required parameter
**{Param}** - Optional parameter
**Param** - Literall text (write Param)
**(Note)** - Note (ie you can use `(No Arguments)` to indicate that your command doesnt expect and parameters

### Translation Strings

> Example: How to use translation strings

```javascript
//Access String 0
this.Languages[LibOpenBot.LanguageIndex(this,BotContext.User.Settings.Language].Strings[0];

//Make a reference to the strings for cleaner code
var Strings=this.Languages[LibOpenBot.LanguageIndex(this,BotContext.User.Settings.Language].Strings;
//Later...
Strings[0];
```
Translation strings allow the text inside your command to be translated. You can have as many as you want, and you can access them from your code.

## Event Box

Your command can have multiple events, or just one. These are where you put your code. You can find a description of what the different events do below.

# Events

> Example: Log to the console

```javascript
console.log('This event was called!');
```

Events are among the most important things in OpenBot. They define the actions that the bot takes. Every event is actually a function which gets passed several variables and has scope to an OpenBot shard. You don't need to write the function, you can treat the code block as if it is directly executed. Ie this code would log to the console every time it was executed.


## Universal

All events receive certain variables, regardless of their type. Here they are:

### Context

**Type:** Object

**Description:** The context contains discord.js objects relevent to the event.

**Children:**  guild, channel\*, user\*
 
 \*May be null
 
### BotContext
 
 **Type:** Object
 
 **Description:** The BotContext contains OpenBot objects relevent to the event
 
 **Children:** Guild, User\*
 
\*May be null

### this

**Type:** Command

**Description:** When in an event, `this` refers to the command whose event is being executed

## Call 

The Call event is executed whenever a message matches Prefix+Callname. For example, when someone sends "-Open Help" on a server where the prefix is "-Open", the command with the callname "Help" runs its Call event.

It receives these variables:

### Message

**Type:** Message

**Description:** The message that was sent to activate the command.

### Arguments

**Type:** String

**Description:** The content of the message, excluding the prefix and callname. For example, if message.content is "-Open Add SomeCommand", Arguments will be "SomeCommand"

## ChannelCreate

The ChannelCreate event is executed when a channel is created.

It receives no special variables.

## ChannelDelete

The ChannelDelete event is executed when a channel is deleted.

It receives no special variables.

## ChannelPinsUpdate

The ChannelPinsUpdate event is executed when the pins of a channel are changed.

It receives no special variables.

## ChannelUpdate

The ChannelUpdate event is executed when a channel is updated (eg. Name changed, Permissions changed, etc.)

It receives these variables:

### OldChannel

**Type:** Channel

**Description:** The channel before the update

### NewChannel

**Type:** Channel

**Description:** The channel after the update

## CommandAdded

The CommandAdded event is executed when your command is added to a server.

It recieves no special variables.

## CommandRemoved

The CommandRemoved event is executed when your command is removed from a server.

It receives no special variables.

## CommandUpdated

The CommandUpdated event is executed when your edit request is approved, and your command is integrated into OpenBot. You can use it to update command data if you change formats, or anything else that needs updated.

## EmojiCreate

The EmojiCreate event is executed when an emoji is added to the guild.

It receives these variables:

### Emoji

**Type:** Emoji

**Description:** The emoji that was added.

## EmojiDelete

The EmojiDelete event is executed when an emoji is deleted from the guild.

It receives these variables:

### Emoji

**Type:** Emoji

**Description:** The emoji that was deleted

## EmojiUpdate

The EmojiUpdate event is executed when an emoji in the guild is updated (eg. Name changed, Icon changed, etc.)

It receives these variables:

### OldEmoji

**Type:** Emoji

**Description:** The emoji before the update

### NewEmoji

**Type:** Emoji

**Description:** The emoji after the update

## GuildBanAdd

The GuildBanAdd event is executed when a user is banned from the guild.

It receives no special variables.

## GuildBanRemove

The GuildBanRemove event is executed when a user is unbanned from the guild.

It receives no special variables.

## GuildIntegrationsUpdate

The GuildIntegrationsUpdate event is executed when a guild's integrations are updated.

It receives no special variables.

## GuildMemberAdd

The GuildMemberAdd event is executed when a user joins a guild.

It receives these variables:

### Member

**Type:** Member

**Description:** The member that joined

## GuildMemberRemove

The GuildMemberRemove event is executed when a user leaves or is kicked from a guild.

It receives these variables:

### Member

**Type:** Member

**Description:** The member that left

## GuildMemberSpeaking

The GuildMemberSpeaking event is executed when a user starts/stops speaking.

It receives these variables:

### Member

**Type:** Member

**Description:** The member that started/stopped speaking

### Speaking

**Type:** Boolean

**Description:** Whether they are speaking.

## GuildMemberUpdate

The GuildMemberUpdate event is executed when a member is updated (eg. Nickname changed, Roles changed, etc.)

It receives these variables:

### OldMember

**Type:** Member

**Description:** The member before the update

### NewMember

**Type:** Member

**Description:** The member after the update

## GuildUpdate

The GuildUpdate event is executed when a guild is updated (eg. Name changed, region changed, etc.)

It receives these variables:

### OldGuild 

**Type:** Guild

**Description:** The guild before the update

### NewGuild

**Type:** Guild

**Description:** The guild after the update

## MessageDelete

The MessageDelete event is executed when a message is deleted.

It receives these variables:

### Message

**Type:** Message

**Description:** The message that was deleted

## MessageReactionAdd

The MessageReactionAdd event is executed when a reaction is added to a message.

It receives these variables:

### Reaction

**Type:** MessageReaction

**Description:** The reaction that was added

## MessageReactionRemove

The MessageReactionRemove event is executed when a reaction is removed from a message

It receives these variables:

### Reaction

**Type:** MessageReaction

**Description:** The reaction that was removed

## MessageReactionRemoveAll

The MessageReactionRemoveAll event is executed when all the reactions are removed from a message

It receives these variables:

### Reaction

**Type:** Message

**Description:** The message from which the reactions were removed

## MessageUpdate

The MessageUpdate event is executed when a message is edited

It receives these variables:

### OldMessage

**Type:** Message

**Description:** The message before the edit

### NewMessage

**Type:** Message

**Description:** The message after the edit

## RoleCreate

The RoleCreate event is executed when a role is created

It receives these variables:

### Role

**Type:** Role

**Description:** The role that was created

## RoleDelete

The RoleDelete event is executed when a role is deleted

It receives these variables:

### Role

**Type:** Role

**Description:** The role that was deleted

## RoleUpdate

The RoleUpdate event is executed when a role is updated (eg. Change name, Change permissions, etc.)

It receives these variables:

### OldRole

**Type:** Role

**Description:** The role before the update

### NewRole

**Type:** Role

**Description:** The role after the update

## VoiceStateUpdate

The VoiceStateUpdate event is executed when a user joins or leaves a voice channel, and when they move between voice channel.

It receives these variables:

### OldMember

**Type:** Member

**Description:** The member before the update

### NewMember

**Type:** Member

**Description:** The member after the update

# Classes

## ChannelSetting

The ChannelSetting Class stores information about the settings in a channel. It can either be related to a guild (Guild.Settings.Channels) or a command (Guild.Settings.Commands[x].Channels). It controls whether commands can be used in that Channel.

<aside class='note'>A ChannelSetting stored in a command takes precedence over a ChannelSetting stored in a guild</aside>

Member | Type | Description
-- | -- | --
enabled | Bool | Whether commands can be used in this channel
id | Number | The id of the channel

## Command

> Example: Print the Icon of the current command

```javascript
Message.channel.send(this.Icon);
```

The Command Class stores information about a command, so that it can be executed by a user.

Member | Type | Description
-- | -- | --
Author | Number | The ID of the author of the command
Events | Object | The Events of the command
Icon | String | The Icon of the command
Languages | Array(Object) | The Languages of the command
Permissions | Object | The Permissions of the command
Support | String | The Support link of the command
id | Number | The ID of the command

### Command.Events

The Events member of the Command Class contains the code for whichever events are used by the command. For example, in a command which uees the Call and Message events, the Events member will have two members: Call, and Message.

<aside class='note'>You do not need to directly access the event code to run an event. Instead you can use the RunEvent function</aside>

### Command.Languages

The Languages member of the Command Class contains the strings used by any languages that the command supports. It is an array of Objects that follow this template:

Member | Type | Description
-- | -- | --
Callname | String | The Callname of the command
Description | String | The Description of the command
Language | String | The language that this object defines
Name | String | The Name of the command
Strings | String | The Translation Strings of the command
Syntax | String | The Syntax of the command

### Command.Permissions

The Permissions member of the Command Class has these members:

Member | Type | Description
-- | -- | --
Bot | Number | The permissions the bot must have to run the command
CoreCommand | Bool | Whether the command is a core command
DevsOnly | Bool | Whether the command is locked to developers
Editable | Bool | Whether the command can be edited by others
User | Bool | The permissions a user needs to run the command
Viewable | Bool | Whether the command can be viewed by others

## Emoji

The Emoji class contains information about an emoji, usefull for displaying it on a website as well as in discord.

Member | Type | Description
-- | -- | --
id | Number | The id of the emoji
tag | String | The tag of the emoji in discord
url | String | The url of the emoji on twemoji
utf | String | The utf/unicode character of the emoji

### tag

To use the tag member in discord, you will have to add ":" to each side. For example, the tag might be "arrow_right_hook", so to display it you would do ":"+Emoji.tag+":", which would send ":arrow_right_hook" and be recognized by discord as an emoji.

### url

To use the url member on a page or link, you will have to add the base twemoji url around it. For example, the url member might be "21aa", so you would have to do "https://twemoji.maxcdn.com/2/72.72/"+Emoji.url+".png" to use a 72x72 png. There are also other sizes, as well as svg. You can find them at twemoji's docs.

### utf

To use the utf member in discord or on a page, just print it as a string.



## Guild

The Guild Class contains data relating to a guild that OpenBot is in.

Member | Type | Description
-- | -- | --
Icon | String | The URL to the icon of the guild
Name | String | The Name of the guild
Settings | Object | The Settings of the guild
Stats | Object | The Stats of the guild
id | Number | The id of the guild

### Guild.Settings

The Settings member of the Guild class contains its settings, along with the settings of the commands in it.

Member | Type | Description
-- | -- | --
Admins | Array(Number) | The IDs of the people in the guild who can manage OpenBot
Channels | Array(ChannelSetting) | The Settings for the channels in the guild
Commands | Array(Object) | The Commands that are in the guild
Prefix | String | OpenBot's Prefix in this guild
Searchable | Bool | Whether this guild can be searched on the website

### Guild.Settings.Commands

The Commands member of the Settings object contains the Commands in the guild, as well as their settings.

Member | Type | Description
-- | -- | --
Channels | Array(ChannelSetting) | Command specific settings for the channels in the guild
Data | Object | Data that this command stores about the guild
Settings | Object | The settings for this command.
id | Number | The id of the command

### Guild.Stats

The Stats member of the guild object contains some stats about the guild.

Member | Type | Description
-- | -- | --
Messages | Number | The number of messages OpenBot has processed in this guild
Users | Number | The number of users in this guild

## Locale

The Locale Class represents a Language that OpenBot supports.

Member | Type | Description
-- | -- | --
code | String | The Locale Code
icon | String | The Locale Icon
name | String | The Language name


## PullRequest

The PullRequest class represents a pull request to someone's command.

Member | Type | Description
-- | -- | --
Command | Command | The edited command
Editor | Number | The id of the person who edited it
Notes | String | The notes left by the editor
Owner | Number | The owner of the command
id | Number | The id of the pull request

## Relay

The Relay class represents a relay to another process

Member | Type | Description
-- | -- | --
type | String | The type of relay
data | Object | The data in the relay

### Relay.type

There are several types of relays available:

Name | Data | Description
async | Javascript | Evaluates javascript and returns callback
dbUpdate | Object | Clears old data from cache
eval | Javascript | Evaluates javascript syncronously
restart | Null | Restarts process
stat | Null | Fetches performance information

<aside class="note">For the async relay, instead of sending "1+1" and getting 2, you send "Callback(1+1)" and get 2. Then you can use asyncrounous functions with .then</aside>


## User

The User Class contains data relating to a user of OpenBot.

Member | Type | Description
-- | -- | --
Avatar | String | The link to the user's avatar
Settings | Object | The user's settings
Stats | Object | Some stats about the user
Username | String | The user's username
id | Number | The user's id

### User.Settings

The Settings member of the User Class contains settings relating to a user.

Member | Type | Description
-- | -- | --
DeveloperMode | Bool | Whether the user has Developer Mode enabled on the website
Language | String | The language the user uses
ShowGuilds | Bool | Whether the user shows their guilds on their profile

### User.Stats

The Stats member of the User Class contains some stats relating to a user

Member | Type | Description
-- | -- | --
CommandsUsed | Number | The number of commands the user has used
Messages | Number | The number of messages the user has sent

## UserData

The UserData Class contains data stored by commands, or about commands, relating to a user. It is kept seperate from the User class so that when a User is requested for a profile or something similar, their data is not exposed.

Member | Type | Description
-- | -- | --
Commands | Array(Object) | Data stored by commands
Private | Object | Private storage of the user
id | Number | The id of the user

### UserData.Commands

The Commands member of the UserData Class contains an array of all the data stored by various commands relating to that user, sorted by author.

Member | Type | Description
Author | Number | The author of the command storing the data
Data | Object | The data being stored

### UserData.Private

The Private member of the UserData Class contains all of the Key/Value pairs that a User set on their website. These are used for putting private information in a public command (Like an API key for a music command). It has no defined members, its members are whatever the user defines them to be.

<aside class='note'>You will not need to directly access this object. You can use the LibOpenBot.GetPrivateStorage function to get the members of this object.</aside>


## VerifyRequest

The VerifyRequest Class contains command edits which are waiting for verification by core developers

Member | Type | Description
-- | -- | --
Command | Command | The edited command
Editor | Number | The id of the person who edited it
Message | Number | The id of the verification message
Notes | String | The notes left by the editor
Owner | Number | The id of the owner of the command
id | Number | The id of the verify request

# Functions

## LibOpenBot.sendRelay

The LibOpenBot.sendRelay function sends a message to another process, and retrieves the result.

### Arguments

Argument | Type | Description
-- | -- | --
Proc | String | The Name of the process to send a relay to
Data | Relay | The Relay to send

### Return Value

Promise(Object)

## LibOpenBot.sendRelayShards

The LibOpenBot.sendRelayShards function sends a message to all of the shards and retrieves the result.

### Arguments

Argument | Type | Description
-- | -- | --
Data | Relay | The Relay to send

### Return Value

Promise(Array(Object))

## LibOpenBot.sendRelayAll

The LibOpenBot.sendRelayAll function sends a message to all of the processes and retrieves the result

### Arguments
Argument | Type | Description
-- | -- | --
Data | Relay | The Relay to send
Master | Bool | Whether to send it to the master process
