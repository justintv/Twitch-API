# Search

***

Search for [streams][streams] or [games][games] with queries.

| Endpoint | Description |
| ---- | --------------- |
| [GET /search/streams](/v2_resources/search.md#get-searchstreams) | Find streams |
| [GET /search/games](/v2_resources/search.md#get-searchgames) | Find games |

[streams]: /v2_resources/streams.md
[games]: /v2_resources/games.md

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
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v2+json' \
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
        "display_name": "test_user",
        "created_at": "2009-09-19T02:07:23Z",
        "status": "Starcraft 2 HOTS GM zerg",
        "updated_at": "2013-02-28T22:30:17Z",
        "mature": false,
        "_id": 8341905,
        "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_user-channel_offline_image-3abeffa573a391d4-640x360.jpeg",
        "name": "test_user",
        "banner": null,
        "background": null,
        "_links": {
          "editors": "https://api.twitch.tv/kraken/channels/test_user/editors",
          "stream_key": "https://api.twitch.tv/kraken/channels/test_user/stream_key",
          "commercial": "https://api.twitch.tv/kraken/channels/test_user/commercial",
          "features": "https://api.twitch.tv/kraken/channels/test_user/features",
          "videos": "https://api.twitch.tv/kraken/channels/test_user/videos",
          "subscriptions": "https://api.twitch.tv/kraken/channels/test_user/subscriptions",
          "follows": "https://api.twitch.tv/kraken/channels/test_user/follows",
          "self": "https://api.twitch.tv/kraken/channels/test_user",
          "chat": "https://api.twitch.tv/kraken/chat/test_user"
        },
        "teams": [ ],
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_user-profile_image-e551610be15ec896-300x300.png",
        "url": "http://www.twitch.tv/test_user"
      },
      "preview": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_user-320x200.jpg",
      "name": "live_user_test_user",
      "_links": {
        "self": "https://api.twitch.tv/kraken/streams/test_user"
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
curl -H 'Accept: application/vnd.twitchtv.v2+json' \
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
