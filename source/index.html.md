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

Your command's icon is displayed next to it in help menus, searches and more. It should relate to your command so that people can tell what it does at a glance. The icon can be any discord emoji. If it is a default emoji, it must be entered into the editor like `:smile:`. If it is a custom emoji, it must be entered in like `<:AddCommand:634475978000695316>` To find the ID of a custom emoji, right click it in discord and click *copy link*. The number in the link is the ID of your emoji. (If you are using discord in your browser, you will click *copy image address* instead of *copy link*)

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

### Private

If your command is marked as private, nobody will be able to add it to a server or see it in search results except for you.

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

**(Note)** - Note (ie you can use `(No Arguments)` to indicate that your command doesnt expect any parameters

### Translation Strings

> Example: How to use translation strings

```javascript
//Send String 0
Message.channel.send(this.Languages[LibOpenBot.LanguageIndex(this,BotContext.User.Settings.Language].Strings[0]);

//Make a reference to the strings for cleaner code
var Strings=this.Languages[LibOpenBot.LanguageIndex(this,BotContext.User.Settings.Language].Strings;
//Later...
Message.channel.send(Strings[0]);
```
Translation strings allow the text inside your command to be translated. You can have as many as you want, and you can access them from your code.

## Event Box

Your command can have multiple events, or just one. These are where you put your code. You can find a description of what the different events do below.

To add an event, click the green "Add" button. You can add all the default events once, and as many custom events as you need.

To edit the parameters of a custom event, click the + to add, - to remove, and use the textfields to edit parameters. You cannot have duplicate or empty parameters.

To delete an event, click the "x" next to its name

<aside type="note">If you are having difficulties scrolling sideways through the tabs, you can hold shift and scoll up/down and it will scroll sideways</aside>

## Settings Box

Your command can have custom settings which guild admins will edit on the dashboard. When your command accesses its settings, they will be represented by an object.

> Example: Access the settings for your command

```javascript
//Create a variable with the command's settings
var Settings=await LibOpenBot.GetCommandSettings(this,BotContext.Guild);
//Print the setting
Message.chanenl.send('My setting is set to '+Settings.ExampleText);
```

### Fields

Fields are the meat of settings. There are several different types of fields, which can store different types of data and can be selected in different ways. All settings have a Name and Default value.

**Name:**  The name to access the field by, and the name displayed in the guild dashboard

**Type:** The type of data stored in the field. Can be Bool, Text, or Set

**Default:** The value that is set when the bot joins a server, or when this setting is added

<aside class="note">A fields name cannot be "type", or "limit". These names are reserved for internal OpenBot usage. Also, settings are case sensitive, so you can use "Type" and "Limit" if you want</aside>

### Field Types

There are several different field types that can be used, each can hold a different type of data.

**Bool:**

The bool type holds a boolean value (true or false). On the guild dashboard, it is chosen using a toggle switch.

**Category:**

The category type is a container for other fields. It allows you to organize your data for easy access.

**List:**

A list is like an array. You define a template for the objects that go inside the list, and users can add as many as they want (up to the limit you set). It is accessed like an array (ie: Settings.MyList[0].SomeProperty accesses the first element in MyList)

**Text:**

The text type holds a string. On the guild dashboard, it is chosen using a text field. It has a special option called RegEx. The RegEx option allows you to set a regular expression which the user's input must match up with.

**Set:**

The set type holds any javascript data type. On the guild dashboard, it is chosen using a dropdown list. It has a special option called Set. The Set option allows you to specify the fields in the dropdown menu. The Set option must be javascripit. It is evaluated on the Bot, with a global variable "Guild" representing the guild that the setting is in. Here are some example Sets.

`[0,1,2]` - Choose 0, 1, or 2,

`[{name:'Zero',value:0},{name:'One',value:1},{name:'Two',value:2}]` - Choose 0, 1, or 2. They are displayed on the dropdown as "Zero" "One" and "Two".

`Guild.channels.cache.array().filter(c=>c.type=='text').map(c=>{return {name:c.name,value:c.id}})` - Choose from the channels in the current guild.

# Events

> Example: Log to the console

```javascript
console.log('This event was called!');
```

Events are among the most important things in OpenBot. They define the actions that the bot takes. Every event is actually a function which gets passed several variables and has scope to an OpenBot shard. You don't need to write the function, you can treat the code block as if it is directly executed. Ie this code would log to the console every time it was executed.


## Universal

All events receive certain variables, regardless of their type. Here they are:

> Example: Print some information about where the command was called

```javascript
Message.channel.send('Current Guild: '+Context.guild.name);
if(Context.channel) Message.channel.send('Current Channel: '+Context.channel.name);
if(Context.user) Message.channel.send('Requested by: '+Context.user.username);
```

### Context

**Type:** Object

**Description:** The context contains discord.js objects relevent to the event.

**Children:**  <a href="https://discord.js.org/#/docs/main/stable/class/Guild">guild</a>, <a href="https://discord.js.org/#/docs/main/stable/class/Channel">channel</a>\*, <a href="https://discord.js.org/#/docs/main/stable/class/User">user</a>\*
 
 \*May be null
 
 > Example: Print some statistics about where the command was called
 
 ```javascript
 Message.channel.send('Messages sent in guild: '+BotContext.Guild.Stats.Messages);
 if(BotContext.User) Message.channel.send('Messages sent by user: '+BotContext.User.Stats.Messages);
 ```
 
### BotContext
 
 **Type:** Object
 
 **Description:** The BotContext contains OpenBot objects relevent to the event
 
 **Children:** <a href="#guild">Guild</a>, <a href="#user">User</a>\*
 
\*May be null

> Example: Print whether the current command is open source

```javascript
Message.channel.send(this.Permissions.Viewable);
```

### this

**Type:** <a href="#command">Command</a>

**Description:** When in an event, `this` refers to the command whose event is being executed

## Call 

> Example: A simple Say Command which says whatever the user requests.

```javascript
Message.channel.send(Arguments);
```

The Call event is executed whenever a message matches Prefix+Callname. For example, when someone sends "-Open Help" on a server where the prefix is "-Open ", the command with the callname "Help" runs its Call event.

It receives these variables:

### Message

**Type:** <a href="https://discord.js.org/#/docs/main/stable/class/Message">Message</a>

**Description:** The message that was sent to activate the command.

### Arguments

**Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a>

**Description:** The content of the message, excluding the prefix and callname. For example, if message.content is "-Open Add SomeCommand", Arguments will be "SomeCommand"

## ChannelCreate

> Example: Be the first message in a channel!

```javascript
Context.channel.send('First!');
```

The ChannelCreate event is executed when a channel is created.

It receives no special variables.

## ChannelDelete

> Example:  Be a bad bot and recreate a channel when it's deleted

```javascript
Context.guild.channels.create(Context.channel.name);
```

The ChannelDelete event is executed when a channel is deleted.

It receives no special variables.

## ChannelPinsUpdate

> Example: Send a message when someone pins or unpins a message.

```javascript
Context.channel.send('Someone is messing with the pins here...');
```

The ChannelPinsUpdate event is executed when the pins of a channel are changed.

It receives no special variables.

## ChannelUpdate

> Example: Send a message when a channel's name is changed

```javascript
if(OldChannel.name!=NewChannel.name)
    NewChannel.send('This channel's name has been changed from '+OldChannel.name+' to '+NewChannel.name);
```

The ChannelUpdate event is executed when a channel is updated (eg. Name changed, Permissions changed, etc.)

It receives these variables:

### OldChannel

**Type:** <a href="https://discord.js.org/#/docs/main/stable/class/Channel">Channel</a>

**Description:** The channel before the update

### NewChannel

**Type:** <a href="https://discord.js.org/#/docs/main/stable/class/Channel">Channel</a>

**Description:** The channel after the update

## CommandAdded

> Example: Send a dm to the person who added the command thanking them. (And probably making them remove the command)

```javascript
Context.user.send('Thank you for adding '+this.Languages[LibOpenBot.LanguageIndex(this,BotContext.User.Settings.Language)].Name)+' to your server');
```

The CommandAdded event is executed when your command is added to a server.

It recieves no special variables.

## CommandRemoved

> Example: Send a dm to the person who removed your command. (Like any good windows freeware when you uninstall it)

```javascript
Context.user.send('We are sorry to see you stop using '+this.Languages[LibOpenBot.LanguageIndex(this,BotContext.User.Settings.Language)].Name);
```

The CommandRemoved event is executed when your command is removed from a server.

It receives no special variables.

## CommandUpdated

> Example: dm yourself when your command is approved (Because the default notification isnt enough?)

```javascript
//Note: this will dm once per guild your command is in, which is spam and API abuse. Don't do this, your command will not be accepted.
LibOpenBot.ExecUser(this.Author,'User.send("Your command been approved! Good job!")');
```

The CommandUpdated event is executed when your edit request is approved, and your command is integrated into OpenBot. You can use it to update command data if you change formats, or anything else that needs updated. It is run once per guild that your command is in.

## EmojiCreate

> Example: Send the new emoji in a random channel in the guild

```javascript
//Note: sending a message unprovoked in a random channel isnt a good idea. Don't do this. In fact, don't do any of these examples, they are just to show how the events work.
var Channels=Context.guild.channels.cache.array().filter(c=>c.type=='text');
Channels[parseInt(Math.random()*Channels.length)].send('I like this new emoji <:'+Emoji.name+':'+Emoji.id+>');
```

The EmojiCreate event is executed when an emoji is added to the guild.

It receives these variables:

### Emoji

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Emoji">Emoji</a>

**Description:** The emoji that was added.

## EmojiDelete

> Example: Be salty about an emoji being removed from a guild

```javascript
//Note: also don't do this...
var Channels=Context.guild.channels.cache.array().filter(c=>c.type=='text');
Channels[parseInt(Math.random()*Channels.length)].send('YALL REMOVED '+Emoji.name+'! I DEMAND JUSTICE FOR EMOJIS!');
```

The EmojiDelete event is executed when an emoji is deleted from the guild.

It receives these variables:

### Emoji

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Emoji">Emoji</a>

**Description:** The emoji that was deleted

## EmojiUpdate

> Example: Change your command's icon to a frankenstein combination of the edited emoji (Don't do this please)

