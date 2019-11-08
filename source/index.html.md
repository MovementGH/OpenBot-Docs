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

 - Go to <a href="https://openbot.ga/">the website</a>
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

<aside class="note">All fields are required. You WILL get an error if you try to submit a command with an empty field</aside>

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

<aside class="note">All fields are required. You WILL get an error if you try to submit a command with an empty field</aside>

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

<aside type="note">If you are having difficulties scrolling sideways through the tabs, you can hold shift and scoll up/down and it will scroll sideways</aside>

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

**Children:**  <a href="https://discord.js.org/#/docs/main/stable/class/Guild">guild</a>, <a href="https://discord.js.org/#/docs/main/stable/class/Channel">channel</a>\*, <a href="https://discord.js.org/#/docs/main/stable/class/User">user</a>\*
 
 \*May be null
 
### BotContext
 
 **Type:** Object
 
 **Description:** The BotContext contains OpenBot objects relevent to the event
 
 **Children:** <a href="#guild">Guild</a>, <a href="#user">User</a>\*
 
\*May be null

### this

**Type:** <a href="#command">Command</a>

**Description:** When in an event, `this` refers to the command whose event is being executed

## Call 

The Call event is executed whenever a message matches Prefix+Callname. For example, when someone sends "-Open Help" on a server where the prefix is "-Open", the command with the callname "Help" runs its Call event.

It receives these variables:

### Message

**Type:** <a href="https://discord.js.org/#/docs/main/stable/class/Message">Message</a>

**Description:** The message that was sent to activate the command.

**Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a>

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

**Type:** <a href="https://discord.js.org/#/docs/main/stable/class/Channel">Channel</a>

**Description:** The channel before the update

### NewChannel

**Type:** <a href="https://discord.js.org/#/docs/main/stable/class/Channel">Channel</a>

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

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Emoji">Emoji</a>

**Description:** The emoji that was added.

## EmojiDelete

The EmojiDelete event is executed when an emoji is deleted from the guild.

It receives these variables:

### Emoji

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Emoji">Emoji</a>

**Description:** The emoji that was deleted

## EmojiUpdate

The EmojiUpdate event is executed when an emoji in the guild is updated (eg. Name changed, Icon changed, etc.)

It receives these variables:

### OldEmoji

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Emoji">Emoji</a>

**Description:** The emoji before the update

### NewEmoji

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Emoji">Emoji</a>

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

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/GuildMember">Member</a>

**Description:** The member that joined

## GuildMemberRemove

The GuildMemberRemove event is executed when a user leaves or is kicked from a guild.

It receives these variables:

### Member

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/GuildMember">Member</a>

**Description:** The member that left

## GuildMemberSpeaking

The GuildMemberSpeaking event is executed when a user starts/stops speaking.

It receives these variables:

### Member

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/GuildMember">Member</a>

**Description:** The member that started/stopped speaking

### Speaking

**Type:** Boolean

**Description:** Whether they are speaking.

## GuildMemberUpdate

The GuildMemberUpdate event is executed when a member is updated (eg. Nickname changed, Roles changed, etc.)

It receives these variables:

### OldMember

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/GuildMember">Member</a>

**Description:** The member before the update

### NewMember

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/GuildMember">Member</a>

**Description:** The member after the update

## GuildUpdate

The GuildUpdate event is executed when a guild is updated (eg. Name changed, region changed, etc.)

It receives these variables:

### OldGuild 

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Guild">Guild</a>

**Description:** The guild before the update

### NewGuild

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Guild">Guild</a>

**Description:** The guild after the update

## MessageDelete

The MessageDelete event is executed when a message is deleted.

It receives these variables:

### Message

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Message">Message</a>

**Description:** The message that was deleted

## MessageReactionAdd

The MessageReactionAdd event is executed when a reaction is added to a message.

It receives these variables:

### Reaction

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/MessageReaction">MessageReaction</a>

**Description:** The reaction that was added

## MessageReactionRemove

The MessageReactionRemove event is executed when a reaction is removed from a message

It receives these variables:

### Reaction

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/MessageReaction">MessageReaction</a>

**Description:** The reaction that was removed

## MessageReactionRemoveAll

