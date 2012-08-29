## Why?

Because it is a good idea! The old API was built to satisfy a different set of requirements than those that we have now on Twitch. On top of that some bad decisions were made, so instead of trying to work out a migration plan we thought it better to build it from the ground up with all of the learning we gained from the last pass. The list of key improvements:
* Super RESTful
* Self describing (as [detailed](http://stdout.heyzap.com/2012/03/07/how-to-write-a-self-documenting-api/) by our buddy [@Immad](https://twitter.com/immad) over at [Heyzap](http://www.heyzap.com/))
* Versioned (i.e. we can now provide backwards compatibility)