```javascript
//I'm running out of ideas for these examples, ok?
this.Icon='<:'+OldEmoji.name+':'+NewEmoji.id+'>';
```

The EmojiUpdate event is executed when an emoji in the guild is updated (eg. Name changed, Icon changed, etc.)

It receives these variables:

### OldEmoji

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Emoji">Emoji</a>

**Description:** The emoji before the update

### NewEmoji

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Emoji">Emoji</a>

**Description:** The emoji after the update

## GuildBanAdd

> Example: Attempt to dm the banned user letting them know that they were banned (Don't do this)

```javascript
Context.user.send('You have been banned from '+Context.guild.name);
```

The GuildBanAdd event is executed when a user is banned from the guild.

It receives no special variables.

## GuildBanRemove

> Example: Attempt to dm the unbanned user letting them know that they were unbanned (Don't do this)

```javascript
Context.user.send('You have been unbanned from '+Context.guild.name);
```

The GuildBanRemove event is executed when a user is unbanned from the guild.

It receives no special variables.

## GuildIntegrationsUpdate

> Example: I don't even know... This only exists here because OpenBot supports every discord.js event.

```javascript
console.log('Somebody did a thing');
```

The GuildIntegrationsUpdate event is executed when a guild's integrations are updated.

It receives no special variables.

## GuildMemberAdd

> Example: Greet a user when they join

```javascript
Member.user.send('Welcome to '+Context.guild.name);
```

The GuildMemberAdd event is executed when a user joins a guild.

It receives these variables:

### Member

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/GuildMember">Member</a>

**Description:** The member that joined

## GuildMemberRemove

> Example: Attempt to dm a user when they leave (Don't do this, its not ok)

```javascript
Member.user.send('Sorry that you left '+Context.guild.name+'. We hope you enjoyed your time here.');
```

The GuildMemberRemove event is executed when a user leaves or is kicked from a guild.

It receives these variables:

### Member

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/GuildMember">Member</a>

**Description:** The member that left

## GuildMemberSpeaking

> Example: Attempt to join the voice channel that they user is in when they start speaking

```javascript
if(Speaking) Member.voice.channel.join();
```

The GuildMemberSpeaking event is executed when a user starts/stops speaking.

It receives these variables:

### Member

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/GuildMember">Member</a>

**Description:** The member that started/stopped speaking

### Speaking

**Type:** Boolean

**Description:** Whether they are speaking.

## GuildMemberUpdate

> Example: Pretend to forget who a user is and dm them asking. (Please don't do this, these examples are worng on many levels)

```javascript
if(OldMember.displayName!=NewMember.displayName)
    NewMember.user.send('I can't recognize u with ur new nickname... U used to be '+OldMember.displayName+' but now ur '+NewMember.displayName);
```

The GuildMemberUpdate event is executed when a member is updated (eg. Nickname changed, Roles changed, etc.)

It receives these variables:

### OldMember

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/GuildMember">Member</a>

**Description:** The member before the update

### NewMember

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/GuildMember">Member</a>

**Description:** The member after the update

## GuildUpdate

> Example: If there is a channel named #logs, log to it when the guild name is changed

```javascript
var Channel=Context.guild.channels.cache.array().filter(c=>c.name=='logs'&&c.type=='text')[0];
if(Channel&&OldGuild.name!=NewGuild.name)
    Channel.send('This guild has been renamed from '+OldGuild.name+' to '+NewGuild.name);
```

The GuildUpdate event is executed when a guild is updated (eg. Name changed, region changed, etc.)

It receives these variables:

### OldGuild 

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Guild">Guild</a>

**Description:** The guild before the update

### NewGuild

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Guild">Guild</a>

**Description:** The guild after the update

## Message

> Example: Be a classic first bot and say "pong" when anyone says "ping"

```javascript
if(Message.content=='ping')
    Message.channel.send('pong!');
```

The Message event is executed whenever a message is sent, regardless of whether a command has been called.

It receives these variables:

### Message

**Type:** <a href="https://discord.js.org/#/docs/main/stable/class/Message">Message</a>

**Description:** The message that was sent

## MessageDelete

> Example: Snipe that deleted message like an annoying bot

```javascript
Message.channel.send('Someone deleted '+Message.author.username+'\'s message which said "'+Message.content+'"');
```

The MessageDelete event is executed when a message is deleted.

It receives these variables:

### Message

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Message">Message</a>

**Description:** The message that was deleted

## MessageReactionAdd

> Example: Ask if you are being summoned any time someone reacts with your command's icon

```javascript
//Note: please don't do this
var IconReaction=await LibOpenBot.EmojiToReaction(this.Icon);
if(Reaction.emoji.name==IconReaction||Reaction.emoji.id==IconReaction)
    Reaction.message.channel.send('Whoms\'t has summoned the ancient one?!?!?!?');
```

The MessageReactionAdd event is executed when a reaction is added to a message.

It receives these variables:

### Reaction

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/MessageReaction">MessageReaction</a>

**Description:** The reaction that was added

## MessageReactionRemove

> Example: Return to your slumber when someone removes a reaction which was your command's icon.

```javascript
//Note: please don't do this
if(Reaction.emoji.name==await LibOpenBot.EmojiToReaction(this.Icon))
    Reaction.message.channel.send('And so i return to my slumber...');
```

The MessageReactionRemove event is executed when a reaction is removed from a message

It receives these variables:

### Reaction

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/MessageReaction">MessageReaction</a>

**Description:** The reaction that was removed

## MessageReactionRemoveAll

> Example: Delete a message if someone removes every reaction from it at once

```javascript
//What am i even doing with these examples anymore...
Message.delete();
```


The MessageReactionRemoveAll event is executed when all the reactions are removed from a message

It receives these variables:

### Message

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Message">Message</a>

**Description:** The message from which the reactions were removed

## MessageUpdate

> Example: Thanks people for editing their message instead of making 5 messages with spelling corrections

```javascript
//Once again, don't do this
NewMessage.author.send('Thank you for editing your message instead of being *that guy* who makes 5 new messages to correct their spelling');
```

The MessageUpdate event is executed when a message is edited

It receives these variables:

### OldMessage

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Message">Message</a>

**Description:** The message before the edit

### NewMessage

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Message">Message</a>

**Description:** The message after the edit

## RoleCreate

> Example: Be a boss and give the bot a new role when it is created

```javascript
//Why do i do this...
(await Context.guild.members.fetch(ObjDiscordClient.user.id)).roles.add(Role.id);
```

The RoleCreate event is executed when a role is created

It receives these variables:

### Role

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Role">Role</a>

**Description:** The role that was created

## RoleDelete

> Example: Be **that bot** that logs everything in DBL

```javascript
var Channel=Context.guild.channels.cache.array().filter(c=>c.type=='text'&&c.name=='testing-1')[0];
if(Channel)
    Channel.send('The role '+Role.name+' has been deleted');
```

The RoleDelete event is executed when a role is deleted

It receives these variables:

### Role

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Role">Role</a>

**Description:** The role that was deleted

## RoleUpdate

> Example: Do absolutely nothing when a role's name is changed

```javascript
if(OldRole.name!=NewRole.name) {
    //Hah you thought there would be an action in every example!
}
```

The RoleUpdate event is executed when a role is updated (eg. Change name, Change permissions, etc.)

It receives these variables:

### OldRole

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Role">Role</a>

**Description:** The role before the update

### NewRole

**Type:** <a href="https://dicsord.js.org/#/docs/main/stable/class/Role">Role</a>

**Description:** The role after the update

## VoiceStateUpdate

> Example: Stalk bob in the vc.

```javascript
if(NewMember.displayName.toUpperCase()=='BOB') 
    if(NewMember.voice.channel)
        NewMember.voice.channel.join();
```

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

> Example: Print the global setting for the current channel

```javascript
Message.channel.send('The current channel is '+(BotContext.Guild.Settings.Channels.filter(c=>c.id==Context.channel.id&&c.enabled==false).length?'disabled':'enabled')+' by default.');
```

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
Private | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | Whether the command is private
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | The permissions a user needs to run the command
Viewable | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | Whether the command can be viewed by others

## Emoji

> Example: Print the discord emoji version of a utf character

```javascript
var Emoji=(await LibOpenBot.GetEmojis()).filter(e=>e.utf==Arguments)[0];
if(Emoji)
    Message.channel.send(':'+Emoji.tag+':');
```

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

> Example: Print the number of messages OpenBot has seen in this guild

```javascript
Message.channel.send(BotContext.Guild.Stats.Messages);
```

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
Owner | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The Discord UserID of the owner of this guild (Equivilant to guild.owner in discord.js)
Users | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The number of users in this guild

## Locale

> Example: Print the icon for a language code

```javascript
var Locale=await LibOpenBot.GetLocales()).filter(l=>l.code==Arguments)[0];
if(Locale) Message.channel.send(Locale.icon);
else Message.channel.send('There is no language with that code');
```

The Locale Class represents a Language that OpenBot supports.

Member | Type | Description
-- | -- | --
code | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Locale Code
icon | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Locale Icon
name | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Language name

## PatreonData

> Example: Do nothing since you don't need to use this class

```javascript
//Insert cool code here
```

The PatreonData class represents a patreon of OpenBot

Member | Type | Description
-- | -- | --
access | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The access token of the patreon
expires | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The timestamp at which the token expires
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The discord id of the user
refresh | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The refresh token of the patreon
tier | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The tier of a patreon

<aside class="warning">You are not allowed to send or store the access or refresh token of a patreon in any way! You can only use them for fetching information from Patreon's API</aside>

## PullRequest

> Example: Print how many incoming pull requests you have

```javascript
Message.channel.send((await LibOpenBot.GetPullRequests(Context.user.id)).length);
```

The PullRequest class represents a pull request to someone's command.

Member | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The edited command
Editor | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the person who edited it
Notes | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The notes left by the editor
Owner | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The owner of the command
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the pull request

## Relay

> Example: Perform some math on the express server using a relay

```javascript
Message.channel.send('1+1 is '+await LibOpenBot.sendRelay('Express Server',{type:'eval',data:'1+1'}));
```

The Relay class represents a relay to another process

Member | Type | Description
-- | -- | --
type | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The type of relay
data | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The data in the relay

### Relay.type

There are several types of relays available:

Name | Data | Description
-- | -- | --
api | Javascript Evaluates javascript asyncrounously with scope for OpenBot API
async | Javascript | Evaluates javascript and returns callback
dbUpdate | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | Clears old data from cache
eval | Javascript | Evaluates javascript syncronously
restart | Null | Restarts process
stat | Null | Fetches performance information

<aside class="note">For the async relay, instead of sending "1+1" and getting 2, you send "Callback(1+1)" and get 2. Then you can use asyncrounous functions with .then</aside>
<aside class="note">For the api relay, instead of seinding "1+1" and getting 2, you send "return 1+1" and get 2. Then you can use async/await to perform asyncrounous requests</aside>

## Timeout

> Example: Create a timeout and print its id

```javascript
var Timeout=new LibOpenBot.Timeout(1000,()=>{(await LibOpenBot.users.fetch(Argument.user)).send('Hello sir')},{user:Context.user.id});
Message.channel.send('Your greeting has been created and has the id '+Timeout.id);
```

The Timeout class stores timeouts for commands and other services, so that they can be called even if the bot restarts.

Member | Type | Description
-- | -- | --
Argument | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | Argument to pass to the timeout upon running it (JSON Object)
Code | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | Code to run (In the form of a function body)
Proc | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The name of the process which requested the timeout
Time | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The time to run the timeout at
id | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the timeout

## User

> Example: Print the user's preferred language

```javascript
Message.channel.send('Your language code is '+BotContext.User.Settings.Language);
```

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

> Example: Dm a user their private storage (Why though?)

```javascript
Context.user.send(JSON.stringify((await LibOpenBot.GetUserData(Context.user.id)).Private);
```


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

> Example: Tell a user how many commands they have in the verification queue

```javascript
Message.channel.send((await LibOpenBot.GetVerifyRequests()).filter(v=>v.Owner==Context.user.id).length)
```

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

> Example: Create a new command for a user

```javascript
//Don't do this, use the website instead
var NewCommand=LibOpenBot.Command(Context.user.id);
```

The LibOpenBot.Command function creates a new Command in the database

Argument | Type | Description
-- | -- | --
Author | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the author of the command

**Return Type:** <a href="#command">Command</a>

## LibOpenBot.DeleteCommand

> Example: Delete the command being called

```javascript
//Uh.... i guess if you really want to?
LibOpenBot.DeleteCommand(this.id);
```

The LibOpenBot.DeleteCommand function deletes a Command from the database

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the command to delete

## LibOpenBot.DeletePullRequest

> Example: Delete all of the pull requests on your commands

```javascript
//Again, don't do this
for(var Request of await LibOpenBot.GetPullRequests(Context.user.id))
    LibOpenBot.DeletePullRequest(Request.id);
```

The LibOpenBot.DeletePullRequest function deletes a pull request from the database

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the pull request to delete

## LibOpenBot.DeleteTimeout

> Example: Start a timeout and then cancel it

```javascript
var Timeout=LibOpenBot.Timeout(1000,()=>{/*Do something*/},null);
//Several bad life choices later
LibOpenBot.DeleteTimeout(Timeout.id);
```

The LibOpenBot.DeleteTimeout function deletes a timeout from the database

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the timeout to delete

## LibOpenBot.DeleteVerifyRequest

> Example: Delete every verify request in existance

```javascript
//100% don't do this
for(var Request of await LibOpenBot.GetVerifyRequests())
    LibOpenBot.DeleteVerifyRequest(Request.id);
```

The LibOpenBot.DeleteVerifyRequest function deletes a verify request from the database

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the verify request to delete

## LibOpenBot.EmojiToReaction

> Example: React with a certain emoji without dealing with unicode

```javascript
Message.react(await LibOpenBot.EmojiToReaction(':white_check_mark:'));
```

The LibOpenBot.EmojiToReaction function returns the unicode of built in emojis, and the id of custom emojis. This is useful for reacting to messages, and determining what emoji a reaction is using.

Argument | Type | Description
-- | -- | --
Tag | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Tag of the emoji

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a>

## LibOpenBot.EmojiToURL

> Example: Print your command's icon as an image

```javascript
Message.channel.send(await LibOpenBot.EmojiToURL(this.Icon));
```

The LibOpenBot.EmojiToURL function returns a url to an image of the discord emoji you pass to it (For example, you would pass ":smile:" or "<:CoolEmoji:12345>")

Argument | Type | Description
-- | -- | --
Tag | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Tag of the emoji

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a>

## LibOpenBot.ExecUser

> Example: DM yourself when an error happens

```javascript
try {
    Message.channel.send(TyP0.Lol);
} catch(Error) {
    LibOpenBot.ExecUser(Command.Author,'User.send(`'+Error+'`);');
}
```

The LibOpenBot.ExecUser function allows you to interact with a user who may not be in the same shard as your code is running in.

Argument | Type | Description
-- | -- | --
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the user you want
Exec | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Code to execute

### Exec

The Exec parameter is evaluated as javascript, with the global variable User as the user you requestsed. If the user is not found, the code will not be executed.

**Return Type:** Whatever your javascript returns

## LibOpenBot.ExecGuild

> Example: Print the name of a guild by id

```javascript
Message.channel.send(await LibOpenBot.ExecGuild(Arguments,'Guild.name'));
```

The LibOpenBot.ExecGuild function allows you to interact with a guild which may not be in the same shard as your code is running in.

Argument | Type | Description
-- | -- | --
Guild | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the guild you want
Exec | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Code to execute

### Exec

The Exec parameter is evaluated as javascript, with the global variable Guild as the user you requestsed. If the guild is not found, the code will not be executed.

**Return Type:** Whatever your javascript returns

## LibOpenBot.GetCommand

> Example: List the events that a command has

```javascript
var Command=await LibOpenBot.GetCommand(Arguments);
if(Command) {
    Message.channel.send(Object.keys(Command.Events).join(', '));
}
```

The LibOpenBot.GetCommand function returns a Command from its ID

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the command to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="#command">Command</a>)

## LibOpenBot.GetCommandData

> Example: Store the arguments that a user used to call the command

```javascript
var Data=await LibOpenBot.GetCommandData(this,Context.user.id);
Data.Arguments=Arguments;
LibOpenBot.WriteCommandData(Data);
```

The LibOpenBot.GetCommandData function returns the data a command has stored about a User. (You can get Guild data directly from the BotContext.Guild Object)

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The Command whose data you want to get
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the user whose data you want to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>)

<aside class="warning">You must pass "this" as the Command argument. If you attempt to view/edit data owned by other commands, your command will be denied</aside>

## LibOpenBot.GetCommandSettings

> Example: Send a configurable greeting

```javascript
var Settings=await LibOpenBot.GetCommandSettings(this,BotContext.Guild);
Message.channel.send(Settings.Greeting);
```

The LibOpenBot.GetCommandSettings function returns the settings for a command.

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The Command whose setting you want to get
Guild | <a href="#guild">Guild | The Guild whose setting you want to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>

<aside class="warning">You must pass "this" as the Command argument. If you attempt to view/edit data owned by other commands, your command will be denied</aside>

## LibOpenBot.GetCommands

> Example: Fetch all of the commands in the current guild

```javascript
var CommandIDs=BotContext.Guild.Settings.Commands.map(c=>c.id);
var Commands=await LibOpenBot.GetCommands(CommandIDs);
```

The LibOpenBot.GetCommands function returns an array of Commands from an array of IDs.

Argument | Type | Description
-- | -- | --
IDs | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a>) | The IDs of the commands to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#command">Command</a>))

## LibOpenBot.GetDevs

> Example: Test if the user is a dev

```javascript
if((await LibOpenBot.GetDevs()).filter(d=>d==Context.user.id).length) {
    Message.channel.send('You\'re a dev!');
} else {
    Message.channel.send('You\'re a normal person!');
}
```

The LibOpenBot.GetDevs function returns the IDs of all of the Users with Developer Permissions

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a>))

