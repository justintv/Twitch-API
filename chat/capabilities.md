Twitch Capabilities
===================

Using IRCv3 capability registration, it is possible to register for Twitch-specific
capabilities. The capabilities are defined below:

## Membership

    < CAP REQ :twitch.tv/membership
    > :tmi.twitch.tv CAP * ACK :twitch.tv/membership

Adds JOIN and PART functionality.  When we remove support for the TWITCHCLIENT command, we will by default *not* send this data to clients without this capability.

## Commands

    < CAP REQ :twitch.tv/commands
    > :tmi.twitch.tv CAP * ACK :twitch.tv/commands

Enables `USERSTATE`, `GLOBALUSERSTATE`, `HOSTTARGET`, `NOTICE` and `CLEARCHAT` raw commands.

### NOTICE

General notices from the server - could be about state change (slowmode enabled), feedback (you have banned <user> from the channel), etc.  Each NOTICE message includes a msg-id tag which can be used for i18ln.

    @msg-id=slow_off :tmi.twitch.tv NOTICE #channel :This room is no longer in slow mode.

### HOSTTARGET

Host starts message:

    :tmi.twitch.tv HOSTTARGET #hosting_channel :target_channel [number]

Host stops message:

    :tmi.twitch.tv HOSTTARGET #hosting_channel :- [number]

Number is assumed to be the number of viewers watching the host.

### CLEARCHAT

Username is timed out on channel:

    :tmi.twitch.tv CLEARCHAT #channel :username

Chat is cleared on channel:

    :tmi.twitch.tv CLEARCHAT #channel

### USERSTATE

Use with tags CAP to get anything out of it. See USERSTATE tags below as it doesn't offer anything without them.

    :tmi.twitch.tv USERSTATE #notventic

## Tags

    < CAP REQ :twitch.tv/tags
    > :tmi.twitch.tv CAP * ACK :twitch.tv/tags

Adds IRC v3 message tags to `PRIVMSG` and `USERSTATE` (if enabled with commands CAP)

### PRIVMSG

Example message:

    @color=#1E0ACC;display-name=3ventic;emotes=25:0-4,12-16/1902:6-10;subscriber=0;turbo=1;user-type=mod;user_type=mod :3ventic!3ventic@3ventic.tmi.twitch.tv PRIVMSG #gophergaming :Kappa Keepo Kappa

- `color` is hexadecimal RGB color code, which *can be empty* if the user never set it.
- `display-name` is the user's display name, escaped as described [as described in the IRCv3 spec](http://ircv3.net/specs/core/message-tags-3.2.html). Empty if it's never been set.
- `emotes` contains information to replace text in the message with the emote images and *can be empty*. The format is as follows:
  - `emote_id:first_index-last_index,another_first-another_last/another_emote_id:first_index-last_index`
  - `emote_id` is the number to use in this URL: `http://static-cdn.jtvnw.net/emoticons/v1/:emote_id/:size` (size is 1.0, 2.0 or 3.0)
  - Emote indexes are simply character indexes. `\001ACTION ` does *not* count and indexing starts from the first character that is part of the user's "actual message". In the example message, the first Kappa (emote id 25) is from character 0 (K) to character 4 (a), and the other Kappa is from 12 to 16.
- `subscriber`and `turbo` are either 0 or 1 depending on whether the user has sub or turbo badge or not.
- `user-type` is either *empty*, `mod`, `global_mod`, `admin` or `staff`. The broadcaster can have any of these.
- `user_type` is deprecated and will be removed soon. Use `user-type` instead.

### USERSTATE

USERSTATE is sent when joining a channel and every time you send a PRIVMSG to a channel. Example:

    @color=#1E0ACC;display-name=3ventic;emote-sets=0,12239,2126,237,33,366,4578,469,793,9400;emotesets=0,12239,2126,237,33,366,4578,469,793,9400;subscriber=0;turbo=1;user-type=mod;user_type=mod :tmi.twitch.tv USERSTATE #gophergaming

The tags shared with PRIVMSG work exactly the same.

`emote-sets` contains your emote set, which you can use to request `https://api.twitch.tv/kraken/chat/emoticon_images?emotesets=[straight from the emote-sets tag]`. Always contains at least 0.

`emotesets` is deprecated and will be removed soon. Use `emote-sets` instead.

### USERSTATE

GLOBALUSERSTATE will be used in the future to describe non-channel-specific state information.
