## Twitch Player API

We expose a Javascript API for our flash Twitch player that gives flexibility and functionality to embedding.

### Example code

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
  <head>
    <script src="//ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
    <script src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
    <script>
      $(function () {
        window.onPlayerLoad = function () {
          var player = $("#twitch_embed_player")[0];
          player.playVideo();
          player.mute();
        };
        swfobject.embedSWF("//www-cdn.jtvnw.net/swflibs/TwitchPlayer.swf", "twitch_embed_player", "640", "400", "11", null,
          { "initCallback":"onPlayerLoad",
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
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>playVideo</code></td>
            <td>If stream is online, will play the player.</td>
        </tr>
        <tr>
            <td><code>pauseVideo</code></td>
            <td>If stream is online, will pause the player.</td>
        </tr>
        <tr>
            <td><code>mute</code></td>
            <td>Mutes the player.</td>
        </tr>
        <tr>
            <td><code>unmute</code></td>
            <td>Unmutes the player.</td>
        </tr>
        <tr>
            <td><code>onlineStatus</code></td>
            <td>Returns the online status of the loaded stream. Values are <code>online</code>, <code>offline</code>, or <code>unknown</code>.</td>
        </tr>
        <tr>
            <td><code>loadStream</code></td>
            <td>Loads a given stream. Parameter is a string.</td>
        </tr>
        <tr>
            <td><code>loadVideo</code></td>
            <td>Loads a given video. Parameter is the video id.</td>
        </tr>
    </tbody>
</table>