The MessageReactionRemoveAll event is executed when all the reactions are removed from a message

It receives these variables:

### Reaction

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Message">Message</a>

**Description:** The message from which the reactions were removed

## MessageUpdate

The MessageUpdate event is executed when a message is edited

It receives these variables:

### OldMessage

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Message">Message</a>

**Description:** The message before the edit

### NewMessage

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Message">Message</a>

**Description:** The message after the edit

## RoleCreate

The RoleCreate event is executed when a role is created

It receives these variables:

### Role

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Role">Role</a>

**Description:** The role that was created

## RoleDelete

The RoleDelete event is executed when a role is deleted

It receives these variables:

### Role

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Role">Role</a>

**Description:** The role that was deleted

## RoleUpdate

The RoleUpdate event is executed when a role is updated (eg. Change name, Change permissions, etc.)

It receives these variables:

### OldRole

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Role">Role</a>

**Description:** The role before the update

### NewRole

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Role">Role</a>

**Description:** The role after the update

## VoiceStateUpdate

The VoiceStateUpdate event is executed when a user joins or leaves a voice channel, and when they move between voice channel.

It receives these variables:

### OldMember

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Member">Member</a>

**Description:** The member before the update

### NewMember

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Member">Member</a>

**Description:** The member after the update

# Classes

## ChannelSetting

The ChannelSetting Class stores information about the settings in a channel. It can either be related to a guild (Guild.Settings.Channels) or a command (Guild.Settings.Commands[x].Channels). It controls whether commands can be used in that Channel.

<aside class='note'>A ChannelSetting stored in a command takes precedence over a ChannelSetting stored in a guild</aside>

Member | Type | Description
-- | -- | --
enabled | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean">Bool</a> | Whether commands can be used in this channel
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the channel

## Command

> Example: Print the Icon of the current command

```javascript
Message.channel.send(this.Icon);
```

The Command Class stores information about a command, so that it can be executed by a user.

Member | Type | Description
-- | -- | --
Author | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the author of the command
Events | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The Events of the command
Icon | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Icon of the command
Languages | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>) | The Languages of the command
Permissions | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The Permissions of the command
Support | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Support link of the command
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the command

### Command.Events

The Events member of the Command Class contains the code for whichever events are used by the command. For example, in a command which uees the Call and Message events, the Events member will have two members: Call, and Message.

<aside class='note'>You do not need to directly access the event code to run an event. Instead you can use the RunEvent function</aside>

### Command.Languages

The Languages member of the Command Class contains the strings used by any languages that the command supports. It is an array of Objects that follow this template:

Member | Type | Description
-- | -- | --
Callname | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Callname of the command
Description | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Description of the command
Language | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The language that this object defines
Name | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Name of the command
Strings | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Translation Strings of the command
Syntax | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Syntax of the command

### Command.Permissions

The Permissions member of the Command Class has these members:

Member | Type | Description
-- | -- | --
Bot | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The permissions the bot must have to run the command
CoreCommand | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | Whether the command is a core command
DevsOnly | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | Whether the command is locked to developers
Editable | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | Whether the command can be edited by others
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | The permissions a user needs to run the command
Viewable | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | Whether the command can be viewed by others

## Emoji

The Emoji class contains information about an emoji, usefull for displaying it on a website as well as in discord.

Member | Type | Description
-- | -- | --
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the emoji
tag | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The tag of the emoji in discord
url | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The url of the emoji on twemoji
utf | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The utf/unicode character of the emoji

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
Icon | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The URL to the icon of the guild
Name | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Name of the guild
Settings | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The Settings of the guild
Stats | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The Stats of the guild
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the guild

### Guild.Settings

The Settings member of the Guild class contains its settings, along with the settings of the commands in it.

Member | Type | Description
-- | -- | --
Admins | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a>) | The IDs of the people in the guild who can manage OpenBot
Channels | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#channelsetting">ChannelSetting</a>) | The Settings for the channels in the guild
Commands | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>) | The Commands that are in the guild
Prefix | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | OpenBot's Prefix in this guild
Searchable | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | Whether this guild can be searched on the website

### Guild.Settings.Commands

The Commands member of the Settings object contains the Commands in the guild, as well as their settings.

