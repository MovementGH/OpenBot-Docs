---


# BEING REWRITTEN

---
title: OpenBot API

language_tabs:
 - javascript

toc_footers:
- <a href='../'>Start Using OpenBot</a>
- <a href='https://github.com/lord/slate'>Powered by Slate</a>

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

## MetaData

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

## Language Support

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

Translation strings allow the text inside your command to be translated. You can have as many as you want, and you can access them from your code.

> Example: How to use translation strings

```javascript
//Access String 0
this.Languages[LibOpenBot.LanguageIndex(this,BotContext.User.Settings.Language].Strings[0];

//Make a reference to the strings for cleaner code
var Strings=this.Languages[LibOpenBot.LanguageIndex(this,BotContext.User.Settings.Language].Strings;
//Later...
Strings[0];
```


 
 

