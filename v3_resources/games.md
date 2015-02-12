# Games

***

Games are categories (e.g. League of Legends, Diablo 3) used by [streams][] and [channels][]. Games can be [searched][search] for by query.

| Endpoint | Description |
| ---- | --------------- |
| [GET /games/top](/v3_resources/games.md#get-gamestop) | Get games by number of viewers |

[streams]: /v3_resources/streams.md
[channels]: /v3_resources/channels.md
[search]: /v3_resources/search.md#search-for-games-

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
            <td>Maximum number of objects in array. Default is 10. Maximum is 100.</td>
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
-X GET https://api.twitch.tv/kraken/games/top
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/games/top?limit=10&offset=0",
    "next": "https://api.twitch.tv/kraken/games/top?limit=10&offset=10"
  },
  "_total": 322,
  "top": [
    {
      "game": {
        "name": "Counter-Strike: Global Offensive",
        "box": {
          "large": "http://static-cdn.jtvnw.net/ttv-boxart/Counter-Strike:%20Global%20Offensive-272x380.jpg",
          "medium": "http://static-cdn.jtvnw.net/ttv-boxart/Counter-Strike:%20Global%20Offensive-136x190.jpg",
          "small": "http://static-cdn.jtvnw.net/ttv-boxart/Counter-Strike:%20Global%20Offensive-52x72.jpg",
          "template": "http://static-cdn.jtvnw.net/ttv-boxart/Counter-Strike:%20Global%20Offensive-{width}x{height}.jpg"
        },
        "logo": {
          "large": "http://static-cdn.jtvnw.net/ttv-logoart/Counter-Strike:%20Global%20Offensive-240x144.jpg",
          "medium": "http://static-cdn.jtvnw.net/ttv-logoart/Counter-Strike:%20Global%20Offensive-120x72.jpg",
          "small": "http://static-cdn.jtvnw.net/ttv-logoart/Counter-Strike:%20Global%20Offensive-60x36.jpg",
          "template": "http://static-cdn.jtvnw.net/ttv-logoart/Counter-Strike:%20Global%20Offensive-{width}x{height}.jpg"
        },
        "_links": {},
        "_id": 32399,
        "giantbomb_id": 36113
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
