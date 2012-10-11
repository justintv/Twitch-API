# Search

## Search for live streams

`GET /search/streams`

This method allows you to retrieve live streams on Twitch based on a search query.

### Parameters

- `query` or `q` (required): A url-encoded search query.
- `limit` (optional): The maximum number of streams to return, up to 100. You may occasionally get fewer streams returned than requested in `limit` due to streams in the search index that that have recently gone offline.
- `offset` (optional): The offset to begin listing streams, starting at 0.

### Response

    {
      "_links": {
        "self": "https://api.twitch.tv/kraken/search/streams?limit=10&offset=0&q=starcraft",
        "next": "https://api.twitch.tv/kraken/search/streams?limit=10&offset=10&q=starcraft"
      },
      "streams": [
        {
          "game": "Dark Souls",
          "name": "live_user_valkyrietv",
          "viewers": 35,
          "_id": 3624658944,
          "_links": {
            "self": "https://api.twitch.tv/kraken/streams/valkyrietv"
          },
          "broadcaster": "fme",
          "channel": {
            "name": "valkyrietv",
            "game": "Dark Souls",
            "created_at": "2011-09-13T23:10:03Z",
            "teams": [],
            "banner": null,
            "updated_at": "2012-08-16T21:57:32Z",
            "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/valkyrietv-channel_background_image-5231affde0537afe.jpeg",
            "url": "http://www.twitch.tv/valkyrietv",
            "_links": {
              "stream_key": "https://api.twitch.tv/kraken/channels/valkyrietv/stream_key",
              "self": "https://api.twitch.tv/kraken/channels/valkyrietv",
              "chat": "https://api.twitch.tv/kraken/chat/valkyrietv",
              "commercial": "https://api.twitch.tv/kraken/channels/valkyrietv/commercial",
              "features": "https://api.twitch.tv/kraken/channels/valkyrietv/features"
            },
            "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/valkyrietv-profile_image-e0a179c8b4651ba9-300x300.jpeg",
            "_id": 24801241,
            "mature": null,
            "video_banner": null,
            "display_name": "ValkyrieTV",
            "status": "Valkyrie Plays Dark Souls - Strength Build"
          },
          "preview": "http://static-cdn.jtvnw.net/previews/live_user_valkyrietv-630x473.jpg",
          "partner": false
        },
        [...]
      ]
    }

## Search for games <a id="games"/>

`GET /search/games`

This method allows you to retrieve games on Twitch based on a search query.

### Parameters

- `query` or `q` (required): A url-encoded search query.
- `type` (required): Type of search to perform. Right now, only 'suggest' is implemented
  - `suggest`: Suggests a list of games similar to the query, e.g. 'star' might suggest 'StarCraft II: Wings of Liberty' among others
- `live` (optional): If set to true, only returns games that are live on at least one channel. Setting live to anything other than true has no effect. 

### Response

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