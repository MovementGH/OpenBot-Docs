
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

# Editable Variables

In addition to function variables, there are some variables accessible to every event that can be edited.


### CurrentUserData

**Type:** <a href="#userdata">UserData</a>

**Description:** The CurrentUserData variable will always contain the UserData of the user who send the message. Basically it is the result of GetUserData(Message.author). It is also editable, so if you are writing a command like Change Locale, you can just edit the CurrentUserData variable and their locale will be changed

### CurrentUserLocale

**Type:** String

**Description:** The CurrentUserLocale is different than CurrentLocale. CurrentUserLocale is the actual locale the user is using, formatted as a string. It can be useful if you want to reference another command but dont know what languages it supports, as FindCommand takes its locale argument as a string.

# Const Variables

Finally, there are some variables which provide information about OpenBot but cannot be edited.

### GlobInvite

**Type:** String

**Description:** The GlobInvite variable contains the invite link to OpenBot (mainly so i dont forget it) but if you want, make a command to print it out and promote OpenBot

### GlobDiscordClient

**Type:** Client

**Description:** The GlobDiscordClient is the discord.js Client class used to login to OpenBot. You can use it to find out information like how many servers OpenBot is in.

<aside class="warning">Do not attempt to do malicious stuff like grabbing OpenBot's token or anything. Your command will get rejected by the mods. Banne!</aside>
