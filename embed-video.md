# Embedding Twitch Live Streams & Videos


## Non-Interactive Embed `<iframe>` Example
    <iframe 
        src="http://player.twitch.tv/?channel={CHANNEL}" 
        height="720" 
        width="1280" 
        frameborder="0" 
        scrolling="no" 
    </iframe>
    
###Parameters
**Either Required**
- `channel`   : Channel name for live streams. (ex. `twitch`)
- `video`     : Video ID for past broadcasts. Has no effect if `channel` is specified. (ex. `v123456`)

**Optional**
- `muted`     : Sets the initial muted state. `true` or `false`. Defaults to `false`.
- `autoplay`  : Automatically starts playing without the user clicking play. `true` or `false`. Defaults to `true`.
- `time`      : Start playback at the given timestamp for videos ONLY. Must be in the format `1h2m3s` specifying hours, minutes, and seconds respectively. Defaults to the start of the video.

###Video and Channel Metadata
For video and channel metadata please refer to the [Twitch API] (https://github.com/justintv/Twitch-API).
Metadata is listed below for convenience. All are available by [`GET/videos/:id`] (https://github.com/justintv/Twitch-API/blob/master/v3_resources/videos.md#get-videosid). 
- Video length
- Video title
- Video description
- Video viewcounts


##Interactive Embed Example (Not Available Yet)
    <div id="video-playback"></div>
	<script type="text/javascript">
		var options = {
			width: 854,
			height: 480,
			channel: "{CHANNEL}", //video: "{VIDEO_ID}",
		};

		var player = new Twitch.embed.Player("video-playback", options);
		player.setCurrentTime(3000);
	</script>
	
###Player Calls
####setVideo(`videoid`)
- `videoid`     : string of the video's id `"v25831761"`

####setChannel(`channelname`)
- `channnelname`: string of the channel's name `"monstercat"`

####setCurrentTime(`timestamp`)
- `timestamp`   : timestamp to seek to (in seconds) `2000`

####getCurrentTime()
Returns current timestamp in seconds `1234`
####getQuality()
Returns current quality `"Source"`
####getQualities()
Returns available qualities `["source","medium","low"]`
####getPaused()
Returns the paused state `true` or `false`


