# Editor UI

The editor is a powerful tool, but its ui can be a bit confusing at first glance. Here are some explainations on what different things do

## Command MetaData

The Command MetaData box holds all of the MetaData for your command. This includes its version, syntax, support link, icon, etc. This is the information that shows up when someone calls `-Open Cominfo [Your Command]`

### Syntax

The syntax field is displayed after the name of your command in help menus, searches, etc. It should tell users what kinds of arguments your command expects them to include. For example, the syntax for a kick command could be something like `[@Mention]`. The square brackets `[]` indicate a required parameter which is an @Mention of a user.

Suggested formatting:

**[Param]** - Required

**{Param}** - Optional

**Param** - Literal text

**(No Arguments)** No paramaters

### Icon

Your command's icon is displayed next to it in help menus, searches, and more. It should give some idea of what your command does. The icon can be any discord emoji. If it is a default emoji, it should be entered into the icon field like `:smile:`, wheras if it is a custom emoji, it should be entered in like `<:AddCommand:539643411179896835>`. To find the ID of your custom emoji, right click it in discord and click copy link. The long number in the link is the ID of your emoji.

### Support Link

The support link is displayed under your command in detailed information screens, and when your command crashes. You can set it to your server or OpenBot's server. Wherever you want people to go when your command breaks.

The support link must be formatted like `https://discordapp.com/invite/abcdef` with abcdef being the invite code.

### Version

This field is mainly asthetic. Set it to any number you like.

### ExecutePerms

The ExecutePerms are the permissions that a user calling your command needs in order to call it. You can calculate permissions at the <a href="https://discordapi.com/permissions.html">Official Discord Permissions Calculator</a>

### BotPerms

The BotPerms are the permissions that OpenBot needs in order to run your command. You can calculate permissions at the <a href="https://discordapi.com/permissions.html">Official Discord Permissions Calculator</a>

### Open Source

If your command is marked as open source, other users will be able to use the `-Open Viewsource` command to view its source and see how you work your magic.

### Pull Requests

If your command is marked as allowing pull requests, other users will be able to use the `-Open Editsource` command to edit its source. All edits will be DMed to you for approval before being submitted to the Core Developers

## Locales

Locales allow your command to support multiple languages. If your command does not support the locale a user is using, the uppermost locale in your list will be used.

### Language

Each locale has a language tag. This language tag tells OpenBot what language the locale is. If you wish to support a language that is not listed here, please contact a Core Developer to get it added.

### Command Name

The full name of your command, translated to the language marked by the Language field.

### Command Callname

The callname of your command. This is the string that people will use to actually activate your command. For example, a kick command could have a name of `Kick User` but a callname of `Kick`.

### Command Description

A detailed description of what your command does

### Translation Strings

Translation strings allow the text inside your command to be translated. You can have as many translation strings as you want, and you can access them from your code. For example, `this.String[CurrentLocale][0]` would return Translation String 0.

## Events

Your command can have multiple events, or just one. These are where you put your actual code. The eye button on the right side of the box lets you hide and show events to prevent UI clutter. The "Active" checkbox toggles whether your command is registered as supporting that event. The events you register will be shown in your ComInfo listing and the events that you dont register will not be executed, making the bot run faster.

**onCall**

The onCall event is executed whenever a message matches Prefix + Callname. It gets <a href="#oncall">these</a> variables

**onReactionAdd**

The onReactionAdd event is executed whenever a reaction is added to a message. It is up to you to determine whether or not the reaction is relavent. It gets <a href="#onreactadd-onreactrem">these</a> variables.

**onReactionRem**

The onReactionRem event is executed whenever a reaction is removed from a message. It is up to you to determine whether or not the reaction is relavent. It gets <a href="#onreactadd-onreactrem">these</a> variables.

**onMemberJoin**

The onMemberJoin event is executed whenever a user joins a guild. It gets <a href="#onmemberjoin-onmemberleave">these</a> variables.

