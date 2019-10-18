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
**Children:**  guild, channel*, user*
 
 *May be null
 
 ### BotContext
 
 **Type:** Object
 **Description:** The BotContext contains OpenBot objects relevent to the event
 **Children:** Guild, User*
 
 *May be null

## Call 

The Call event is executed whenever a message matches Prefix+Callname. For example, when someone sends "-Open Help" on a server where the prefix is "-Open", the command with the callname "Help" runs its Call event.

It receives these variables:

### Message

**Type:** Message
**Description:** The message that was sent to activate the command.

### Arguments

**Type:** String
**Description:** The content of the message, excluding the prefix and callname. For example, if message.content is `-Open Add SomeCommand`, Arguments will be "SomeCommand"

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