Member | Type | Description
-- | -- | --
Channels | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#channelsetting">ChannelSetting</a>) | Command specific settings for the channels in the guild
Data | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | Data that this command stores about the guild
Settings | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The settings for this command.
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the command

### Guild.Stats

The Stats member of the guild object contains some stats about the guild.

Member | Type | Description
-- | -- | --
Messages | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The number of messages OpenBot has processed in this guild
Users | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The number of users in this guild

## Locale

The Locale Class represents a Language that OpenBot supports.

Member | Type | Description
-- | -- | --
code | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Locale Code
icon | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Locale Icon
name | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Language name


## PullRequest

The PullRequest class represents a pull request to someone's command.

Member | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The edited command
Editor | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the person who edited it
Notes | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The notes left by the editor
Owner | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The owner of the command
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the pull request

## Relay

The Relay class represents a relay to another process

Member | Type | Description
-- | -- | --
type | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The type of relay
data | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The data in the relay

### Relay.type

There are several types of relays available:

Name | Data | Description
-- | -- | --
async | Javascript | Evaluates javascript and returns callback
dbUpdate | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | Clears old data from cache
eval | Javascript | Evaluates javascript syncronously
restart | Null | Restarts process
stat | Null | Fetches performance information

<aside class="note">For the async relay, instead of sending "1+1" and getting 2, you send "Callback(1+1)" and get 2. Then you can use asyncrounous functions with .then</aside>


## User

The User Class contains data relating to a user of OpenBot.

Member | Type | Description
-- | -- | --
Avatar | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The link to the user's avatar
Settings | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The user's settings
Stats | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | Some stats about the user
Username | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The user's username
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The user's id

### User.Settings

The Settings member of the User Class contains settings relating to a user.

Member | Type | Description
-- | -- | --
DeveloperMode | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | Whether the user has Developer Mode enabled on the website
Language | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The language the user uses
ShowGuilds | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | Whether the user shows their guilds on their profile

### User.Stats

The Stats member of the User Class contains some stats relating to a user

Member | Type | Description
-- | -- | --
CommandsUsed | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The number of commands the user has used
Messages | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The number of messages the user has sent

## UserData

The UserData Class contains data stored by commands, or about commands, relating to a user. It is kept seperate from the User class so that when a User is requested for a profile or something similar, their data is not exposed.

Member | Type | Description
-- | -- | --
Commands | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>) | Data stored by commands
Private | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | Private storage of the user
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the user

### UserData.Commands

The Commands member of the UserData Class contains an array of all the data stored by various commands relating to that user, sorted by author.

Member | Type | Description
-- | -- | --
Author | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The author of the command storing the data
Data | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The data being stored

### UserData.Private

The Private member of the UserData Class contains all of the Key/Value pairs that a User set on their website. These are used for putting private information in a public command (Like an API key for a music command). It has no defined members, its members are whatever the user defines them to be.

<aside class='note'>You will not need to directly access this object. You can use the LibOpenBot.GetPrivateStorage function to get the members of this object.</aside>


## VerifyRequest

The VerifyRequest Class contains command edits which are waiting for verification by core developers

Member | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The edited command
Editor | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the person who edited it
Message | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the verification message
Notes | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The notes left by the editor
Owner | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the owner of the command
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the verify request

# Functions

## LibOpenBot.Command

The LibOpenBot.Command function creates a new Command in the database

Argument | Type | Description
-- | -- | --
Author | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the author of the command

**Return Type:** <a href="#command">Command</a>

## LibOpenBot.DeleteCommand

The LibOpenBot.DeleteCommand function deletes a Command from the database

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the command to delete

## LibOpenBot.DeletePullRequest

The LibOpenBot.DeletePullRequest function deletes a pull request from the database

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the pull request to delete

## LibOpenBot.DeleteVerifyRequest

The LibOpenBot.DeleteVerifyRequest function deletes a verify request from the database

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the verify request to delete

## LibOpenBot.EmojiToURL

The LibOpenBot.EmojiToURL function returns a url to an image of the discord emoji you pass to it (For example, you would pass ":smile:" or "<:CoolEmoji:12345>")

