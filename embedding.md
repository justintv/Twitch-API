## Embedding Streams, Videos, and Chat

Here are the embed codes and parameters you might need to integrate streams, videos, or chat onto your site.

### Streams

#### Parameters
- `height`  : Player height. Default is 378.
- `width`   : Player width. Default is 620.
- `channel` : Channel to show.
- `volume`  : Player volume ranging from 0 to 50. Default is 25.

#### Code

```html
<object type="application/x-shockwave-flash" 
        height="{HEIGHT}" 
        width="{WIDTH}" 
        id="live_embed_player_flash" 
        data="http://www.twitch.tv/widgets/live_embed_player.swf?channel={CHANNEL}" 
        bgcolor="#000000">
  <param  name="allowFullScreen" 
          value="true" />
  <param  name="allowScriptAccess" 
          value="always" />
  <param  name="allowNetworking" 
          value="all" />
  <param  name="movie" 
          value="http://www.twitch.tv/widgets/live_embed_player.swf" />
  <param  name="flashvars" 
          value="hostname=www.twitch.tv&channel={CHANNEL}&auto_play=true&start_volume={VOLUME}" />
</object>
```

#### Example

```html
<object type="application/x-shockwave-flash" height="378" width="620" id="live_embed_player_flash" data="http://www.twitch.tv/widgets/live_embed_player.swf?channel=hebo" bgcolor="#000000"><param name="allowFullScreen" value="true" /><param name="allowScriptAccess" value="always" /><param name="allowNetworking" value="all" /><param name="movie" value="http://www.twitch.tv/widgets/live_embed_player.swf" /><param name="flashvars" value="hostname=www.twitch.tv&channel=hebo&auto_play=true&start_volume=25" /></object>
```

### HTML5 Streams Player

#### Parameters
- `height`  : Player height. Default is 378.
- `width`   : Player width. Default is 620.
- `channel` : Channel to show.

#### Code

```html
<iframe id="player" type="text/html" width="620" height="378"
  src="http://www.twitch.tv/{CHANNEL}/hls"
  frameborder="0"></iframe>
```

### Videos

#### Parameters
- `height`  : Player height. Default is 300.
- `width`   : Player width. Default is 400.
- `channel` : Channel that video belongs to.
- `chapter_id` : Chapter ID of the video.
- `volume`  : Player volume ranging from 0 to 50. Default is 25.

#### Code

```html
<object bgcolor='#000000' 
        data='http://www.twitch.tv/widgets/archive_embed_player.swf' 
        height='{HEIGHT}' 
        id='clip_embed_player_flash' 
        type='application/x-shockwave-flash' 
        width='{WIDTH}'> 
  <param  name='movie' 
          value='http://www.twitch.tv/widgets/archive_embed_player.swf' /> 
  <param  name='allowScriptAccess' 
          value='always' /> 
  <param  name='allowNetworking' 
          value='all' /> 
  <param  name='allowFullScreen' 
          value='true' /> 
  <param  name='flashvars' 
          value='channel={CHANNEL}&start_volume={VOLUME}&auto_play=false&chapter_id={CHAPTER_ID}' />
</object>
```

#### Example

```html
<object bgcolor='#000000' data='http://www.twitch.tv/widgets/archive_embed_player.swf' height='378' id='clip_embed_player_flash' type='application/x-shockwave-flash' width='620'><param name='movie' value='http://www.twitch.tv/widgets/archive_embed_player.swf' /><param name='allowScriptAccess' value='always' /><param name='allowNetworking' value='all' /><param name='allowFullScreen' value='true' /><param name='flashvars' value='channel=tsm_chaox&start_volume=25&auto_play=false&chapter_id=1353487' /></object>
```

### Chat

#### Parameters
- `height`  : Chat window height. Default is 500.
- `width`   : Chat window width. Default is 350.
- `channel` : Channel the chat belongs to.

#### Code

```html
<iframe frameborder="0" 
        scrolling="no" 
        id="chat_embed" 
        src="http://twitch.tv/chat/embed?channel={CHANNEL}&amp;popout_chat=true" 
        height="{HEIGHT}" 
        width="{WIDTH}">
</iframe>
```

#### Example

```html
<iframe frameborder="0" scrolling="no" id="chat_embed" src="http://twitch.tv/chat/embed?channel=hebo&amp;popout_chat=true" height="500" width="350"></iframe>
```
