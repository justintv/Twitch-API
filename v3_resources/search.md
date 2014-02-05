# Search

***

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
      "updated_at": "2013-12-25T15:18:23Z", 
      "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/starcrafttv2013-channel_offline_image-16ceb6186030f1a8-640x360.jpeg", 
      "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/starcrafttv2013-profile_image-1c30dd07717a3007-300x300.jpeg", 
      "display_name": "Starcrafttv2013", 
      "delay": 0, 
      "followers": 1216, 
      "_links": {
        "videos": "https://api.twitch.tv/kraken/channels/starcrafttv2013/videos", 
        "features": "https://api.twitch.tv/kraken/channels/starcrafttv2013/features", 
        "stream_key": "https://api.twitch.tv/kraken/channels/starcrafttv2013/stream_key", 
        "subscriptions": "https://api.twitch.tv/kraken/channels/starcrafttv2013/subscriptions", 
        "follows": "https://api.twitch.tv/kraken/channels/starcrafttv2013/follows", 
        "self": "https://api.twitch.tv/kraken/channels/starcrafttv2013", 
        "commercial": "https://api.twitch.tv/kraken/channels/starcrafttv2013/commercial", 
        "editors": "https://api.twitch.tv/kraken/channels/starcrafttv2013/editors", 
        "teams": "https://api.twitch.tv/kraken/channels/starcrafttv2013/teams", 
        "chat": "https://api.twitch.tv/kraken/chat/starcrafttv2013"
      }, 
      "status": "Star TV\u5373\u5c07\u66ab\u505c\u4e00\u6bb5\u6642\u9593", 
      "primary_team_name": null, 
      "views": 80334, 
      "abuse_reported": null, 
      "game": "StarCraft II: Heart of the Swarm", 
      "background": null, 
      "banner": null, 
      "name": "starcrafttv2013", 
      "url": "http://www.twitch.tv/starcrafttv2013", 
      "created_at": "2013-10-07T15:00:40Z", 
      "primary_team_display_name": null, 
      "mature": false, 
      "profile_banner_background_color": null, 
      "_id": 49902474, 
      "profile_banner": null
    }, 
    ...
  ], 
  "_total": 42679, 
  "_links": {
    "self": "https://api.twitch.tv/kraken/search/channels?limit=10&offset=0&q=starcraft", 
    "next": "https://api.twitch.tv/kraken/search/channels?limit=10&offset=10&q=starcraft"
  }
}```

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
      "viewers": 2,
      "_id": 4989654544,
      "channel": {
        "game": "StarCraft II: Heart of the Swarm",
        "display_name": "Blade55555",
        "created_at": "2009-09-19T02:07:23Z",
        "status": "Starcraft 2 HOTS GM zerg",
        "updated_at": "2013-02-28T22:30:17Z",
        "mature": null,
        "_id": 8341905,
        "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/blade55555-channel_offline_image-3abeffa573a391d4-640x360.jpeg",
        "name": "blade55555",
        "banner": null,
        "delay": 0,
        "background": null,
        "_links": {
          "editors": "https://api.twitch.tv/kraken/channels/blade55555/editors",
          "stream_key": "https://api.twitch.tv/kraken/channels/blade55555/stream_key",
          "commercial": "https://api.twitch.tv/kraken/channels/blade55555/commercial",
          "features": "https://api.twitch.tv/kraken/channels/blade55555/features",
          "videos": "https://api.twitch.tv/kraken/channels/blade55555/videos",
          "subscriptions": "https://api.twitch.tv/kraken/channels/blade55555/subscriptions",
          "follows": "https://api.twitch.tv/kraken/channels/blade55555/follows",
          "self": "https://api.twitch.tv/kraken/channels/blade55555",
          "chat": "https://api.twitch.tv/kraken/chat/blade55555"
        },
        "teams": [ ],
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/blade55555-profile_image-e551610be15ec896-300x300.png",
        "url": "http://www.twitch.tv/blade55555"
      },
      "preview": "http://static-cdn.jtvnw.net/previews-ttv/live_user_blade55555-320x200.jpg",
      "name": "live_user_blade55555",
      "_links": {
        "self": "https://api.twitch.tv/kraken/streams/blade55555"
      },
      "broadcaster": "fme"
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
        "small": "http://static-cdn.jtvnw.net/ttv-boxart/StarCraft%20II%3A%20Wings%20of%20Liberty.jpg?w=52&h=72&fit=scale",
        "large": "http://static-cdn.jtvnw.net/ttv-boxart/StarCraft%20II%3A%20Wings%20of%20Liberty.jpg?w=272&h=380&fit=scale",
        "medium": "http://static-cdn.jtvnw.net/ttv-boxart/StarCraft%20II%3A%20Wings%20of%20Liberty.jpg?w=136&h=190&fit=scale",
        "template": "http://static-cdn.jtvnw.net/ttv-boxart/StarCraft%20II%3A%20Wings%20of%20Liberty.jpg?w={width}&h={height}&fit=scale"
      },
      "logo": {
        "small": "http://static-cdn.jtvnw.net/ttv-logoart/StarCraft%20II%3A%20Wings%20of%20Liberty.jpg?w=60&h=36&fit=scale",
        "large": "http://static-cdn.jtvnw.net/ttv-logoart/StarCraft%20II%3A%20Wings%20of%20Liberty.jpg?w=240&h=144&fit=scale",
        "medium": "http://static-cdn.jtvnw.net/ttv-logoart/StarCraft%20II%3A%20Wings%20of%20Liberty.jpg?w=120&h=72&fit=scale",
        "template": "http://static-cdn.jtvnw.net/ttv-logoart/StarCraft%20II%3A%20Wings%20of%20Liberty.jpg?w={width}&h={height}&fit=scale"
      },
      "images": {
        "thumb": "http://media.giantbomb.com/uploads/0/30/1319229-sc2_se_2d_rgb_web_na_thumb.jpg",
        "tiny": "http://media.giantbomb.com/uploads/0/30/1319229-sc2_se_2d_rgb_web_na_tiny.jpg",
        "small": "http://media.giantbomb.com/uploads/0/30/1319229-sc2_se_2d_rgb_web_na_small.jpg",
        "super": "http://media.giantbomb.com/uploads/0/30/1319229-sc2_se_2d_rgb_web_na_super.jpg",
        "medium": "http://media.giantbomb.com/uploads/0/30/1319229-sc2_se_2d_rgb_web_na_small.jpg",
        "icon": "http://media.giantbomb.com/uploads/0/30/1319229-sc2_se_2d_rgb_web_na_icon.jpg",
        "screen": "http://media.giantbomb.com/uploads/0/30/1319229-sc2_se_2d_rgb_web_na_screen.jpg"
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
