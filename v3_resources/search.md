# Search

Search for [channels][channels], [streams][streams] or [games][games] with queries.

| Endpoint | Description |
| ---- | --------------- |
| [GET /search/channels](/v3_resources/search.md#get-searchchannels) | Find channels |
| [GET /search/streams](/v3_resources/search.md#get-searchstreams) | Find streams |
| [GET /search/games](/v3_resources/search.md#get-searchgames) | Find games |

[channels]: /v3_resources/channels.md
[streams]: /v3_resources/streams.md
[games]: /v3_resources/games.md

## `GET /search/channels`

Returns a list of channel objects matching the search query.

### Parameters

<table width=100%>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>query</code> or <code>q</code></td>
            <td>required</td>
            <td>string</td>
            <td>A url-encoded search query.</td>
        </tr>
        <tr>
            <td><code>limit</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Maximum number of objects in array. Default is 25. Maximum is 100.</td>
        </tr>
        <tr>
            <td><code>offset</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Object offset for pagination. Default is 0.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/search/channels?q=starcraft
```

### Example Response

```json
{
  "channels": [
    {
      "mature": false,
      "status": "test status",
      "broadcaster_language": "en",
      "display_name": "test_channel",
      "game": "StarCraft II: Heart of the Swarm",
      "delay": 0,
      "language": "en",
      "_id": 12345,
      "name": "test_channel",
      "created_at": "2007-05-22T10:39:54Z",
      "updated_at": "2015-02-12T04:15:49Z",
      "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-94a42b3a13c31c02-300x300.jpeg",
      "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_header_image-08dd874c17f39837-640x125.png",
      "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_offline_image-b314c834d210dc1a-640x360.png",
      "background": null,
      "profile_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_banner-6936c61353e4aeed-480.png",
      "profile_banner_background_color": "null",
      "partner": true,
      "url": "http://www.twitch.tv/test_channel",
      "views": 49144894,
      "followers": 215780,
      "_links": {
        "self": "https://api.twitch.tv/kraken/channels/test_channel",
        "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows",
        "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
        "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
        "chat": "https://api.twitch.tv/kraken/chat/test_channel",
        "features": "https://api.twitch.tv/kraken/channels/test_channel/features",
        "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
        "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
        "teams": "https://api.twitch.tv/kraken/channels/test_channel/teams",
        "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos"
      }
    }, 
    ...
  ], 
  "_total": 42679, 
  "_links": {
    "self": "https://api.twitch.tv/kraken/search/channels?limit=10&offset=0&q=starcraft", 
    "next": "https://api.twitch.tv/kraken/search/channels?limit=10&offset=10&q=starcraft"
  }
}
```

### Errors

`503 Service Unavailable` if unable to retrieve search results.

## `GET /search/streams`

Returns a list of stream objects matching the search query.

### Parameters

<table width=100%>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>query</code> or <code>q</code></td>
            <td>required</td>
            <td>string</td>
            <td>A url-encoded search query.</td>
        </tr>
        <tr>
            <td><code>limit</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Maximum number of objects in array. Default is 25. Maximum is 100.</td>
        </tr>
        <tr>
            <td><code>offset</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Object offset for pagination. Default is 0.</td>
        </tr>
        <tr>
            <td><code>hls</code></td>
            <td>optional</td>
            <td>bool</td>
            <td>If set to true, only returns streams using HLS. If set to false, only returns streams that are non-HLS.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/search/streams?q=starcraft
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/search/streams?limit=25&offset=0&q=starcraft",
    "next": "https://api.twitch.tv/kraken/search/streams?limit=25&offset=25&q=starcraft"
  },
  "streams": [
    {
      "game": "StarCraft II: Heart of the Swarm",
      "viewers": 2123,
      "created_at": "2015-02-12T04:42:31Z",
      "_id": 4989654544,
      "channel": {
        "mature": false,
        "status": "test status",
        "broadcaster_language": "en",
        "display_name": "test_channel",
        "game": "StarCraft II: Heart of the Swarm",
        "delay": 0,
        "language": "en",
        "_id": 12345,
        "name": "test_channel",
        "created_at": "2007-05-22T10:39:54Z",
        "updated_at": "2015-02-12T04:15:49Z",
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-94a42b3a13c31c02-300x300.jpeg",
        "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_header_image-08dd874c17f39837-640x125.png",
        "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_offline_image-b314c834d210dc1a-640x360.png",
        "background": null,
        "profile_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_banner-6936c61353e4aeed-480.png",
        "profile_banner_background_color": "null",
        "partner": true,
        "url": "http://www.twitch.tv/test_channel",
        "views": 49144894,
        "followers": 215780,
        "_links": {
          "self": "https://api.twitch.tv/kraken/channels/test_channel",
          "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows",
          "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
          "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
          "chat": "https://api.twitch.tv/kraken/chat/test_channel",
          "features": "https://api.twitch.tv/kraken/channels/test_channel/features",
          "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
          "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
          "teams": "https://api.twitch.tv/kraken/channels/test_channel/teams",
          "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos"
        }
      },
      "preview": {
        "small": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-80x45.jpg",
        "medium": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-320x180.jpg",
        "large": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-640x360.jpg",
        "template": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-{width}x{height}.jpg"
      },
      "_links": {
        "self": "https://api.twitch.tv/kraken/streams/test_channel"
      }
    },
    ...
  ]
}
```

### Errors

`503 Service Unavailable` if unable to retrieve search results.

## `GET /search/games`

Returns a list of game objects matching the search query.

### Parameters

<table width=100%>
    <thead>
        <tr>
            <th width=15%>Name</th>
            <th>Required?</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>query</code> or <code>q</code></td>
            <td>required</td>
            <td>string</td>
            <td>A url-encoded search query.</td>
        </tr>
        <tr>
            <td><code>type</code></td>
            <td>required</td>
            <td>string</td>
            <td><code>suggest</code>: Suggests a list of games similar to query, e.g. 'star' query might suggest 'StarCraft II: Wings of Liberty'.</td>
        </tr>
        <tr>
            <td><code>live</code></td>
            <td>optional</td>
            <td>bool</td>
            <td>If true, only returns games that are live on at least one channel.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/search/games?q=star&type=suggest
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/search/games?q=star&type=suggest",
  },
  "games": [
    {
      "box": {
        "large": "http://static-cdn.jtvnw.net/ttv-boxart/StarCraft%20II:%20Wings%20of%20Liberty-272x380.jpg",
        "medium": "http://static-cdn.jtvnw.net/ttv-boxart/StarCraft%20II:%20Wings%20of%20Liberty-136x190.jpg",
        "small": "http://static-cdn.jtvnw.net/ttv-boxart/StarCraft%20II:%20Wings%20of%20Liberty-52x72.jpg",
        "template": "http://static-cdn.jtvnw.net/ttv-boxart/StarCraft%20II:%20Wings%20of%20Liberty-{width}x{height}.jpg"
      },
      "logo": {
        "large": "http://static-cdn.jtvnw.net/ttv-logoart/StarCraft%20II:%20Wings%20of%20Liberty-240x144.jpg",
        "medium": "http://static-cdn.jtvnw.net/ttv-logoart/StarCraft%20II:%20Wings%20of%20Liberty-120x72.jpg",
        "small": "http://static-cdn.jtvnw.net/ttv-logoart/StarCraft%20II:%20Wings%20of%20Liberty-60x36.jpg",
        "template": "http://static-cdn.jtvnw.net/ttv-logoart/StarCraft%20II:%20Wings%20of%20Liberty-{width}x{height}.jpg"
      },
      "popularity": 114,
      "name": "StarCraft II: Wings of Liberty",
      "_id": 63011880,
      "_links": { },
      "giantbomb_id": 20674          
    },
    ...
  ]
}
```

### Errors

`503 Service Unavailable` if unable to retrieve search results.
