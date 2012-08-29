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