Argument | Type | Description
-- | -- | --
Tag | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Tag of the emoji

## LibOpenBot.ExecUser

The LibOpenBot.ExecUser allows you to interact with a user who may not be in the same shard as your code is running in.

Argument | Type | Description
-- | -- | --
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the user you want
Exec | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Code to execute

### Exec

The Exec parameter is evaluated as javascript, with the global variable User as the user you requestsed. If the user is not found, the code will not be executed.

## LibOpenBot.GetCommand

The LibOpenBot.GetCommand function returns a Command from its ID

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the command to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="#command">Command</a>)

## LibOpenBot.GetCommandData

The LibOpenBot.GetCommandData function returns the data a command has stored about a User. (You can get Guild data directly from the BotContext.Guild Object)

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The Command whose data you want to get
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the user whose data you want to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>)

<aside class="warning">You must pass "this" as the Command argument. If you attempt to view/edit data owned by other commands, your command will be denied</aside>

## LibOpenBot.GetCommands

The LibOpenBot.GetCommands function returns an array of Commands from an array of IDs.

Argument | Type | Description
-- | -- | --
IDs | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a>) | The IDs of the commands to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#command">Command</a>))

## LibOpenBot.GetDevs

The LibOpenBot.GetDevs function returns the IDs of all of the Users with Developer Permissions

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a>))

## LibOpenBot.GetEmojis

The LibOpenBot.GetEmojis function returns all of the Emojis indexed by OpenBot

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#emoji">Emoji</a>))

## LibOpenBot.GetLocales

The LibOpenBot.GetLocales function returns all of the Locales supported by OpenBot

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#locale">Locale</a>))

## LibOpenBot.GetPrivateStorage

The LibOpenBot.GetPrivateStorage function returns all or some of your private storage.

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the User whose private storage you want to get.
Key | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Key of the private storage you want to get

### Key

If Key is null, then it will return all of the private storage. If key is a string, it will return the private storage entry that has that Key as its Name.

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>/<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a>)

<aside class="warning">If you attempt to get the private storage of another user other than yourself, your command will be denied.</aside>

## LibOpenBot.GetPullRequest

The LibOpenBot.GetPullRequest function returns a Pull Request from its ID

Argument | Tyoe | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the Pull Request to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="#pullrequest">PullRequest</a>)

## LibOpenBot.GetPullRequests

The LibOpenBot.GetPullRequests function gets all of the Pull Requests to a certain User's Commands.

Argument | Type | Description
-- | -- | --
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the User whose Pull Requests you want

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#pullrequest">PullRequest</a>))

## LibOpenBot.GetUser

The LibOpenBot.GetUser function returns a User from an ID

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the User to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="#user">User</a>)

## LibOpenBot.GetUserCommands

The LibOpenBot.GetUserCommands function returns all of the Commands that a User has made

Argument | Type | Description
-- | -- | --
UserID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the User whose Commands you want to get

**Return Type:** Promise(Array(Command))

## LibOpenBot.GetUserData

The LibOpenBot.GetUserData function returns the User Data of a user (Including Private Storage and Command Data).

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the User whose data you want to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#command">Command</a>))

<aside class="note">You do not need to directly interact with this function, instead you can use LibOpenBot.GetPrivateStorage or LibOpenBot.GetCommandData to get the individual parts of a User's data</aside>

## LibOpenBot.GetVerifiers

The LibOpenBot.GetVerifiers function returns the IDs of all of the Users who have Verifier Permissions

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#number">Number</a>))

## LibOpenBot.GetVerifyRequests

The LibOpenBot.GetVerifyRequests function returns all of the Verification requests in the queue.

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#verifyrequest">VerifyRequest</a>))

## LibOpenBot.GetWebLocales

The LibOpenBot.GetWebLocales function returns all of the locale codes supported on OpenBot's Website

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a>))

## LibOpenBot.Guild

The LibOpenBot.Guild function creates a new guild in the database

Argument | Type | Description
-- | -- | --
DiscordGuild | <a href="https://discord.js.org/#/docs/main/stable/class/Guild">guild</a> | A discord.js guild

**Return Type:** <a href="#guild">Guild</a>

## LibOpenBot.HasPermissions