## LibOpenBot.GetEmojis


> Example: Brag on how many emojis OpenBot supports

```javascript
var Emojis=await LibOpenBot.GetEmojis();
Message.channel.send(Emojis.lenth);
```

The LibOpenBot.GetEmojis function returns all of the Emojis indexed by OpenBot

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#emoji">Emoji</a>))

## LibOpenBot.GetFlakeStamp

> Example: Sort two commands by their creation date

```javascript
Commands.sort((c1,c2)=>LibOpenBot.GetFlakeStamp(c1)-LibOpenBot.GetFlakeStamp(c2));
```

The LibOpenBot.GetFlakeStamp function returns the timestamp of a snowflake

Argument | Type | Description
-- | -- | --
Flake | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The snowflake to get the timestamp of

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a>

## LibOpenBot.GetHoistedUsers

> Example: Output whether the current user is hoisted on the web search

```javascript
var Hoisted=await LibOpenBot.GetHoistedUsers();
if(Hoisted.filter(u=>u==Context.user.id).length) {
    Message.channel.send('You are hoisted!');
} else {
    Message.channel.send('You are a normal boi.');
}
```

The LibOpenBot.GetHoistedUsers function returns a list of all users with a role or status which hoists them in the user search.

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a>))

## LibOpenBot.GetLocales

