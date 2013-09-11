## Twitch Player API

We expose a Javascript API for our flash Twitch player that gives flexibility and functionality to embedding.

### Example code

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
  <head>
    <script src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js
"></script>
    <script>
      window.onPlayerLoad = function () {
        var player = document.getElementById("twitch_embed_player");
        player.playVideo();
        player.pauseVideo();
        player.mute();
        player.unmute();
      };
      swfobject.embedSWF("http://www-cdn.jtvnw.net/swflibs/TwitchPlayer.swf", "twitch_embed_player", "100%", "100%", "11", null, {"loadCallback":"onPlayerLoad","hostname":"www.twitch.tv","publisherGuard":null,"hide_chat":"true","publisherTimezoneOffset":-240,"channel":"chaoxlol","auto_play":"true"}, {"allowScriptAccess":"always","allowNetworking":"all","wmode":"opaque","allowFullScreen":"true"});
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
    </tbody>
</table>

