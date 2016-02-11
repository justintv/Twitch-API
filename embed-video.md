# Embedding Twitch Live Streams & Videos


## Non-Interactive Iframe Embed
```html
    <iframe 
        src="http://player.twitch.tv/?channel={CHANNEL}" 
        height="720" 
        width="1280" 
        frameborder="0" 
        scrolling="no"
        allowfullscreen="true">
    </iframe>
```

### Parameters
**Either Required**
- `channel`   : Channel name for live streams. (ex. `twitch`)
- `video`     : Video ID for past broadcasts. Has no effect if `channel` is specified. (ex. `v123456`)

**Optional**
- `muted`     : Sets the initial muted state. `true` or `false`. Defaults to `false`.
- `autoplay`  : Automatically starts playing without the user clicking play. `true` or `false`. Defaults to `true`.
- `time`      : Start playback at the given timestamp for videos ONLY. Must be in the format `1h2m3s` specifying hours, minutes, and seconds respectively. Defaults to the start of the video.

### Video and Channel Metadata
For video and channel metadata refer to the [Twitch API (Kraken)] (https://github.com/justintv/Twitch-API).
Info such as video channel, length, description, viewcounts are available through the Twitch API.

## Interactive Embed
```html
<script src= "http://player.twitch.tv/js/embed/v1.js"></script>
<div id="{PLAYER_DIV_ID}"></div>
<script type="text/javascript">
	var options = {
		width: 854,
		height: 480,
		channel: "{CHANNEL}", 
		//video: "{VIDEO_ID}"		}
	;
	var player = new Twitch.Player("{PLAYER_DIV_ID}", options);
	player.seek(3000);
</script>
```

### Options
- `width:Number`	: width of embed player in pixels
- `height:Number`	: height of embed player in pixels
- `channel:String`	: channel name for live streams `monstercat` 
- `video:String`	: video id for past broadcast `v40464143` 

Either a channel or a video can be loaded at one time.

### Embed Player Calls
All calls are synchronous.

#### Playback Controls
`pause():void`

Pauses player

`play():void`

Begins playing specified content.

`setVideo(videoid:String):void` 

- `videoid`     : video id (e.g. `"v1234567890"`)

`setChannel(channelname:String):void`

- `channelname`: channel name 

`seek(timestamp:Float):void`

Does not work for live streams. Seeks to `timestamp` in video and resumes playing, if paused.
- `timestamp`   : timestamp to seek to (in seconds)

`setQuality(quality:String):void`

There are 5 available qualities: `"Source"`, `"High"`, `"Medium"`, `"Low"`, `"Mobile"`.
Quality will default to `"Source"`if there are no transcodes available for the video.
- `quality`: quality wanted (e.g. `"High"`) 

#### Volume Controls

`setVolume(volumelevel:Float):void`

- `volumelevel`: volume level between 0.0 and 1.0

`setMuted(muted:Boolean):void`

- `muted`: `true` mutes the player independent of volume setting, `false` unmutes

`getVolume():Float`

Returns volume level, between 0.0 and 1.0

`getMuted():Boolean`

Returns `true` if muted, else `false`

#### Player Status
`getEnded():Boolean`

Returns `true` if stream or video has ended, else `false`

`getDuration():Float`

Does not work for live streams. Returns duration of video in seconds.

`getCurrentTime():Float`

Does not work for live streams. Returns current timestamp in seconds for video.

`getQuality():String`

Returns current quality of playback. (e.g. `"Source"`)

`getQualities():String[]`

Returns available qualities. (e.g. `["Source", "High", "Medium", "Low", "Mobile"]` or `["Source"]`)

`isPaused():Boolean`

Returns `true` if paused, else `false`. Buffering or seeking is considered playing.

`getChannel():String`

Doesn't work for videos. Returns the channel's name.

`getVideo():String`

Doesn't work for channels. Returns the video's id.

`getPlaybackStats():Object`

Returns an `Object` with the stats on the player and the current video or live stream.

#### Event Handling

`addEventListener(event:String, callback:Function)`

- `event`     : the event to listen to `"pause"`
- `callback`  : function to call when `event` is triggered `function() { console.log("Event fired"); }`

`removeEventListener(event:String, callback:Function)`

- `event`     : the `event` the `callback` is associated with
- `callback`  : the function to remove 


### Events
Events emitted by player. Call `addEventListener(event:String, callback:Function)` to listen to events.

- `"play"`   : Emitted when player is playing.
- `"pause"`  : Emitted when player is paused. Buffering and seeking is not considered paused.
- `"ended"`  : Emitted when video or stream ends.
- `"online"` : Emitted when loaded channel goes online.
- `"offline"`: Emitted when loaded channel goes offline.


