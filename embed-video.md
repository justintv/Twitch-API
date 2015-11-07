# Embedding Twitch Live Streams & Videos

## Embed `<iframe>` Example
    <iframe 
        src="http://player.twitch.tv/?channel={CHANNEL}" 
        height="720" 
        width="1280" 
        frameborder="0" 
        scrolling="no" 
        allowfullscreen>
    </iframe>
    
## Parameters
**Either Required**
- `channel`   : Channel name for live streams. (ex. `twitch`)
- `video`     : Video ID for past broadcasts. Has no effect if `channel` is specified. (ex. `v123456`)

**Optional**
- `muted`     : Sets the initial muted state. `true` or `false`. Defaults to `false`.
- `autoplay`  : Automatically starts playing without the user clicking play. `true` or `false`. Defaults to `true`.
- `time`      : Start playback at the given timestamp for videos ONLY. Must be in the format `1h2m3s` specifying hours, minutes, and seconds respectively. Defaults to the start of the video.