The LibOpenBot.HasPermissions function compares two permissions bitfields to see whether they include eachother. It returns true if the user/entity has the permissions that it needs.

Argument | Type | Description
-- | -- | --
Has | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The Permissions that the user/entity has
Needs | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The Permissions that the user/entity needs

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean">Bool</a>

## LibOpenBot.LanguageIndex

The LibOpenBot.LanguageIndex function returns the index in which a language is found in a command.

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The command to search
Language | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The language to find

**Return type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a>

## LibOpenBot.PullRequest

The LibOpenBot.PullRequest function creates a new pull request to a command

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The Edited Command
Editor | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the editor of the command
Notes | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The notes about the edit

**Return Type:** <a href="#pullrequest">PullRequest</a>

## LibOpenBot.RegSearch

The LibOpenBot.RegSearch function turns a search query into a valid reqular expression. This would be used when using String.match in the ReQL language (Used in LibOpenBot.Search functions), to search for part of a string instead of a whole string (.eq) or regular expression (.match without using LibOpenBot.RegSearch).

Argument | Type | Description
-- | -- | --
Query | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Query to search for

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a>

## LibOpenBot.SearchCommands

The LibOpenBot.SearchCommands function searches in the database for commands that match the search.

Argument | Type | Description
-- | -- | --
Search | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">Function</a> | The Search Criteria.

### Search

OpenBot supports using an Object `{Icon:":DopeIcon:"}` or an Anonymous Function `(Command)=>Command('Icon').eq(':DopeIcon:')`. You can learn how these parameters work <a href="https://rethinkdb.com/api/javascript/filter">here.</a>

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#command">Command</a>))

<aside class="note">The Anonymous Function looks like javascript, but it is actually written in ReQL. If you try to use Javascript comparitors it will not work.</aside>

## LibOpenBot.SearchGuilds

The LibOpenBot.SearchGuilds function searches in the database for guilds that match the search.

Argument | Type | Description
-- | -- | --
Search | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">Function</a> | The Search Criteria

### Search

OpenBot supports using an Object `{Icon:":DopeIcon:"}` or an Anonymous Function `(Command)=>Command('Icon').eq(':DopeIcon:')`. You can learn how these parameters work <a href="https://rethinkdb.com/api/javascript/filter">here.</a>

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#guild">Guild</a>))

<aside class="note">The Anonymous Function looks like javascript, but it is actually written in ReQL. If you try to use Javascript comparitors it will not work.</aside>

## LibOpenBot.SearchUsers

The LibOpenBot.SearchUsers function searches in the dtabase for users that match the search.

Argument | Type | Description
-- | -- | --
Search | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">Function</a> | The Search Criteria

### Search

OpenBot supports using an Object `{Icon:":DopeIcon:"}` or an Anonymous Function `(Command)=>Command('Icon').eq(':DopeIcon:')`. You can learn how these parameters work <a href="https://rethinkdb.com/api/javascript/filter">here.</a>

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise"></a>Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#user">User</a>))

<aside class="note">The Anonymous Function looks like javascript, but it is actually written in ReQL. If you try to use Javascript comparitors it will not work.</aside>

## LibOpenBot.User

The LibOpenBot.User function creates a new user in the database.

Argument | Type | Description
-- | -- | --
DiscordUser | <a href="https://discord.js.org/#/docs/main/stable/class/User">user</a> | A discord.js user

**Return Type:** <a href="#user">User</a>

## LibOpenBot.UserData

The LibOpenBot.UserData function creates a new UserData entry in the database

Argument | Type | Description
-- | -- | --
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the user whose data this is

**Return Type:** <a href="#userdata">UserData</a>

## LibOpenBot.VerifyRequest

The LibOpenBot.VerifyRequest function creates a new verification request to a command

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The Edited Command
Editor | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the editor of the command
Notes | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The notes about the edit
Message | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the verification message

**Return Type:** <a href="#verifyrequest">VerifyRequest</a>

## LibOpenBot.WriteCommand

The LibOpenBot.WriteCommand function writes a command to the database, saving any changes that may have been made.

Argument | Type | Descrpition
-- | -- | --
Command | <a href="#command">Command</a> | The Command to save