> Example: Print the user's language in their own language

```javascript
var Locales=await LibOpenBot.GetLocales();
var Locale=Locales.filter(l=>l.code==BotContext.User.Settings.Language)[0];
if(Locale) {
    Message.channel.send(Locale.name);
}
```

The LibOpenBot.GetLocales function returns all of the Locales supported by OpenBot

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#locale">Locale</a>))

## LibOpenBot.GetPatreon

> Example: Print a user's patreon tier

```javascript
//Note: this might provide out of date data. To ensure up to date data, you need to use LibOpenBot.UpdatePatreonTier
var Patreon=await LibOpenBot.GetPatreon(Context.user.id);
Message.channel.send(Patreon.tier);
```

The LibOpenBot.GetPatreon function returns the patreon data for a user in OpenBot

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the User whose patreon data you want to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="#patreondata">PatreonData</a>)

## LibOpenBot.GetPatreons

> Example: Brag on how many patreon's OpenBot has

```javascript
var Patreons=await LibOpenBot.GetPatreons();
Message.channel.send(Patreons.length);
```

The LibOpenBot.GetPatreons function returns all of the patreons of OpenBot

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#patreondata">PatreonData</a>))

## LibOpenBot.GetPrivateStorage

> Example: Retrieve an api key from your private storage

