# Videos

***

Videos are broadcasts or highlights owned by a [channel][channels]. Broadcasts are unedited videos that are saved after a streaming session. Highlights are videos edited from broadcasts by the channel's owner.

| Endpoint | Description |
| ---- | --------------- |
| [GET /videos/:id](/v2_resources/videos.md#get-videosid) | Get video object|
| [GET /videos/top](/v2_resources/videos.md#get-videostop) | Get top videos by number of views |
| [GET /channels/:channel/videos](/v2_resources/videos.md#get-channelschannelvideos) | Get list of video objects belonging to channel |

[channels]: /v2_resources/channels.md

## `GET /videos/:id`

Returns a video object.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v2+json' \
-X GET https://api.twitch.tv/kraken/videos/c6055863
```

### Example Response

```json
{
  "title": "Twitch Weekly - February 6, 2015",
  "description": "Twitch Weekly LIVE on February 6, 2015!",
  "broadcast_id": 13019796368,
  "status": "recorded",
  "_id": "c6055863",
  "recorded_at": "2015-02-06T21:01:09Z",
  "game": null,
  "length": 4015,
  "preview": "http://static-cdn.jtvnw.net/jtv.thumbs/archive-621292653-320x240.jpg",
  "url": "http://www.twitch.tv/twitch/c/6055863",
  "embed": "<object bgcolor='#000000' data='http://www.twitch.tv/swflibs/TwitchPlayer.swf' height='300' id='clip_embed_player_flash' type='application/x-shockwave-flash' width='400'>\n<param name='movie' value='http://www.twitch.tv/swflibs/TwitchPlayer.swf' />\n<param name='allowScriptAccess' value='always' />\n<param name='allowNetworking' value='all' />\n<param name='allowFullScreen' value='true' />\n<param name='flashvars' value='title=Twitch%2BWeekly%2B-%2BFebruary%2B6%252C%2B2015&amp;channel=twitch&amp;auto_play=false&amp;start_volume=25&amp;videoId=c6055863' />\n</object>\n",
  "views": 318,
  "broadcast_type": "highlight",
  "_links": {
    "self": "https://api.twitch.tv/kraken/videos/c6055863",
    "channel": "https://api.twitch.tv/kraken/channels/twitch"
  },
  "channel": {
    "name": "twitch",
    "display_name": "Twitch"
  }
}
```

## `GET /videos/top`

Returns a list of videos created in a given time period sorted by number of views, most popular first.

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>limit</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Maximum number of objects in array. Default is 10. Maximum is 100.</td>
        </tr>
        <tr>
            <td><code>offset</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Object offset for pagination. Default is 0.</td>
        </tr>
        <tr>
            <td><code>game</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Returns only videos from <code>game</code>.</td>
        </tr>
        <tr>
            <td><code>period</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Returns only videos created in time period. Valid values are <code>week</code>, <code>month</code>, or <code>all</code>. Default is <code>week</code>.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v2+json' \
-X GET https://api.twitch.tv/kraken/videos/top?game=Gaming+Talk+Shows&period=month
```

### Example Response

```json
{
  "_links": {
    "next": "https://api.twitch.tv/kraken/videos/top?game=Gaming+Talk+Shows&limit=10&offset=10&period=month",
    "self": "https://api.twitch.tv/kraken/videos/top?game=Gaming+Talk+Shows&limit=10&offset=0&period=month"
  },
  "videos": [
    {
      "title": "Twitch Weekly - February 6, 2015",
      "description": "Twitch Weekly LIVE on February 6, 2015!",
      "broadcast_id": 13019796368,
      "status": "recorded",
      "_id": "c6055863",
      "recorded_at": "2015-02-06T21:01:09Z",
      "game": "Gaming Talk Shows",
      "length": 4015,
      "preview": "http://static-cdn.jtvnw.net/jtv.thumbs/archive-621292653-320x240.jpg",
      "url": "http://www.twitch.tv/twitch/c/6055863",
      "embed": "<object bgcolor='#000000' data='http://www.twitch.tv/swflibs/TwitchPlayer.swf' height='300' id='clip_embed_player_flash' type='application/x-shockwave-flash' width='400'>\n<param name='movie' value='http://www.twitch.tv/swflibs/TwitchPlayer.swf' />\n<param name='allowScriptAccess' value='always' />\n<param name='allowNetworking' value='all' />\n<param name='allowFullScreen' value='true' />\n<param name='flashvars' value='title=Twitch%2BWeekly%2B-%2BFebruary%2B6%252C%2B2015&amp;channel=twitch&amp;auto_play=false&amp;start_volume=25&amp;videoId=c6055863' />\n</object>\n",
      "views": 318,
      "broadcast_type": "highlight",
      "_links": {
        "self": "https://api.twitch.tv/kraken/videos/c6055863",
        "channel": "https://api.twitch.tv/kraken/channels/twitch"
      },
      "channel": {
        "name": "twitch",
        "display_name": "Twitch"
      }
    }
    ...
  ]
}
```

## `GET /channels/:channel/videos`

Returns a list of videos ordered by time of creation, starting with the most recent from `:channel`.

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>limit</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Maximum number of objects in array. Default is 10. Maximum is 100.</td>
        </tr>
        <tr>
            <td><code>offset</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Object offset for pagination. Default is 0.</td>
        </tr>
        <tr>
            <td><code>broadcasts</code></td>
            <td>optional</td>
            <td>bool</td>
            <td>Returns only broadcasts when <code>true</code>. Otherwise only highlights are returned. Default is <code>false</code>.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v2+json' \
-X GET https://api.twitch.tv/kraken/channels/twitch/videos?limit=10
```

### Example Response

```json
{
  "_total": 179,
  "videos": [
    {
      "title": "Twitch Weekly - February 6, 2015",
      "description": "Twitch Weekly LIVE on February 6, 2015!",
      "broadcast_id": 13019796368,
      "status": "recorded",
      "_id": "c6055863",
      "recorded_at": "2015-02-06T21:01:09Z",
      "game": null,
      "length": 4015,
      "preview": "http://static-cdn.jtvnw.net/jtv.thumbs/archive-621292653-320x240.jpg",
      "url": "http://www.twitch.tv/twitch/c/6055863",
      "embed": "<object bgcolor='#000000' data='http://www.twitch.tv/swflibs/TwitchPlayer.swf' height='300' id='clip_embed_player_flash' type='application/x-shockwave-flash' width='400'>\n<param name='movie' value='http://www.twitch.tv/swflibs/TwitchPlayer.swf' />\n<param name='allowScriptAccess' value='always' />\n<param name='allowNetworking' value='all' />\n<param name='allowFullScreen' value='true' />\n<param name='flashvars' value='title=Twitch%2BWeekly%2B-%2BFebruary%2B6%252C%2B2015&amp;channel=twitch&amp;auto_play=false&amp;start_volume=25&amp;videoId=c6055863' />\n</object>\n",
      "views": 318,
      "broadcast_type": "highlight",
      "_links": {
        "self": "https://api.twitch.tv/kraken/videos/c6055863",
        "channel": "https://api.twitch.tv/kraken/channels/twitch"
      },
      "channel": {
        "name": "twitch",
        "display_name": "Twitch"
      }
    },
    ...
  ],
  "_links": {
    "self": "https://api.twitch.tv/kraken/channels/twitch/videos?limit=10&offset=0",
    "next": "https://api.twitch.tv/kraken/channels/twitch/videos?limit=10&offset=10"
  }
}
```

## Embedding

[See here for embedding.][embedding]

[embedding]: /embedding.md#embedding-streams-vods-and-chat