## LibOpenBot.WriteCommandData

The LibOpenBot.WriteCommandData function writes a CommandData object to the database

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The Command that the data belongs to
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the user that the data is about
Data | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The Data to write

<aside class="note">This will overwrite the previous value, not just modify it. Also, CommandData is stored by Author, not Command, so all of your commands share the same entry.</aside>

## LibOpenBot.WriteGuild

The LibOpenBot.WriteGuild function writes a guild to the database, saving any changes that may have been made.

Argument | Type | Description
-- | -- | --
Guild | <a href="#guild">Guild</a> | The Guild to save

## LibOpenBot.WritePrivateStorage

The LibOpenBot.WritePrivateStorage function writes a PrivateStorage object to the database, saving any changes that may have been made.

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The User ID that the storage belongs to
Value | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The value of the private storage

<aside class="note">This will overwrite the entire private storage, not just update one key.</aside>

## LibOpenBot.WritePullRequest

The LibOpenBot.WritePullRequest function writes a pull request to the database, saving any changes that may have been made.

Argument | Type | Description
-- | -- | --
PullRequest | <a href="#pullrequest">PullRequest</a> | The Pull Request to save

## LibOpenBot.WriteUser

The LibOpenBot.WriteUser function writes a user to the database, saving any changes that may have been made.

Argument | Type | Description
-- | -- | --
User | <a href="#user">User</a> | The User to save

## LibOpenBot.WriteUserData

The LibOpenBot.WriteUserData function writes a UserData object to the database, saving any changes that may have been made

Argument | Type | Description
-- | -- | --
UserData | <a href="#userdata">UserData</a> | The UserData to save

<aside class="note">You most likely will not need to use this function directly, instead you can use LibOpenBot.WritePrivateStorage or LibOpenBot.WriteCommandData to write the individual parts of a UserData Object</aside>

## LibOpenBot.WriteVerifyRequest

The LibOpenBot.WriteVerifyRequest function writes a verify request to the database, saving any changes that may have been made.

Argument | Type | Description
-- | -- | --
VerifyRequest | <a href="#verifyrequest">VerifyRequest</a> | The Verify Request to save

## LibOpenBot.sendRelay

The LibOpenBot.sendRelay function sends a message to another process, and retrieves the result.

Argument | Type | Description
-- | -- | --
Proc | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Name of the process to send a relay to
Data | <a href="#relay">Relay</a> | The Relay to send

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>)

## LibOpenBot.sendRelayShards

The LibOpenBot.sendRelayShards function sends a message to all of the shards and retrieves the result.

Argument | Type | Description
-- | -- | --
Data | <a href="#relay">Relay</a> | The Relay to send

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>))

## LibOpenBot.sendRelayAll

The LibOpenBot.sendRelayAll function sends a message to all of the processes and retrieves the result

Argument | Type | Description
-- | -- | --
Data | <a href="#relay">Relay</a> | The Relay to send
Master | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | Whether to send it to the master process

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>))

## RunEvent

The RunEvent function runs an event of a command.

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The Command to run
Event | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Event to run
Context | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The Context object to pass the event
BotContext | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The BotContext object to pass the event
Arg1 | Anything | The First argument to pass to the event
Arg2 | Anything | The Second argument to pass to the event

<aside class="note">The RunEvent function is only available inside of a shard. All Commands are run inside of a shard, so that will not be a problem unless you are using relays.</aside>

# Globals

There are some global variables that commands can access in order to do things.

## ObjDiscordClient

ObjDiscordClient is the discord.js client.

**Type:** <a href="https://discord.js.org/#/docs/main/stable/class/Client">Client</a>

# Libraries

OpenBot provides access to multiple libraries that you can use in your command. If you need a library that is not on this list, you can contact the developers at the OpenBot Support discord server and they will consider adding it.

You do not need to use the require function in order to include libraries. All libraries are included when OpenBot loads, and are available through the constants below.

## LibDiscord

LibDiscord references a fork of the `discord.js` npm package. (The changes in the fork are not relavant to commands, they are for sharding purposes)

## LibOpenBot

LibOpenBot references the OpenBot API. Its documentation is found right here.