```javascript
var APIKey=await LibOpenBot.GetPrivateStorage(this.Author,'YoutubeAPI');
```

The LibOpenBot.GetPrivateStorage function returns all or some of your private storage. Your private storage can be configured in your user settings on the OpenBot website.

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the User whose private storage you want to get.
Key | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Key of the private storage you want to get

### Key

If Key is null, then it will return all of the private storage. If key is a string, it will return the private storage entry that has that Key as its Name.

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>/<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a>)

<aside class="warning">If you attempt to get the private storage of another user other than yourself, your command will be denied.</aside>

## LibOpenBot.GetPullRequest

> Example: Print the person who created a pull request

```javascript
var Request=await LibOpenBot.GetPullRequest(Arguments);
Message.channel.send(Request.Editor);
```

The LibOpenBot.GetPullRequest function returns a Pull Request from its ID

Argument | Tyoe | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the Pull Request to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="#pullrequest">PullRequest</a>)

## LibOpenBot.GetPullRequests

> Example: Print the number of incoming pull requests you have

```javascript
var Requests=await LibOpenBot.GetPullRequests(Context.user.id);
Message.channel.send(Requests.length);
```

The LibOpenBot.GetPullRequests function gets all of the Pull Requests to a certain User's Commands.

Argument | Type | Description
-- | -- | --
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the User whose Pull Requests you want

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#pullrequest">PullRequest</a>))

