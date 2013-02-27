# Streams

## Get the specified channel's stream

`GET /streams/:channel/`

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/streams/magicprotour
```

### Response

#### If the specified channel is offline

`200 OK` with an empty stream object.

```json
{
  "stream": null,
  "_links": {
    "self": "https://api.twitch.tv/kraken/streams/magicprotour",
    "channel": "https://api.twitch.tv/kraken/channels/magicprotour"
  }
}
```

#### If the specified channel is online

`200 OK` with the stream object.

```json
{
  "_links": {
    "channel": "https://api.twitch.tv/kraken/channels/magicprotour",
    "self": "https://api.twitch.tv/kraken/streams/magicprotour"
  },
  "stream": {
    "_links": {
      "self": "https://api.twitch.tv/kraken/streams/magicprotour"
    },
    "broadcaster": "unknown_rtmp",
    "preview": "http://static-cdn.jtvnw.net/previews-ttv/live_user_magicprotour-320x200.jpg",
    "_id": 4869165040,
    "viewers": 11754,
    "channel": {
      "display_name": "MagicProTour",
      "_links": {
        "stream_key": "https://api.twitch.tv/kraken/channels/magicprotour/stream_key",
        "editors": "https://api.twitch.tv/kraken/channels/magicprotour/editors",
        "subscriptions": "https://api.twitch.tv/kraken/channels/magicprotour/subscriptions",
        "commercial": "https://api.twitch.tv/kraken/channels/magicprotour/commercial",
        "videos": "https://api.twitch.tv/kraken/channels/magicprotour/videos",
        "follows": "https://api.twitch.tv/kraken/channels/magicprotour/follows",
        "self": "https://api.twitch.tv/kraken/channels/magicprotour",
        "chat": "https://api.twitch.tv/kraken/chat/magicprotour",
        "features": "https://api.twitch.tv/kraken/channels/magicprotour/features"
      },
      "teams": [ ],
      "status": "Pro Tour Gatecrash in Montreal",
      "created_at": "2011-12-23T18:03:44Z",
      "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/magicprotour-profile_image-1806cdccb1108442-300x300.jpeg",
      "updated_at": "2013-02-15T15:22:24Z",
      "mature": null,
      "video_banner": null,
      "_id": 26991613,
      "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/magicprotour-channel_background_image-21fffe7f0c309a23.jpeg",
      "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/magicprotour-channel_header_image-4eb6147d464d9053-640x125.jpeg",
      "name": "magicprotour",
      "url": "http://www.twitch.tv/magicprotour",
      "game": "Magic: The Gathering"
    },
    "name": "live_user_magicprotour",
    "game": "Magic: The Gathering"
  }
}
```

## Get a list of streams <a id="streams"/>

`GET /streams`

This is a flexible method that allows you to query for multiple streams based on a number of parameters.

### Parameters

- `game` (optional): The game to query.
- `channel` (optional): A list of channel names to query, seperated by commas.
- `limit` (optional): The maximum number of streams to return, up to 100.
- `offset` (optional): The offset to begin listing streams, defaults to 0.
- `embeddable` (optional): If true you'll only get streams which can be embedded. Setting this to false will just drop the flag, because that is a weird thing to do!
- `hls` (optional): If true, only returns streams using HLS.

#### Get list of Diablo III streams

`GET /streams?game=Diablo+III`

#### Get multiple channels

`GET /streams?channel=incredibleorb,incontroltv`

## Get a list of featured (promoted) streams

`GET /streams/featured`

### Parameters

- `limit` (optional): The maximum number of streams to return, up to 100. Defaults to 25.
- `offset` (optional): The offset to begin listing streams, defaults to 0.
- `hls` (optional): If true, only returns streams using HLS.

Note that the number of promoted streams varies from day to day, and there is no guarantee on how many streams will be promoted at a given time.

### Response
    
Response has an array of featured streams and paginated links. Each element in the featured array has promotional text, a promotional image, and a nested stream object (see above).

```json
{
  "_links": {
     "self": "https://api.twitch.tv/kraken/streams/featured?limit=25&offset=0",
     "next": "https://api.twitch.tv/kraken/streams/featured?limit=25&offset=25"
  },
  "featured": [
    {
      "image": "http://s.jtvnw.net/jtv_user_pictures/hosted_images/therun.jpg",
      "text": "This is the run! Watch as multi-time world record Super Mario 64 gamer, Siglemic, pushes the N64 classic to its absolute limits.",
      "stream": {
        ...
      }
    },
    [...]
  ]
}
```
    
## Summarize streams  <a id="summary"/>

`GET /streams/summary`

### Parameters

- `game` (optional): Summarize streams on a per-game basis.
- `channel` (optional): Summarize streams limited to the specified set of comma separated channels.
- `hls` (optional): If true, only returns streams using HLS.

### Response

```json
{
  "viewers": 194774,
  "_links": {
    "self": "https://api.twitch.tv/kraken/streams/summary"
  },
  "channels": 4144
}
```

## Get a list of user's followed streams

[See the Users resource][users]

[users]: /resources/Users.md

## Embedding

[See here for embedding.][embedding]

[embedding]: /embedding.md#embedding-streams-vods-and-chat
