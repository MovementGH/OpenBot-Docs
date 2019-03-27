
# Function Variables

Every OpenBot command is actually a function, which gets passed several variables. These variables belong to your function, so editing them does nothing.

## Message

> Sending "pong" back through the channel the message came from

```javascript
Message.channel.send("pong!");
```

> Will output this

```output
pong!
```

The Message variable will always contain the message that called your command. You can use it to respond, get the author, or anything else you want.

### Type: Message


## CurrentLocale

> Saying "hi" to the user in their native language

```javascript
Message.channel.send(this.String[CurrentLocale][0]);
```

> Will output something like this depending on what you set your String to

```output
Hi!

or

Hola!
```

The CurrentLocale variable will always contain the index of your Names, Descriptions, Strings, etc. that contains the language which the author of the message is using. Basically, it is the result of `FindLocale(this,GetUserData(Message.author).Locale)`.

### Type: Number

## FilteredMessage

> Sending "ding dong" when the user includes "pong" in your ping command

```javascript
if(FilteredMessage=="pong")
    Message.channel.send("ding dong");
else
    Message.channel.send("pong")
```

> Will output one of these

```output
pong

or

ding dong
```

The FilteredMessage variable will always contain the content of the message with your commands callname filtered out. For example, if Message.content is "-Open add new command" then FilteredMessage is "new command"

### Type: String

# Editable Variables

In addition to the read-only variables, there are some variables accessible to every command that can be edited.

## CurrentUserData

> Printing out the number of messages that the caller of the command has sent

```javascript
Message.channel.send(CurrentUserData.MessageCount);
```

> Will output something like this

```output
1336
```

The CurrentUserData variable will always contain the UserData of the user who send the message. Basically it is the result of GetUserData(Message.author). It is also editable, so if you are writing a command like Change Locale, you can just edit the CurrentUserData variable and their locale will be changed

### Type: <a href="#userdata">UserData</a>

## CurrentUserLocale

> Printing out the current user's locale

```javascript
Message.channel.send(CurrentUserLocale)
```

> Will output something like this

```output
en
```

The CurrentUserLocale is different than CurrentLocale. CurrentUserLocale is the actual locale the user is using, formatted as a string. It can be useful if you want to reference another command but dont know what languages it supports, as FindCommand takes its locale argument as a string.

### Type: String

# Const Variables

## GlobInvite

> Outputting an invite link for OpenBot

```javascript
Message.channel.send(GlobInvite)
```

> Will output this (please click ;) ik u want to)

```output
https://discordapp.com/oauth2/authorize?client_id=497087852568641536&scope=bot&permissions=2146958839
```

The GlobInvite variable contains the invite link to OpenBot (mainly so i dont forget it) but if you want, make a command to print it out and promote OpenBot

### Type: String

## GlobDiscordClient

> Outputting OpenBot's Username

```javascript
Message.channel.send(GlobDiscordClient.user.username)
```

> Will output this

```output
OpenBot
```

The GlobDiscordClient is the discord.js Client class used to login to OpenBot. You can use it to find out information like how many servers OpenBot is in.

### Type: Client

<aside class="warning">Do not attempt to do malicious stuff like grabbing OpenBot's token or anything. Your command will get rejected by the mods. Banne!</aside>