## LibOpenBot.GetTimeouts

> Example: Print the number of timeouts in the active shard

```javascript
var Timeouts=await LibOpenBot.GetTimeouts();
Message.channel.send(Timeouts.length);
```

The LibOpenBot.GetTimeouts function returns all Timeouts for the current process.

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#Timeout">Timeout</a>)

## LibOpenBot.GetUser

> Example: Print the number of messages that a user has sent

```javascript
var User=await LibOpenBot.GetUser(Arguments);
if(User) {
    Message.channel.send(User.Stats.Messages);
}
```

The LibOpenBot.GetUser function returns a User from an ID

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the User to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="#user">User</a>)

## LibOpenBot.GetUserClass

> Example: Print whether the current user is a founder

```javascript
if(await LibOpenBot.GetUserClass(BotContext.User)==0) {
    Message.channel.send('You are a founder');
} else {
    Message.channel.send('You are not a founder');
}
```

The LibOpenBot.UserClass function returns a user's class.

Argument | Type | Description
-- | -- | --
User | <a href="#user">User</a> | The user whose class you want

The function returns the highest class the user has. For example, if a user is an Admin and a Dev, it will return Admin.

Return Value | Class
-- | --
0 | Founder
1 | Admin
2 | Mod
3 | Dev
4 | Translator
5 | Patreon
6 | Voter
7 | None

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a>)

## LibOpenBot.GetUserCommands

> Example: Print how many commands a user has created

```javascript
var Commands=await LibOpenBot.GetUserCommands(Context.user.id);
Message.channel.send(Commands.length);
```

The LibOpenBot.GetUserCommands function returns all of the Commands that a User has made

Argument | Type | Description
-- | -- | --
UserID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the User whose Commands you want to get

**Return Type:** Promise(Array(Command))

## LibOpenBot.GetUserData

> Example: Dm a user their private storage (Why though?)

```javascript
Context.user.send(JSON.stringify((await LibOpenBot.GetUserData(Context.user.id)).Private);
```
The LibOpenBot.GetUserData function returns the User Data of a user (Including Private Storage and Command Data).

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the User whose data you want to get

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#command">Command</a>))

<aside class="note">You do not need to directly interact with this function, instead you can use LibOpenBot.GetPrivateStorage or LibOpenBot.GetCommandData to get the individual parts of a User's data</aside>

## LibOpenBot.GetVerifiers

> Example: List the OpenBot verifiers

```javascript
var VerifierIDs=await LibOpenBot.GetVerifiers();
var Verifiers=[];
for(var ID of VerifierIDs)
    Verifiers.push(await LibOpenBot.GetUser(ID));
Message.channel.send(Verifiers.map(v=>v.Username).join(', '));
```

The LibOpenBot.GetVerifiers function returns the IDs of all of the Users who have Verifier Permissions

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#number">Number</a>))

## LibOpenBot.GetVerifyRequests

> Example: Print how many commands are waiting to be verified

```javascript
var Requests=await LibOpenBot.GetVerifyRequests();
Message.channel.send(Requests.length);
```

The LibOpenBot.GetVerifyRequests function returns all of the Verification requests in the queue.

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#verifyrequest">VerifyRequest</a>))

## LibOpenBot.GetWebLocales

> Example: Tell a user if their language is supported on the website

```javascript
var Locales=await LibOpenBot.GetWebLocales();
if(Locales.filter(l=>l==BotContext.User.Settings.Language).length)
    Message.channel.send('Your language is supported');
else
    Message.channel.send('Your language is not supported');
```

The LibOpenBot.GetWebLocales function returns all of the locale codes supported on OpenBot's Website

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a>))

## LibOpenBot.Guild

> Example: Create a new guild in the database if the current one is invalid

```javascript
//Honestly this would never happen, this is just an example
if((!BotContext.Guild)&&Context.guild)
    var Guild=new LibOpenBot.Guild(Context.guild);
```

The LibOpenBot.Guild function creates a new guild in the database

Argument | Type | Description
-- | -- | --
DiscordGuild | <a href="https://discord.js.org/#/docs/main/stable/class/Guild">guild</a> | A discord.js guild

**Return Type:** <a href="#guild">Guild</a>

## LibOpenBot.HasPermissions

> Example: Check if the bot has admin permissions in the current server

```javascript
var Member=await Context.guild.members.fetch(ObjDiscordClient.user.id);
if(Member) {
    if(LibOpenBot.HasPermissions(Member.permissions.bitfield,8))
        Message.channel.send('I am an admin');
    else
        Message.channel.send('I am not an admin');
}
```

The LibOpenBot.HasPermissions function compares two permissions bitfields to see whether they include eachother. It returns true if the user/entity has the permissions that it needs.

Argument | Type | Description
-- | -- | --
Has | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The Permissions that the user/entity has
Needs | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The Permissions that the user/entity needs

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean">Bool</a>

## LibOpenBot.LanguageIndex

> Example: Get the strings of your command in the user's language

```javascript
var Strings=this.Languages[LibOpenBot.LanguageIndex(this,BotContext.User.Settings.Language)].Strings;
Message.channel.send(Strings[0]);
```

The LibOpenBot.LanguageIndex function returns the index in which a language is found in a command.

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The command to search
Language | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The language to find

**Return type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a>

## LibOpenBot.PullRequest

> Example: Create a pull request for your command, from yourself, just to mess with us devs...

```javascript
//Don't do this
var Request=new LibOpenBot.PullRequest(this,this.Author,'I literally changed nothing');
```

The LibOpenBot.PullRequest function creates a new pull request to a command

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The Edited Command
Editor | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the editor of the command
Notes | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The notes about the edit

**Return Type:** <a href="#pullrequest">PullRequest</a>

## LibOpenBot.RegSearch

> Example: Search for commands from user input

```javascript
var Commands=await LibOpenBot.SearchCommands(Command=>Command.match(LibOpenBot.RegSearch(Arguments)));
Message.channel.send(Commands.length+' commands found');
```

The LibOpenBot.RegSearch function turns a search query into a valid reqular expression. This would be used when using String.match in the ReQL language to search for part of a string instead of a whole string (.eq) or regular expression (.match without using LibOpenBot.RegSearch).

Argument | Type | Description
-- | -- | --
Query | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Query to search for

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a>

## LibOpenBot.SearchCommands

> Example: Search for commands from user input

```javascript
var Commands=await LibOpenBot.SearchCommands(Command=>Command.match(LibOpenBot.RegSearch(Arguments)));
Message.channel.send(Commands.length+' commands found');
```

