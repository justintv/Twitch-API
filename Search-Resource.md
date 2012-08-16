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