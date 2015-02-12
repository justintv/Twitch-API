## Embedding Streams, Videos, and Chat

Here are the embed codes and parameters you might need to integrate streams, videos, or chat onto your site.

### Streams

#### Parameters
- `auto_play` : Boolean value for playing the video on player load.
- `channel`   : Channel to show.
- `height`    : Player height.
- `volume`    : Player volume ranging from 0 to 50. Default is 25.
- `width`     : Player width.

#### Code

```html
<object bgcolor="#000000" 
        data="//www-cdn.jtvnw.net/swflibs/TwitchPlayer.swf" 
        height="{HEIGHT}" 
        type="application/x-shockwave-flash" 
        width="{WIDTH}" 
        > 
  <param name="allowFullScreen" 
          value="true" />
  <param name="allowNetworking" 
          value="all" />
  <param name="allowScriptAccess" 
          value="always" />
  <param name="movie" 
          value="//www-cdn.jtvnw.net/swflibs/TwitchPlayer.swf" />
  <param name="flashvars" 
          value="channel={CHANNEL}&auto_play={AUTO_PLAY}&start_volume={VOLUME}" />
</object>
```

#### Example

```html
<object type="application/x-shockwave-flash" height="378" width="620" data="//www-cdn.jtvnw.net/swflibs/TwitchPlayer.swf" bgcolor="#000000"><param name="allowFullScreen" value="true" /><param name="allowScriptAccess" value="always" /><param name="allowNetworking" value="all" /><param name="movie" value="//www-cdn.jtvnw.net/swflibs/TwitchPlayer.swf" /><param name="flashvars" value="channel=hebo&auto_play=true&start_volume=25" /></object>
```

#### Player API

Our Flash Twitch player also exposes a JavaScript API. Read the [Twitch Player API][] for documentation.

### IFrame Streams Player

#### Parameters
- `channel` : Channel to show.
- `height`  : Player height.
- `width`   : Player width.

#### Code

```html
<iframe id="player" type="text/html" width="{WIDTH}" height="{HEIGHT}"
  src="http://www.twitch.tv/{CHANNEL}/embed"
  frameborder="0"></iframe>
```

### Videos

#### Parameters
- `auto_play`    : Boolean value for playing the video on player load.
- `channel`      : Channel the video belongs to.
- `height`       : Player height.
- `initial_time` : Start time in seconds.
- `video_id`     : ID of the video.
- `volume`       : Player volume ranging from 0 to 50. Default is 25.
- `width`        : Player width.

#### Code

```html
<object bgcolor='#000000' 
        data='//www-cdn.jtvnw.net/swflibs/TwitchPlayer.swf' 
        height='{HEIGHT}' 
        type='application/x-shockwave-flash' 
        width='{WIDTH}'> 
  <param name="allowFullScreen" 
          value="true" />
  <param name="allowNetworking" 
          value="all" />
  <param name="allowScriptAccess" 
          value="always" />
  <param name='movie' 
          value='//www-cdn.jtvnw.net/swflibs/TwitchPlayer.swf' /> 
  <param name='flashvars' 
          value='channel={CHANNEL}&start_volume={VOLUME}&auto_play={AUTO_PLAY}&videoId={VIDEO_ID}&initial_time={INITIAL_TIME}' />
</object>
```

#### Example

```html
<object bgcolor='#000000' data='//www-cdn.jtvnw.net/swflibs/TwitchPlayer.swf' height='378' id='clip_embed_player_flash' type='application/x-shockwave-flash' width='620'><param name='movie' value='//www-cdn.jtvnw.net/swflibs/TwitchPlayer.swf' /><param name='allowScriptAccess' value='always' /><param name='allowNetworking' value='all' /><param name='allowFullScreen' value='true' /><param name='flashvars' value='channel=chaoxlol&start_volume=25&auto_play=true&videoId=c1353487&initial_time=0' /></object>
```

#### Player API

Our Flash Twitch player also exposes a JavaScript API. Read the [Twitch Player API][] for documentation.

### Chat

#### Parameters
- `channel` : Channel the chat belongs to.
- `height`  : Chat window height.
- `width`   : Chat window width.

#### Code

```html
<iframe frameborder="0" 
        scrolling="no" 
        id="chat_embed" 
        src="http://www.twitch.tv/{CHANNEL}/chat" 
        height="{HEIGHT}" 
        width="{WIDTH}">
</iframe>
```

#### Example

```html
<iframe frameborder="0" scrolling="no" id="chat_embed" src="http://www.twitch.tv/hebo/chat" height="500" width="350"></iframe>
```

[Twitch Player API]: player.md