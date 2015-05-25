## Overview

The Twitch iOS and Android applications can be launched externally. This page serves to document how to do so. For support, visit the [Twitch Developer Forums][].

[Twitch Developer Forums]: http://discuss.dev.twitch.tv

### Checking for the presense of the app
You can check if the Twitch app is installed on the device with something along the following lines:

##### iOS
    NSURL *twitchURL = [NSURL URLWithString:@"twitch://open"];
    if ([[UIApplication sharedApplication] canOpenURL:twitchURL]) {
        // The Twitch app is installed, do whatever logic you need, and call -openURL:
    } else {
        // The Twitch app isn't installed, prompt the user to install it!
    }
    
##### Android
    // Where 'packagename' is the package name of the Twitch app:
    
    private boolean isPackageInstalled(String packagename, Context context) {
        PackageManager pm = context.getPackageManager();
        try {
            pm.getPackageInfo(packagename, PackageManager.GET_ACTIVITIES);
            return true;
        } catch (NameNotFoundException e) {
            return false;
        }
    }
    
### URL Scheme
URLs starting with twitch:// or ttv:// will open up the Twitch app, if it's installed on the device. 

##### Launch the App and optionally go to a live stream, a game's directory, or a VOD:

    twitch://open
    twitch://open?stream=#channel_name
    twitch://open?game=#game_name
    twitch://open?video=#video_id

##### Launch the app and go to the user's following directory (if user is not logged in, goes to the login page):

    twitch://following

##### Launch the app and go to the login page:

    twitch://login