The LibOpenBot.SearchCommands function searches in the database for commands that match the search.

Argument | Type | Description
-- | -- | --
Search | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">Function</a> | The Search Criteria.

### Search

OpenBot supports using an Object `{Icon:":DopeIcon:"}` or an Anonymous Function `(Command)=>Command('Icon').eq(':DopeIcon:')`. You can learn how these parameters work <a href="https://rethinkdb.com/api/javascript/filter">here.</a>

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#command">Command</a>))

<aside class="note">The Anonymous Function looks like javascript, but it is actually written in ReQL. If you try to use Javascript comparitors it will not work.</aside>

## LibOpenBot.SearchGuilds

> Example: Search for guilds from user input

```javascript
var Guilds=await LibOpenBot.SearchGuilds(Guild=>Guild.match(LibOpenBot.RegSearch(Arguments)));
Message.channel.send(Guilds.length+' guilds found');
```

The LibOpenBot.SearchGuilds function searches in the database for guilds that match the search.

Argument | Type | Description
-- | -- | --
Search | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">Function</a> | The Search Criteria

### Search

OpenBot supports using an Object `{Icon:":DopeIcon:"}` or an Anonymous Function `(Command)=>Command('Icon').eq(':DopeIcon:')`. You can learn how these parameters work <a href="https://rethinkdb.com/api/javascript/filter">here.</a>

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#guild">Guild</a>))

<aside class="note">The Anonymous Function looks like javascript, but it is actually written in ReQL. If you try to use Javascript comparitors it will not work.</aside>

## LibOpenBot.SearchUsers

> Example: Search for users from user input

```javascript
var Users=await LibOpenBot.SearchUsers(User=>User.match(LibOpenBot.RegSearch(Arguments)));
Message.channel.send(Users.length+' users found');
```

The LibOpenBot.SearchUsers function searches in the dtabase for users that match the search.

Argument | Type | Description
-- | -- | --
Search | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">Function</a> | The Search Criteria

### Search

OpenBot supports using an Object `{Icon:":DopeIcon:"}` or an Anonymous Function `(Command)=>Command('Icon').eq(':DopeIcon:')`. You can learn how these parameters work <a href="https://rethinkdb.com/api/javascript/filter">here.</a>

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise"></a>Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="#user">User</a>))

<aside class="note">The Anonymous Function looks like javascript, but it is actually written in ReQL. If you try to use Javascript comparitors it will not work.</aside>

## LibOpenBot.Timeout

> Example: Respond after 10 seconds

```javascript
var Timeout=new LibOpenBot.Timeout(10000,()=>{
    ObjDiscordClient.channels.cache.array().filter(c=>c.id==Argument.channel)[0].send('Super lag')
},{channel:Message.channel.id});
```

The LibOpenBot.Timeout function creates a new timeout. (Must be called with "new" keyword, ie `new LibOpenBot.Timeout(x,y,z)`)
The function provided, if it contains arguments, will always rename the arguments to Argument, so make sure your code accesses Argument under the variable name Argument. For example, the function `(Number)=>{return Number+1}` will be executed as `(Argument)=>{return Number+1}`, so make sure you name your argument "Argument"
The argument provided must not contain circular references. (So no discord.js objects, etc.). It must be possible to convert the argument to JSON.

Argument | Type | Description
-- | -- | --
Time | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The time (in milliseconds) until the code should be run
Func | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">Function</a> | The function to run
Argument | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | An argument to pass to the function

**Return Type:** <a href="#Timeout">Timeout</a>

## LibOpenBot.UpdatePatreonTier

> Example: Update a patreon's tier before using it

```javascript
var Patreon=await LibOpenBot.GetPatreon(Context.user.id);
//Method 1: Update in place and then print
await LibOpenBot.UpdatePatreonTier(Patreon);
Message.channel.send(Patreon.tier);
//Method 2: Print immediately
Message.channel.send(await LibOpenBot.UpdatePatreonTier(Patreon));
```

The LibOpenBot.UpdatePatreonTier fetches a patreon's tier from the Patreon API to ensure it is correct, returns it, and updates the db. You should run this before doing mission critical things with a patreon's data.

Argument | Type | Description
-- | -- | --
PatreonData | <a href="#patreondata">PatreonData</a> | The PatreonData that you want to update the tier of

**Return Type:** String

## LibOpenBot.User

> Example: Create a user if they are missing

```javascript
//This would never happen
if(Context.user&&!BotContext.User)
    BotContext.User=new LibOpenBot.User(Context.user);
```

The LibOpenBot.User function creates a new user in the database.

Argument | Type | Description
-- | -- | --
DiscordUser | <a href="https://discord.js.org/#/docs/main/stable/class/User">user</a> | A discord.js user

**Return Type:** <a href="#user">User</a>

## LibOpenBot.UserData

> Example: Do i really need to make examples for stuff you don't need to use?

```javascript
var Data=await LibOpenBot.GetUserData(Context.user.id);
if(!Data) {
    //Note: this would never get run, since LibOpenBot.GetUserData creates data if it doesnt exist
    Data=new LibOpenBot.UserData(Context.user.id);
}
```

The LibOpenBot.UserData function creates a new UserData entry in the database

Argument | Type | Description
-- | -- | --
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the user whose data this is

**Return Type:** <a href="#userdata">UserData</a>

## LibOpenBot.VerifyRequest

> Example: Create a verify request for your command, from yourself, just to mess with us devs...

```javascript
//Don't do this.
var Request=new LibOpenBot.VerifyRequest(this,this.Author,'I literally changed nothing',Message.id);
```

The LibOpenBot.VerifyRequest function creates a new verification request to a command

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The Edited Command
Editor | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the editor of the command
Notes | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The notes about the edit
Message | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The id of the verification message

**Return Type:** <a href="#verifyrequest">VerifyRequest</a>

## LibOpenBot.WriteCommand

> Example: Bypass verification to edit your command's icon

```javascript
//Note: don't do this, your command will get denied
this.Icon=':smile:';
LibOpenBot.WriteCommand(this);
```

The LibOpenBot.WriteCommand function writes a command to the database, saving any changes that may have been made.

Argument | Type | Descrpition
-- | -- | --
Command | <a href="#command">Command</a> | The Command to save

## LibOpenBot.WriteCommandData

> Example: Save a note on a user for later

```javascript
var Data=await LibOpenBot.GetCommandData(this,Context.user.id);
Data.note=Arguments;
LibOpenBot.WriteCommandData(this,Context.user.id,Data);
```

