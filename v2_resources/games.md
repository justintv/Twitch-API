# Games

***

Games are categories (e.g. League of Legends, Diablo 3) used by [streams][] and [channels][]. Games can be [searched][search] for by query.

| Endpoint | Description |
| ---- | --------------- |
| [GET /games/top](/v2_resources/games.md#get-gamestop) | Get games by number of viewers |

[streams]: /v2_resources/streams.md
[channels]: /v2_resources/channels.md
[search]: /v2_resources/search.md#search-for-games-

## `GET /games/top`

Returns a list of games objects sorted by number of current viewers on Twitch, most popular first.

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
            <td>If set to true, only returns game objects with streams using HLS</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v2+json' \
-X GET https://api.twitch.tv/kraken/games/top
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/games/top?limit=25&offset=0",
    "next": "https://api.twitch.tv/kraken/games/top?limit=25&offset=25"
  },
  "_total": 322,
  "top": [
    {
      "game": {
        "name": "League of Legends",
        "box": {
          "large": "http://static-cdn.jtvnw.net/ttv-boxart/League%20of%20Legends.jpg?w=272&h=380&fit=scale",
          "medium": "http://static-cdn.jtvnw.net/ttv-boxart/League%20of%20Legends.jpg?w=136&h=190&fit=scale",
          "small": "http://static-cdn.jtvnw.net/ttv-boxart/League%20of%20Legends.jpg?w=52&h=72&fit=scale",
          "template": "http://static-cdn.jtvnw.net/ttv-boxart/League%20of%20Legends.jpg?w={width}&h={height}&fit=scale"
        },
        "logo": {
          "large": "http://static-cdn.jtvnw.net/ttv-logoart/League%20of%20Legends.jpg?w=240&h=144&fit=scale",
          "medium": "http://static-cdn.jtvnw.net/ttv-logoart/League%20of%20Legends.jpg?w=120&h=72&fit=scale",
          "small": "http://static-cdn.jtvnw.net/ttv-logoart/League%20of%20Legends.jpg?w=60&h=36&fit=scale",
          "template": "http://static-cdn.jtvnw.net/ttv-logoart/League%20of%20Legends.jpg?w={width}&h={height}&fit=scale"
        },
        "_links": {},
        "_id": 21779,
        "giantbomb_id": 24024
      },
      "viewers": 23873,
      "channels": 305
    },
    ...
  ]
}
```

### Errors

`503 Service Unvailable` if error retrieving games status.
