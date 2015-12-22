# Embedding Twitch Live Streams & Videos


## Non-Interactive Iframe Embed
    <iframe 
        src="http://player.twitch.tv/?channel={CHANNEL}" 
        height="720" 
        width="1280" 
        frameborder="0" 
        scrolling="no"
        allowfullscreen="true">
    </iframe>
    
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

## Interactive Embed (Not Available Yet)
    <div id="{PLAYER_DIV_ID}"></div>
	<script type="text/javascript">
		var options = {
			width: 854,
			height: 480,
			channel: "{CHANNEL}", //video: "{VIDEO_ID}",
		};

		var player = new Twitch.embed.Player("{PLAYER_DIV_ID}", options);
		player.setCurrentTime(3000);
		
	</script>

Include *.js files??? TBD

### Embed Calls
All calls are synchronous. 

**pause()**

Pauses player

**play()**

Unpauses player

**setVideo(`videoid`)**

- `videoid`     : string of the video's id `"v25831761"`

**setChannel(`channelname`)**

- `channnelname`: string of the channel's name `"monstercat"`

**setCurrentTime(`timestamp`)**

Does not work for streams. Seeks to `timestamp` in video and plays.
- `timestamp`   : timestamp to seek to (in seconds) `2000`

**getCurrentTime()**

Does not work for streams. Returns current timestamp in seconds for video. `1230`

**getQuality()**

Returns current quality. `"Source"`

**getQualities()**

Returns available qualities. `["source","medium","low"]`

**getPaused()**

Returns the paused state of the player. `true` or `false`

### Events

TBD
