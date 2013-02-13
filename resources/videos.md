# Videos

Videos are videos-on-demand owned by a [channel][channels].

[channels]: /resources/channels.md

## Get the specified video

`GET /videos/:id/`

Returns the specified video metadata and embed code.

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/videos/a328087483
```

### Response

```json
{
    "recorded_at": "2012-08-09T20:49:47Z",
    "title": "VanillaTV - Sweden vs Russia - ETF2L Nations Cup - Snakewater [Map3] - Part 3",
    "url": "http://www.twitch.tv/vanillatv/b/328087483",
    "_id": "a328087483",
    "_links": {
        "self": "https://api.twitch.tv/kraken/videos/a328087483",
        "owner": "https://api.twitch.tv/kraken/channels/vanillatv"
    },
    "embed": "<object type="application/x-shockwave-flash" height="300" width="400" id="clip_embed_player_flash" data="http://www.justin.tv/widgets/archive_embed_player.swf" bgcolor="#000000">
        <param name="movie" value="http://www.justin.tv/widgets/archive_embed_player.swf" />
        <param name="allowScriptAccess" value="always" />
        <param name="allowNetworking" value="all" />
        <param name="allowFullScreen" value="true" />
        <param name="flashvars" value="channel=vanillatv&title=VanillaTV - Sweden vs Russia - ETF2L Nations Cup - Snakewater [Map3] - Part 3&auto_play=false&archive_id=328087483&start_volume=25" />
    </object>",
    "views": 93,
    "description": "VanillaTV - Sweden vs Russia - ETF2L Nations Cup - Snakewater [Map3] - Part 3",
    "length": 204,
    "preview": "http://static-cdn.jtvnw.net/jtv.thumbs/archive-328087483-320x240.jpg"
}
```


## Get videos for a channel <a id="videos-channel" />

`GET /channels/:channel/videos`

Returns an array of videos ordered by time of creation, starting with the most recent.

### Parameters

- `limit` (optional): The maximum number of videos to return, up to 100.
- `offset` (optional): The offset to begin listing videos, defaults to 0.

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/channels/vanillatv/videos?limit=10
```

### Response

```json
{
    "videos": [
        {
            "title": "ETF2L Week 1: Epsilon vs. Dignitas",
            "recorded_at": "2011-10-02T19:57:06Z",
            "_id": "a296529186",
            "_links": {
                "self": "https://api.twitch.tv/kraken/videos/a296529186",
                "owner": "https://api.twitch.tv/kraken/channels/vanillatv"
            },
            "embed": "<object type="application/x-shockwave-flash" height="300" width="400" id="clip_embed_player_flash" data="http://www.justin.tv/widgets/archive_embed_player.swf" bgcolor="#000000">
                <param name="movie" value="http://www.justin.tv/widgets/archive_embed_player.swf" />
                <param name="allowScriptAccess" value="always" />
                <param name="allowNetworking" value="all" />
                <param name="allowFullScreen" value="true" />
                <param name="flashvars" value="channel=vanillatv&title=VanillaTV - Sweden vs Russia - ETF2L Nations Cup - Snakewater [Map3] - Part 3&auto_play=false&archive_id=328087483&start_volume=25" />
            </object>",
            "url": "http://www.twitch.tv/vanillatv/b/296529186",
            "views": 1,
            "preview": "http://static-cdn.jtvnw.net/jtv.thumbs/archive-296529186-320x240.jpg",
            "length": 23,
            "description": null
        },
        {
            "title": "ETF2L Week 1: Epsilon vs. Dignitas",
            "recorded_at": "2011-10-02T19:01:23Z",
            "_id": "a296526250",
            "_links": {
                "self": "https://api.twitch.tv/kraken/videos/a296526250",
                "owner": "https://api.twitch.tv/kraken/channels/vanillatv"
            },
            "embed": "<object type="application/x-shockwave-flash" height="300" width="400" id="clip_embed_player_flash" data="http://www.justin.tv/widgets/archive_embed_player.swf" bgcolor="#000000">
                <param name="movie" value="http://www.justin.tv/widgets/archive_embed_player.swf" />
                <param name="allowScriptAccess" value="always" />
                <param name="allowNetworking" value="all" />
                <param name="allowFullScreen" value="true" />
                <param name="flashvars" value="channel=vanillatv&title=VanillaTV - Sweden vs Russia - ETF2L Nations Cup - Snakewater [Map3] - Part 3&auto_play=false&archive_id=328087483&start_volume=25" />
            </object>",
            "url": "http://www.twitch.tv/vanillatv/b/296526250",
            "views": 1,
            "preview": "http://static-cdn.jtvnw.net/jtv.thumbs/archive-296526250-320x240.jpg",
            "length": 1296,
            "description": null
        },
        ...
    ],
    "_links": {
        "self": "https://api.twitch.tv/kraken/channels/vanillatv/videos?limit=10&offset=0",
        "next": "https://api.twitch.tv/kraken/channels/vanillatv/videos?limit=10&offset=10"
    }
}
```

## Embedding

[See here for embedding.][embedding]

[embedding]: /embedding.md#embedding-streams-vods-and-chat