**onMemberLeave**

The onMemberLeave event is executed whenever a user leaves a guild. It gets <a href="#onmemberjoin-onmemberleave">these</a> variables.

**onMemberUpdate**

The onMemberUpdate event is executed whenever a guild member's properties change. This can be roles, nicknames, etc. It gets <a href="#onmemberupdate-onvoiceupdate-onpresenceupdate">these</a> variables.

**onMemberBan**

The onMemberBan event is executed whenever a member is banned from a guild. It gets <a href="#onmemberban-onmemberunban">these</a> variables.

**onMemberUnban**

The onMemberUnban event is executed whenever a member is unbanned from a guild. It gets <a href="#onmemberban-onmemberunban">these</a> variables.

**onBotJoin**

The onBotJoin event is executed when OpenBot joins a server, or when your command is added to a server. It gets <a href="#onbotjoin-onbotleave">these</a> variables.

**onBotLeave**

The onBotLeave event is executed when OpenBot leaves a server, or when your command is removed from a server. It gets <a href="#onbotjoin-onbotleave">these</a> variables.

**onChannelCreate**

The onChannelCreate event is executed when a channel is created. It gets <a href="#onchannelcreate-onchanneldelete">these</a> variables.

**onChannelDelete**

The onChannelDelete event is executed when a channel is deleted. It gets <a href="#onchannelcreate-onchanneldelete">these</a> variables.

**onChannelUpdate**

The onChannelUpdate event is executed when a channel is updated. It gets <a href="#onchannelupdate">these</a> variables.

**onMessageDelete**

The onMessageDelete event is executed whenever a message is deleted. It gets <a href="#onmessagedelete">these</a> variables.

**onPinsUpdate**

The onPinsUpdate event is executed whenever the pins of a channel are updated. It gets <a href="#onpinsupdate">these</a> variables.

**onEmojiCreate**

The onEmojiCreate event is executed whenever a custom emoji is created on a server. It gets <a href="#onemojicreate-onemojidelete">these</a> variables.

**onEmojiDelete**

The onEmojiDelete event is executed whenever a custom emoji is deleted on a server. It gets <a href="#onemojicreate-onemojidelete">these</a> variables.

**onEmojiUpdate**

The onEmojiUpdate event is executed whenever a custom emoji is updated on a server. It gets <a href="#onemojiupdate">these</a> variables.

**onMessageUpdate**

The onMessageUpdate event is executed whenever a message is edited. It gets <a href="#onmessageupdate">these</a> variables.

**onRoleCreate**

The onRoleCreate event is executed whenever a role is created on a server. It gets <a href="#onrolecreate-onroledelete">these</a> variables.

**onRoleDelete**

The onRoleDelete event is executed whenever a role is deleted on a server. It gets <a href="#onrolecreate-onroledelete">these</a> variables.

**onRoleUpdate**

The onRoleUpdate event is executed whenever a role is updated on a server. It gets <a href="#onroleupdate">these</a> variables.

**onUserUpdate**

The onUserUpdate event is executed whenever a user updates their details, for example if they change their username. It gets <a href="#onuserupdate">these</a> variables.

**onVoiceUpdate**

The onVoiceUpdate event is executed whenever a user joins a voice channel. It gets <a href="#onmemberupdate-onvoiceupdate-onpresenceupdate">these</a> variables.

**onGuildUpdate**

The onGuildUpdate event is executed whenever a guilds name, region, etc is updated. It gets <a href="#onguildupdate">these</a> variables.

**onPresenceUpdate**

The onPresenceUpdate event is executed when users come online, offline, enter a game, etc. It gets <a href="#onmemberupdate-onvoiceupdate-onpresenceupdate">these</a> variables.

**onMessage**

The onMessage event is executed when a message arives, whether is is a command call or not. It is usefull for spam filters and the like. It gets <a href="#onmessagedelete-onmessage">these</a> variables.
