# Games


## Get the top games

`GET /games/top`

This method allows you to retrieve the top games on Twitch (by current viewers).

### Parameters

- `limit` (optional): The maximum number of games to return, up to 100.
- `offset` (optional): The offset to begin listing games, defaults to 0.

### Response

    {
      "_links": {
        "self": "https://api.twitch.tv/kraken/games/top?limit=10&offset=0",
        "next": "https://api.twitch.tv/kraken/games/top?limit=10&offset=10"
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
