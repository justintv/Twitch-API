## Overview

The TwitchTV iOS application can be launched externally. This page serves to document how to do so. For support or issue help, visit the [API Developers Group][] or [Github Issues][]

### URI Scheme
URLs starting with twitch:// or ttv:// will open up the Twitch iOS app, if the user has it installed. You can check if the Twitch app is installed with something along the following lines:

    NSURL *twitchURL = [NSURL URLWithString:@"twitch://open"];
    [[UIApplication sharedApplication] canOpenURL:twitchURL];

### Opening up the App
If the only thing you want to do is launch the app, you should use the following:

    twitch://open

### Live Streams
To open the app up to a live stream, specify the name in the URL, eg:

    twitch://stream/hebo

This URI was first introduced in Twitch for iOS 2.0.

### Games
To open the app up to a list of games, specify the game name as a a percent-encoded string in the URI, eg:

    twitch://game/Minecraft
    twitch://game/Starcraft%20II%3a%20Wings%20of%20Liberty

This URI was first introduced in Twitch for iOS 2.0.6.

### Searching
To open the app up to a specific search query, specify the query name as a a percent-encoded string in the URI, eg:
 
    twitch://search/Minecraft
    twitch://search/Starcraft%20II%3a%20Wings%20of%20Liberty

This URI was first introduced in Twitch for iOS 2.1.1.
