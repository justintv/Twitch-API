## Why?

Because it is a good idea! The old API was built to satisfy a different set of requirements than those that we have now on Twitch. On top of that some bad decisions were made, so instead of trying to work out a migration plan we thought it better to build it from the ground up with all of the learning we gained from the last pass. The list of key improvements:

* Super RESTful
* Self describing - as [detailed](http://stdout.heyzap.com/2012/03/07/how-to-write-a-self-documenting-api/) by our buddy [@Immad](https://twitter.com/immad) over at [Heyzap](http://www.heyzap.com/)
* Versioned - i.e. we can now provide backwards compatibility
* OAuth2 - so much easier to get right than OAuth1!
* Secured by scopes - fine grained access to certain properties
* Consistent

The last point, consistency, requires more details. Historically we had absolutely no rhyme or reason as to what we returned to users, our thought process was to return _exactly_ what you needed, however that was not scalable and made client side code so much more complex than it needed to be. Now if we say you'll get a User object back, you'll get a User object back regardless of which part of the API you're using.

Finally, this API has a full integration suite, so should we change our objects - we know.

## How do I get support?

Right now as we ramp up the support infrastructure of this new API your best bet is going to be making sure you read this wiki, for questions you can use the [Twitch API mailing list](https://groups.google.com/forum/?fromgroups#!forum/twitch-api).

## Migration guide

If you're working on a front end, you probably just want to use our [JavaScript library](https://github.com/justintv/twitch-js-sdk) - it gives you super easy access to all of the features as well as letting you make use of Twitch Connect, which lets you link your user accounts to twitch user accounts and grants you the ability to use the API as those users. 

Srsly, you probably just want to use the [JS library](https://github.com/justintv/twitch-js-sdk) :)

... However if you use a backend to make queries for you, or if have a browser extension, etc, you probably want to know which old calls map to which new calls. This list will evolve, and if you want something added to it let us know on the [Twitch API mailing list](https://groups.google.com/forum/?fromgroups#!forum/twitch-api) or open up an [issue on this repo](https://github.com/justintv/Twitch-API/issues).

### listing streams
old: http://apiwiki.justin.tv/mediawiki/index.php/Stream/list

new: https://github.com/justintv/Twitch-API/wiki/Streams-Resource#wiki-streams

### summary
old: http://apiwiki.justin.tv/mediawiki/index.php/Stream/summary

new: https://github.com/justintv/Twitch-API/wiki/Streams-Resource#wiki-summary

### search
old: http://apiwiki.justin.tv/mediawiki/index.php/Stream/search

new: https://github.com/justintv/Twitch-API/wiki/Search-Resource

### user data
old: http://apiwiki.justin.tv/mediawiki/index.php/User/show

new: https://github.com/justintv/Twitch-API/wiki/Users-Resource

### channel data
old: http://apiwiki.justin.tv/mediawiki/index.php/Channel/show

new: https://github.com/justintv/Twitch-API/wiki/Channels-Resource

### archive data
old: http://apiwiki.justin.tv/mediawiki/index.php/Channel/archives

new: https://github.com/justintv/Twitch-API/wiki/Videos-Resource


## Some things are missing!

Yes, this is true. Some things will not have a like for like implementation, some things will be dropped, some others will be worked on. The old API broadly broke down into some key categories;

 - the REST API
 - the chat embed
 - the SWF API

So far we have concentrated primarily on the REST API. We are also building a brand spanking new chat API to replace the embed - we want you to be able to use chat as a first class citizen, not through some proxy that we control. We're also planning to build a brand new SWF integration, if you want to use our SWF player you should use our existing one, however it is tied into the old API so I warn you now... your mileage will definitely vary and we'll not be well suited to helping you a whole bunch. 

Below we detail all of the things that will stay gone, if you've any issues with this list then [you are encouraged to let us know why it is a bad idea](https://groups.google.com/forum/?fromgroups#!forum/twitch-api).

### things that will stay missing from the REST API
 - stream callbacks
 - listing user events
 - channel creation
 - channel events
 - chat send message (will be replaced by the new chat API)
 - category listing (Twitch only has one category - GAMES!)