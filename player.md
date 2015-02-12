## Twitch Player API

We expose a JavaScript API for our Flash Twitch player that gives flexibility and functionality to embedding. The IFrame embed does not yet have an external interface.

### Example code

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
  <head>
    <script src="//ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
    <script src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
    <script>
      $(function () {
        window.onPlayerEvent = function (data) {
          data.forEach(function(event) {
            if (event.event == "playerInit") {
              var player = $("#twitch_embed_player")[0];
              player.playVideo();
              player.mute();
            }
          });
        }
        
        swfobject.embedSWF("//www-cdn.jtvnw.net/swflibs/TwitchPlayer.swf", "twitch_embed_player", "640", "400", "11", null,
          { "eventsCallback":"onPlayerEvent",
            "embed":1,
            "channel":"day9tv",
            "auto_play":"true"},
          { "allowScriptAccess":"always",
            "allowFullScreen":"true"});
      });
    </script>
  </head>
  <body>
    <div id="twitch_embed_player">
    </div>
  </body>
</html>
```

### Functions

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th width="100%">Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>isPaused</code></td>
            <td>Gets the playing status of the video. Returns boolean <code>true</code> or <code>false</code></td>
        </tr>
        <tr>
            <td><code>loadStream</code></td>
            <td>Loads a given stream. Parameter is a channel name (as a String).</td>
        </tr>
        <tr>
            <td><code>loadVideo</code></td>
            <td>Loads a given video. Parameter is the video ID (as a String).</td>
        </tr>
        <tr>
            <td><code>mute</code></td>
            <td>Mutes the player.</td>
        </tr>
        <tr>
            <td><code>onlineStatus</code></td>
            <td>Returns the online status of the loaded stream. Values returned are <code>online</code>, <code>offline</code>, or <code>unknown</code>.</td>
        </tr>
        <tr>
            <td><code>pauseVideo</code></td>
            <td>If stream is online, will pause the player.</td>
        </tr>
        <tr>
            <td><code>playVideo</code></td>
            <td>If stream is online, will play the player.</td>
        </tr>
        <tr>
            <td><code>videoSeek</code></td>
            <td>Seeks a video. Parameter is seconds (as a Number)</td>
        </tr>
        <tr>
            <td><code>unmute</code></td>
            <td>Unmutes the player.</td>
        </tr>
    </tbody>
</table>

### Events

Events are emitted through the eventsCallback Flash player parameter in the following form:

```json
[
  {
    "event": "",
    "data": {}
  },
  ...
]
```

<table>
    <thead>
        <tr>
            <th width="25%">Event</th>
            <th width="50%">Description</th>
            <th width="25%">Data</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>streamLoaded</code></td>
            <td>Emitted when a stream is loaded in the video player</td>
            <td>
<pre>{
  channel: "test_stream",
  channelSteamId: null,
  videoId: null,
  videoLengthInSecs: 0,
  viewerSteamId: null
}</pre>
            </td>
        </tr>
        <tr>
            <td><code>videoLoaded</code></td>
            <td>Emitted when a video is loaded in the video player</td>
            <td>
<pre>{
  channel: "test_stream",
  channelSteamId: null,
  videoId: "4345634",
  videoLengthInSecs: 15,
  viewerSteamId: null
}</pre>
            </td>
        </tr>
        <tr>
            <td><code>online</code></td>
            <td>Emitted when the stream is online (emitted on stream load too)</td>
            <td><pre>{}</pre></td>
        </tr>
        <tr>
            <td><code>offline</code></td>
            <td>Emitted when the stream goes offline</td>
            <td><pre>{}</pre></td>
        </tr>
        <tr>
            <td><code>viewerCount</code></td>
            <td>The viewer count is emitted periodically for streams</td>
            <td>
<pre>{
  channel: "test_stream",
  viewers: 12975
}</pre>
            </td>
        </tr>
        <tr>
            <td><code>videoLoading</code></td>
            <td>Emitted when a stream or video is loading</td>
            <td><pre>{}</pre></td>
        </tr>
        <tr>
            <td><code>playerInit</code></td>
            <td>Emitted when the player is loaded</td>
            <td><pre>{}</pre></td>
        </tr>
        <tr>
            <td><code>videoPlaying</code></td>
            <td>Emitted when a stream or video starts playing</td>
            <td><pre>{}</pre></td>
        </tr>
        <tr>
            <td><code>mouseScroll</code></td>
            <td>Emitted when the user scrolls over the video</td>
            <td>
<pre>{
  delta: 1
}</pre>
            </td>
        </tr>
    </tbody>
</table>
