---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='../'>Start Coding</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the OpenBot API!

We appreciate any contributions you make to OpenBot's commands, and as such we feel it is important to provide a quality API. If you have any questions about the API, feel these Docs are unclear, or anything else, please go to the official OpenBot Development Server and let us know.

<aside class="notice"> OpenBot only supports code written in node.js using the discord.js library to interact with Discord </aside>

# Classes

## UserData

> Example: Printing out a user's Username, ID, and Avatar

```javascript
console.log(CurrentUserData.UserName);
console.log(CurrentUserData.UserID);
console.log(CurrentUserData.AvatarURL);
```
> This will output something along the lines of this:

```output
Movement
473469567323078676
https://cdn.discordapp.com/avatars/473469567323078676/1a679b6f2c447e33133440f1421eb1d0.png?size=2048
```

Information about a user is stored in the UserData class.

Member | Description
--------- | -----------
UserID | The ID of the user
UserName | The Username of the user
AvatarURL | The URL of the user's discord avatar
MessageCount | The number of message the user has sent
Locale | The locale the user is using
CommandData | Data stored by commands about this user
