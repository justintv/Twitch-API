# Videos

## Get the specified video

`GET /videos/:id/`

### Response

    {
        recorded_at: "2012-08-09T20:49:47Z",
        title: "VanillaTV - Sweden vs Russia - ETF2L Nations Cup - Snakewater [Map3] - Part 3",
        url: "http://www.twitch.tv/vanillatv/b/328087483",
        _id: "a328087483",
        _links: {
            self: "https://api.twitch.tv/kraken/videos/a328087483",
            owner: "https://api.twitch.tv/kraken/channels/vanillatv"
        },
        views: 93,
        description: "VanillaTV - Sweden vs Russia - ETF2L Nations Cup - Snakewater [Map3] - Part 3",
        length: 204,
        preview: "http://static-cdn.jtvnw.net/jtv.thumbs/archive-328087483-320x240.jpg"
    }


## Get videos for a channel <a id="videos-channel" />

`GET /channels/:channel/videos`

### Parameters

- `limit` (optional): The maximum number of videos to return, up to 100.
- `offset` (optional): The offset to begin listing videos, defaults to 0.

### Response
    {
        videos: [
            {
                title: "ETF2L Week 1: Epsilon vs. Dignitas",
                recorded_at: "2011-10-02T19:57:06Z",
                _id: "a296529186",
                _links: {
                    self: "https://api.twitch.tv/kraken/videos/a296529186",
                    owner: "https://api.twitch.tv/kraken/channels/vanillatv"
                },
                url: "http://www.twitch.tv/vanillatv/b/296529186",
                views: 1,
                preview: "http://static-cdn.jtvnw.net/jtv.thumbs/archive-296529186-320x240.jpg",
                length: 23,
                description: null
            },
            {
                title: "ETF2L Week 1: Epsilon vs. Dignitas",
                recorded_at: "2011-10-02T19:01:23Z",
                _id: "a296526250",
                _links: {
                    self: "https://api.twitch.tv/kraken/videos/a296526250",
                    owner: "https://api.twitch.tv/kraken/channels/vanillatv"
                },
                url: "http://www.twitch.tv/vanillatv/b/296526250",
                views: 1,
                preview: "http://static-cdn.jtvnw.net/jtv.thumbs/archive-296526250-320x240.jpg",
                length: 1296,
                description: null
            },
            ...
        ],
        _links: {
            self: "https://api.twitch.tv/kraken/channels/vanillatv/videos?limit=10&offset=0",
            next: "https://api.twitch.tv/kraken/channels/vanillatv/videos?limit=10&offset=10"
        }
    }