The LibOpenBot.WriteCommandData function writes a CommandData object to the database

Argument | Type | Description
-- | -- | --
Command | <a href="#command">Command</a> | The Command that the data belongs to
User | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The ID of the user that the data is about
Data | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The Data to write

<aside class="note">This will overwrite the previous value, not just modify it. Also, CommandData is stored by Author, not Command, so all of your commands share the same entry.</aside>

## LibOpenBot.WriteGuild

> Example: Add yourself as an admin to a guild

```javascript
//Note: obviously, don't do this
BotContext.Guild.Settings.Admins.push(this.Author);
LibOpenBot.WriteGuild(BotContext.Guild);
```

The LibOpenBot.WriteGuild function writes a guild to the database, saving any changes that may have been made.

Argument | Type | Description
-- | -- | --
Guild | <a href="#guild">Guild</a> | The Guild to save

## LibOpenBot.WritePrivateStorage

> Example: Add a key to your private storage

```javascript
var Storage=await LibOpenBot.GetPrivateStorage(this.Author);
Storage['Top Secret']='Grandma\'s cookie recipe';
LibOpenBot.WritePrivateStorage(this.Author,Storage);
```


The LibOpenBot.WritePrivateStorage function writes a PrivateStorage object to the database, saving any changes that may have been made.

Argument | Type | Description
-- | -- | --
ID | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number">Number</a> | The User ID that the storage belongs to
Value | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a> | The value of the private storage

<aside class="note">This will overwrite the entire private storage, not just update one key.</aside>

## LibOpenBot.WritePullRequest

> Example: Just don't

```javascript
//Just don't use this function, idek why i put the non-useful functions in here.
```

The LibOpenBot.WritePullRequest function writes a pull request to the database, saving any changes that may have been made.

Argument | Type | Description
-- | -- | --
PullRequest | <a href="#pullrequest">PullRequest</a> | The Pull Request to save

## LibOpenBot.WriteTimeout

> Example: Change the argument of a timeout after you create it

```javascript
var Timeout=new LibOpenBot.Timeout(1000,()=>console.log(Argument.log));
Timeout.Argument={log:'Hello world!'};
LibOpenBot.WriteTimeout(Timeout);
```

The LibOpenBot.WriteTimeout function writes a timeout to the database, saving any changes that may have been made.

Argument | Type | Description
-- | -- | --
Timeout | <a href="#timeout">Timeout</a> | The Timeout to save

## LibOpenBot.WriteUser

> Example: Reset your message count to 0

```javascript
//But why?
BotContext.User.Stats.Messages=0;
LibOpenBot.WriteUser(BotContext.User);
```

The LibOpenBot.WriteUser function writes a user to the database, saving any changes that may have been made.

Argument | Type | Description
-- | -- | --
User | <a href="#user">User</a> | The User to save

## LibOpenBot.WriteUserData

> Example: Clear a user's command data, and break all of the commands

```javascript
var Data=await LibOpenBot.GetUserData(Context.user.id);
Data.Commands=[];
LibOpenBot.WriteUserData(Data);
```

The LibOpenBot.WriteUserData function writes a UserData object to the database, saving any changes that may have been made

Argument | Type | Description
-- | -- | --
UserData | <a href="#userdata">UserData</a> | The UserData to save

<aside class="note">You most likely will not need to use this function directly, instead you can use LibOpenBot.WritePrivateStorage or LibOpenBot.WriteCommandData to write the individual parts of a UserData Object</aside>

## LibOpenBot.WriteVerifyRequest

> Example: Just don't

```javascript
//Just don't use this function, idek why i put the non-useful functions in here.
```

The LibOpenBot.WriteVerifyRequest function writes a verify request to the database, saving any changes that may have been made.

Argument | Type | Description
-- | -- | --
VerifyRequest | <a href="#verifyrequest">VerifyRequest</a> | The Verify Request to save

## LibOpenBot.sendRelay

> Example: Do math on the master process instead of on the shard cuz why not

```javascript
var OnePlusOne=await LibOpenBot.sendRelay('Master',{type:'script',data:'return 1+1'});
Message.channel.send(OnePlusOne);
```

The LibOpenBot.sendRelay function sends a message to another process, and retrieves the result.

Argument | Type | Description
-- | -- | --
Proc | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">String</a> | The Name of the process to send a relay to
Data | <a href="#relay">Relay</a> | The Relay to send

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>)

## LibOpenBot.sendRelayShards

> Example: Make sure that math works right on all the shards

```javascript
var Results=await LibOpenBot.sendRelayShards({type:'script',data:'return 1+1'});
var Correct=1+1;
var Broken=false;
for(var Result of Results)
    if(Result!=Correct)
        Broken=true;
if(Broken)
    Message.channel.send('Math is broken somewhere!');
else
    Message.channel.send('Math is working fine everywhere');
```

The LibOpenBot.sendRelayShards function sends a message to all of the shards and retrieves the result.

Argument | Type | Description
-- | -- | --
Data | <a href="#relay">Relay</a> | The Relay to send

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>))

## LibOpenBot.sendRelayAll

> Example: Make sure that math works right on all the processes

```javascript
var Results=await LibOpenBot.sendRelayAll({type:'script',data:'return 1+1'},true);
var Correct=1+1;
var Broken=false;
for(var Result of Results)
    if(Result!=Correct)
        Broken=true;
if(Broken)
    Message.channel.send('Math is broken somewhere!');
else
    Message.channel.send('Math is working fine everywhere');
```

The LibOpenBot.sendRelayAll function sends a message to all of the processes and retrieves the result

Argument | Type | Description
-- | -- | --
Data | <a href="#relay">Relay</a> | The Relay to send
Master | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Bool</a> | Whether to send it to the master process

**Return Type:** <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promise</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array</a>(<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">Object</a>))

## RunEvent

> Example: Execute a custom event

```javascript
var Result=await RunEvent(this,'MyEvent',Context,BotContext,'Super good argument');
```

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

NPM Page: <a href="https://www.npmjs.com/package/discord.js">discord.js</a>

Docs: <a href="https://discord.js.org/">discord.js.org</a>

Version: 12.0

## LibOpenBot

LibOpenBot references the OpenBot API. It is used for interacting with OpenBot's database.

Docs: <a href="https://docs.openbot.ga/">docs.openbot.ga</a>

Version: 1.4.0

## LibJuration

LibJuration references the `juration` npm package. It is used for converting seconds to a human readable time format.

NPM Page: <a href="https://www.npmjs.com/package/juration">juration</a>

Version: 0.1.1