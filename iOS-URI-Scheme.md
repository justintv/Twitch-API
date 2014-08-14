## Overview

The TwitchTV iOS application can be launched externally. This page serves to document how to do so. For support or issue help, visit the [API Developers Group][] or [Github Issues][]

[API Developers Group]: https://groups.google.com/forum/?fromgroups#!forum/justintv-api-developers
[Github Issues]: /justintv/Twitch-API/issues

### URI Scheme
URLs starting with twitch:// or ttv:// will open up the Twitch iOS app, if the user has it installed. You can check if the Twitch app is installed with something along the following lines:

    NSURL *twitchURL = [NSURL URLWithString:@"twitch://open"];
    if ([[UIApplication sharedApplication] canOpenURL:twitchURL]) {
        // The Twitch app is installed, do whatever logic you need, and call -openURL:
    } else {
        // The Twitch app isn't installed, prompt the user to install it!
    }

### Opening up the App
If the only thing you want to do is launch the app, you should use the following:

    twitch://open

### Live Streams
To open the app up to a live stream, specify the name in the URL, eg:

    twitch://stream/hebo

This URI was first introduced in Twitch for iOS 2.0.
