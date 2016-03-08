# Twitch IRC

Twitch offers an IRC interface to its chat. This allows for people to do things like develop bots for their channel, or to connect to a channel's chat with an IRC client instead of using the web interface. While our IRC server is built to follow [RFC1459](http://tools.ietf.org/html/rfc1459.html), it is important to note that there are *several* cases where it will behave slightly differently than another IRC server would. These cases are noted when necessary in the following document.

Such differences in behavior are **necessary** both to accommodate the massive scale at which our chat servers must operate, as well as the complex Twitch-specific features that we provide our users.

Lines prefixed with < are sent from client to server, and lines prefixed with > are sent from the server to the connecting client.

## Connecting

You can connect to Twitch IRC using the following bits of information:

- The server name to connect to is: `irc.chat.twitch.tv`.
<<<<<<< 1e79c18b5bb0bf1c30587ae19d751be36730c4e4
- The port to connect to is `6667`
- SSL is supported on `irc.chat.twitch.tv` on port 443
=======
- The port to connect to is `6667`, or `6697` for SSL.
>>>>>>> SSL support via 6697
- Your nickname must be your Twitch username in lowercase.
- Your password should be an OAuth token [authorized through our API](/authentication.md) with the `chat_login` scope.
  - The token must have the prefix of `oauth:`. For example, if you have the token `abcd`, you send `oauth:abcd`.
  - You can quickly get a token for your account with this helpful [page](http://twitchapps.com/tmi/) (thanks to [Andrew Bashore](https://github.com/bashtech)!).

## Upon a Successful Connection

A successful connection session will look something like this:

```
< PASS oauth:twitch_oauth_token
< NICK twitch_username
> :tmi.twitch.tv 001 twitch_username :Welcome, GLHF!
> :tmi.twitch.tv 002 twitch_username :Your host is tmi.twitch.tv
> :tmi.twitch.tv 003 twitch_username :This server is rather new
> :tmi.twitch.tv 004 twitch_username :-
> :tmi.twitch.tv 375 twitch_username :-
> :tmi.twitch.tv 372 twitch_username :You are in a maze of twisty passages, all alike.
> :tmi.twitch.tv 376 twitch_username :>
```

About once every five minutes, you will receive a `PING :tmi.twitch.tv` from the server, in order to ensure that your connection to the server is not prematurely terminated, you should reply with `PONG :tmi.twitch.tv`.

## On an Unsuccessful Connection

If your connection fails for any reason, you will be disconnected from the server. Some common reasons for being disconnected immediately include:

- Connecting on the wrong port
- Connecting to the wrong server
- Using an incorrect username and/or password

## Command & Message Limit

- If you send more than 20 commands or messages to the server within a 30 second period, you will be locked out for 2 hours automatically. These are *not* lifted so please be careful when working with IRC!
- This limit is elevated to 100 messages per 30 seconds for users that *only* send messages/commands to channels in which they have Moderator/Operator status.

## Commands you can send

If you send an invalid command, you will receive a 421 numeric back:

```
< WHO #channel
> :tmi.twitch.tv 421 twitch_username WHO :Unknown command
```

A brief list of commands supported by our IRC server include:
### JOIN: Opening up a chat room

**JOIN** *#channel*

Note: After a successful `JOIN`, you will *not* receive a membership state events (`NAMES`, `JOIN`, `PART`, or `MODE`) *unless* you've requested our [IRCv3 `Membership`](#membership) capability. The channel name should be entered in lowercase.

```
< JOIN #channel
> :twitch_username!twitch_username@twitch_username.tmi.twitch.tv JOIN #channel
> :twitch_username.tmi.twitch.tv 353 twitch_username = #channel :twitch_username
> :twitch_username.tmi.twitch.tv 366 twitch_username #channel :End of /NAMES list
```

### PART: Leaving a chat room

**PART** *#channel*

```
< PART #channel
> :twitch_username!twitch_username@twitch_username.tmi.twitch.tv PART #channel
````

### PRIVMSG: Sending a message

**PRIVMSG** *#channel* :Message to send

Basic message reception is as follows:

```
> :twitch_username!twitch_username@twitch_username.tmi.twitch.tv PRIVMSG #channel :message here
```

# Twitch Capabilities

Using IRCv3 capability registration, it is possible to register for Twitch-specific capabilities. The capabilities are defined below:

## Membership

```
< CAP REQ :twitch.tv/membership
> :tmi.twitch.tv CAP * ACK :twitch.tv/membership
```

Adds membership state event (`NAMES`, `JOIN`, `PART`, or `MODE`) functionality. By default we do *not* send this data to clients without this capability.

### NAMES

The list of current chatters in a channel:

```
> :twitch_username.tmi.twitch.tv 353 twitch_username = #channel :twitch_username user2 user3
> :twitch_username.tmi.twitch.tv 353 twitch_username = #channel :user5 user6 nicknameN
> :twitch_username.tmi.twitch.tv 366 twitch_username #channel :End of /NAMES list
```

### JOIN

Someone joined a channel:

```
> :twitch_username!twitch_username@twitch_username.tmi.twitch.tv JOIN #channel
```

### PART

Someone left a channel:

```
> :twitch_username!twitch_username@twitch_username.tmi.twitch.tv PART #channel
```

### MODE

Someone gained or lost operator:

```
> :jtv MODE #channel +o operator_user
> :jtv MODE #channel -o operator_user
```

*Notes*:
- If there are greater than 1000 chatters in a room, NAMES will only return the list of OPs currently in the room
- Due to caching, events are not sent immediately to a channel. They are instead batched up and sent every 10 seconds.
- `WHO` is unsupported
- All elevated users are given OP. To determine a user's actual elevation level, request the [tags](#tags) capability and parse the `user-type` tag

## Commands

```
< CAP REQ :twitch.tv/commands
> :tmi.twitch.tv CAP * ACK :twitch.tv/commands
```

Enables `USERSTATE`, `GLOBALUSERSTATE`, `ROOMSTATE`, `HOSTTARGET`, `NOTICE` and `CLEARCHAT` raw commands.

### NOTICE

General notices from the server - could be about state change (slowmode enabled), feedback (you have banned <user> from the channel), etc.  Each NOTICE message includes a msg-id tag which can be used for i18ln.

```
> @msg-id=slow_off :tmi.twitch.tv NOTICE #channel :This room is no longer in slow mode.
```

 msg-id | reponse
 ---|---
subs_on | This room is now in subscribers-only mode.
subs_off | This room is no longer in subscribers-only mode.
slow_on | This room is now in slow mode. You may send messages every `slow_duration` seconds.
slow_off | This room is no longer in slow mode.
r9k_on | This room is now in r9k mode.
r9k_off | This room is no longer in r9k mode.
host_on | Now hosting `target_channel`.
host_off | Exited host mode.

### HOSTTARGET

Host starts message:

```
> :tmi.twitch.tv HOSTTARGET #hosting_channel :target_channel [number]
```
Host stops message:

```
> :tmi.twitch.tv HOSTTARGET #hosting_channel :- [number]
```
Number is assumed to be the number of viewers watching the host.

### CLEARCHAT

Username is timed out on channel:

```
> :tmi.twitch.tv CLEARCHAT #channel :twitch_username
```
Chat is cleared on channel:

```
> :tmi.twitch.tv CLEARCHAT #channel
```
### USERSTATE

Use with tags CAP. See USERSTATE tags [below](#userstate-1).

```
> :tmi.twitch.tv USERSTATE #channel
```

### RECONNECT

Twitch IRC processes ocasionally need to be restarted. When this happens, clients that have requested the IRCv3 `twitch.tv/commands` capability are issued a `RECONNECT`. After a short period of time, the connection will be closed.
 
In this circumstance, please reconnect and rejoin channels that were on that connection as you would normally.

### ROOMSTATE

Use with tags CAP. See ROOMSTATE tags [below](#roomstate-1).

```
> :tmi.twitch.tv ROOMSTATE #channel
```
## Tags

```
< CAP REQ :twitch.tv/tags
> :tmi.twitch.tv CAP * ACK :twitch.tv/tags
```
Adds IRC v3 message tags to `PRIVMSG`, `USERSTATE`, `NOTICE` and `GLOBALUSERSTATE` (if enabled with commands CAP)

### PRIVMSG

Example message:

```
> @color=#0D4200;display-name=TWITCH_UserNaME;emotes=25:0-4,12-16/1902:6-10;mod=0;room-id=1337;subscriber=0;turbo=1;user-id=1337;user-type=global_mod :twitch_username!twitch_username@twitch_username.tmi.twitch.tv PRIVMSG #channel :Kappa Keepo Kappa
```

- `color` is a hexadecimal RGB color code
  - Empty if it's never been set.
- `display-name` is the user's display name, escaped [as described in the IRCv3 spec](http://ircv3.net/specs/core/message-tags-3.2.html).
  - Empty if it's never been set.
- `emotes` contains information to replace text in the message with the emote images and *can be empty*. The format is as follows:
  - `emote_id:first_index-last_index,another_first-another_last/another_emote_id:first_index-last_index`
  - `emote_id` is the number to use in this URL: `http://static-cdn.jtvnw.net/emoticons/v1/:emote_id/:size` (size is 1.0, 2.0 or 3.0)
  - Emote indexes are simply character indexes. `\001ACTION ` does *not* count and indexing starts from the first character that is part of the user's "actual message". In the example message, the first Kappa (emote id 25) is from character 0 (K) to character 4 (a), and the other Kappa is from 12 to 16.
- `mod`, `subscriber` and `turbo` are either 0 or 1 depending on whether the user has mod, sub or turbo badge or not.
- `room-id` is the ID of the channel.
- `user-id` is the user's ID.
- `user-type` is either *empty*, `mod`, `global_mod`, `admin` or `staff`.
  - The broadcaster can have any of these, including empty.

### USERSTATE

USERSTATE is sent when joining a channel and every time you send a PRIVMSG to a channel. Example:

```
> @color=#0D4200;display-name=TWITCH_UserNaME;emote-sets=0,33,50,237,793,2126,3517,4578,5569,9400,10337,12239;mod=1;subscriber=1;turbo=1;user-type=staff :tmi.twitch.tv USERSTATE #channel
```

- `emote-sets` contains your emote set, which you can use to request a subset of [`/chat/emoticon_images`](/v3_resources/chat.md#get-chatemoticon_images).
  - eg: `https://api.twitch.tv/kraken/chat/emoticon_images?emotesets=0,33,50,237,793,2126,3517,4578,5569,9400,10337,12239`
  - Always contains at least 0.
- Other tags are shared with PRIVMSG and function the same way.

### GLOBALUSERSTATE

GLOBALUSERSTATE is sent on successful login, if the capabilities have been acknowledged before then. Example:

```
@color=#0D4200;display-name=TWITCH_UserNaME;emote-sets=0,33,50,237,793,2126,3517,4578,5569,9400,10337,12239;turbo=0;user-id=1337;user-type=admin :tmi.twitch.tv GLOBALUSERSTATE
```

- All tags are shared with PRIVMSG or USERSTATE and function the same way.

### ROOMSTATE

ROOMSTATE is sent when joining a channel and every time one of the chat room settings, like slow mode, change. The message on join contains all room settings. Example:

```
> @broadcaster-lang=;r9k=0;slow=0;subs-only=0 :tmi.twitch.tv ROOMSTATE #channel
```

Changes only contain the relevant tag. Setting slow mode to 10 seconds for example:

```
> @slow=10 :tmi.twitch.tv ROOMSTATE #channel
```

- `broadcaster-lang` is the chat language when [broadcaster language mode](http://blog.twitch.tv/2015/07/broadcaster-language-mode/) is enabled, and empty otherwise. A few examples would be `en` for English, `fi` for Finnish and `es-MX` for Mexican variant of Spanish.
- `r9k` is R9K mode. Messages with more than 9 characters must be unique. `0` means disabled, `1` enabled.
- `subs-only` is subscribers only mode. Only subscribers and moderators can chat. `0` disabled, `1` enabled.
- `slow` determines how many seconds chatters without moderator privileges must wait between sending messages.
