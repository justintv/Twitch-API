# Connecting to IRC

Twitch offers an IRC interface to its chat. This allows for people to do things like develop bots for their channel, or to connect to a channel's chat with an IRC client instead of using the web interface. While our IRC server is built to follow [RFC1459](http://tools.ietf.org/html/rfc1459.html), it is important to note that there are some cases where it will behave slightly differently than another IRC server would. These cases are noted when necessary in the following document.

Lines prefixed with < are sent from client to server, and lines prefixed with > are sent from the server to the connecting client.

## Prerequisites
In order to connect to Twitch IRC, you must have two pieces of information:

1. The name of channel that you want to join.
2. A Twitch account.

## Connecting
Once you have that information, you can then take it to connect to Twitch IRC with the following bits of information:

- The server name to connect to is: *irc.twitch.tv*.
- The port to connect to is *6667*.
- SSL **is not** supported for Twitch IRC.
- Your nickname must be your Twitch nickname

### If you are connecting with an IRC client
- Your password should be your Twitch password.

### With a bot or app for multiple users
- An OAuth token for the user, with the `chat_login` scope. The token must have the prefix of `oauth:`. For example, if you have the token `abcd`, you send `oauth:abcd`.

## Upon a Successful Connection
A successful connection session will look something like this:
```
< PASS oauth:twitch_oauth_token
< NICK twitch_username
> :tmi.twitch.tv 001 twitch_username :connected to TMI
> :tmi.twitch.tv 002 twitch_username :your host is TMI
> :tmi.twitch.tv 003 twitch_username :this server is pretty new
> :tmi.twitch.tv 004 twitch_username tmi.twitch.tv 0.0.1 w n
> :tmi.twitch.tv 375 twitch_username :- tmi.twitch.tv Message of the day - 
> :tmi.twitch.tv 372 twitch_username :- not much to say here
> :tmi.twitch.tv 376 twitch_username :End of /MOTD command
```

About once every five minutes, you will receive a `PING channelname.jtvirc.com` from the server, in order to ensure that your connection to the server is not prematurely terminated, you should reply with `PONG channelname.jtvirc.com`.

## On an Unsuccessful Connection
If your connection fails for any reason, you will be disconnected from the server. Some common reasons for being disconnected immediately include:

- Connecting on the wrong port
- Connecting to the wrong server
- Using an incorrect username and/or password

## Commands you can send
If you send an invalid command, you will receive a 421 numeric back:
```
< CAP REQ :multi-prefix
> :tmi.twitch.tv 421 you CAP :Unknown command
```

A brief list of commands supported by our IRC server include:
### JOIN: Opening up a chat room (and obtaining a list of users)
**JOIN** *#channelname*

Notes:

- You should not JOIN any chat room other than the one which you are connected to the server of.
- See [Further Notes](https://github.com/justintv/Twitch-API/blob/master/IRC.md#further-notes-about-lists-of-users) for more information
- After a successful JOIN, the following will take place:

1. You will be sent a list of users that are currently in the channel.
2. A number of MODEs will be set from the **jtv** user to signify that a user can moderate chat. Users that can moderate chat are are defined as *Channel Moderators*, *Admin*'s and *Staff*.

```
< JOIN #channelname
> JOIN #channelname
> 353: = #channelname nickname nickname2 nickname3 nickname4 anotherNickname
> 353: = #channelname nickname25 nickname26 nicknameN
> 366: #channelname End of /NAMES list
> jtv MODE #ignproleague +o ignproleague
> jtv MODE #ignproleague +o ravager01
> jtv MODE #ignproleague +o mirhi
> jtv MODE #ignproleague +o zadr
```
### PART: Leaving a chat room
**PART** *#channelname*
```
< PART #channelname
> PART #channelname
````
### WHO: Obtaining a detailed list of users
**WHO** *#channel*
```
< WHO #channelname
> 352: #channelname nickname channelname.tmi.twitch.tv tmi.twitch.tv username H 0 realname
> 352: #channelname nickname2 channelname.tmi.twitch.tv tmi.twitch.tv username H 0 realname
> ...
> 352: #channelname nicknameN channel.tmi.twitch.tv tmi.twitch.tv username H 0 realname
> 315: #channelname End of /WHO list
```

## Commands you may receive
### JOIN: Someone joined a channel!
```:nickname!username@nickname.tmi.twitch.tv JOIN #channelname```

### PART: Someone parted a channel
```:nickname!username@nickname.tmi.twitch.tv PART #channelname```

### PRIVMSG: Someone sent a message to a channel
```:nickname!username@nickname.tmi.twitch.tv PRIVMSG #channel :message that was sent```

## Further notes about lists of users

- A list of users that are currently in a channel is sent after a successful JOIN, so WHO is often not required.
- Due to caching, JOINs and PARTs are not sent immediately to a channel. They are instead batched up and sent every 10 seconds.
- After receiving your initial list of users or after performing your first WHO, it is recommended to process PARTs and JOINs as they come in instead of re-requesting this list from the server.
- Due to caching, the response of this command may be delayed by up to 10 seconds on initial connect and may be up, but no more than, to 10 seconds out of date.
- You cannot request a list of users for a channel that you did not JOIN.
