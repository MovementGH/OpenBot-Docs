
# Read-Only Variables

Every OpenBot command is actually a function, which gets passed several variables. These variables belong to your function, so editing them does nothing.

## Message

> Sending "pong" back through the channel the message came from

```javascript
Message.channel.send("pong!");
```

The Message variable will always contain the message that called your command. You can use it to respond, get the author, or anything else you want.

### Type: Message


## CurrentLocale

> Saying "hi" to the user in their native language

```javascript
Message.channel.send(this.String[CurrentLocale][0]);
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
The FilteredMessage variable will always contain the content of the message with your commands callname filtered out. For example, if Message.content is "-Open add new command" then FilteredMessage is "new command"
