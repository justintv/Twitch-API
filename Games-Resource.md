# Games


## Get the top games

`GET /games/top`

This method allows you to retrieve the top (by viewers) games on the site.

### Parameters

- `limit` (optional): The maximum number of games to return, up to 100.
- `offset` (optional): The offset to begin listing games, defaults to 0.

### Response

    {
      "_links": {
        "self": "https://api.twitch.tv/kraken/games/top?limit=10&offset=0",
        "next": "https://api.twitch.tv/kraken/games/top?limit=10&offset=10"
      },
      "top": [
        {
          "game": {
            "name": "League of Legends",
            "_id": 21779,
            "_links": {},
            "images": {
              "screen": "http://media.giantbomb.com/uploads/8/87209/2115067-box_lol_screen.png",
              "medium": "http://media.giantbomb.com/uploads/8/87209/2115067-box_lol_small.png",
              "small": "http://media.giantbomb.com/uploads/8/87209/2115067-box_lol_small.png",
              "tiny": "http://media.giantbomb.com/uploads/8/87209/2115067-box_lol_tiny.png",
              "thumb": "http://media.giantbomb.com/uploads/8/87209/2115067-box_lol_thumb.png",
              "icon": "http://media.giantbomb.com/uploads/8/87209/2115067-box_lol_icon.png",
              "super": "http://media.giantbomb.com/uploads/8/87209/2115067-box_lol_super.png"
            },
            "giantbomb_id": 24024
          },
          "viewers": 24677,
          "channels": 284
        },
        [...]
      ]
    }
