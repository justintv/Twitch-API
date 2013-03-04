# Streams

***

Streams are video broadcasts that are currently live. They have a [broadcaster][users] and are part of a [channel][channels].

| Endpoint | Description |
| ---- | --------------- |
| [GET /streams/:channel/](/v3_resources/streams.md#get-streamschannel) | Get stream object |
| [GET /streams](/v3_resources/streams.md#get-streams) | Get stream object |
| [GET /streams/featured](/v3_resources/streams.md#get-streamsfeatured) | Get a list of featured streams |
| [GET /streams/summary](/v3_resources/streams.md#get-streamssummary) | Get a summary of streams |
| [GET /streams/followed](/v3_resources/streams.md#get-streamsfollowed) | Get a list of streams user is following |

[users]: /v3_resources/users.md
[channels]: /v3_resources/channels.md

## `GET /streams/:channel/`

Returns a stream object if live.

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/streams/test_channel
```

### Example Response

#### If offline

```json
{
  "stream": null,
  "_links": {
    "self": "https://api.twitch.tv/kraken/streams/test_channel",
    "channel": "https://api.twitch.tv/kraken/channels/test_channel"
  }
}
```

#### If online

```json
{
  "_links": {
    "channel": "https://api.twitch.tv/kraken/channels/test_channel",
    "self": "https://api.twitch.tv/kraken/streams/test_channel"
  },
  "stream": {
    "_links": {
      "self": "https://api.twitch.tv/kraken/streams/test_channel"
    },
    "broadcaster": "test_user1",
    "preview": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-320x200.jpg",
    "_id": 4869165040,
    "viewers": 11754,
    "channel": {
      "display_name": "test_channel",
      "_links": {
        "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
        "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
        "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
        "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
        "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos",
        "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows",
        "self": "https://api.twitch.tv/kraken/channels/test_channel",
        "chat": "https://api.twitch.tv/kraken/chat/test_channel",
        "features": "https://api.twitch.tv/kraken/channels/test_channel/features"
      },
      "teams": [ ],
      "status": "Testing 1 2 3",
      "created_at": "2011-12-23T18:03:44Z",
      "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-1806cdccb1108442-300x300.jpeg",
      "updated_at": "2013-02-15T15:22:24Z",
      "mature": null,
      "video_banner": null,
      "_id": 26991613,
      "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_background_image-21fffe7f0c309a23.jpeg",
      "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_header_image-4eb6147d464d9053-640x125.jpeg",
      "name": "test_channel",
      "url": "http://www.twitch.tv/test_channel",
      "game": "Magic: The Gathering"
    },
    "name": "test_channel",
    "game": "Magic: The Gathering"
  }
}
```

## `GET /streams`

Returns a list of stream objects that are queried by a number of parameters.

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
            <td><code>game</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Streams categorized under <code>game</code>.</td>
        </tr>
        <tr>
            <td><code>channel</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Streams from a comma separated list of channels.</td>
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
        <tr>
            <td><code>embeddable</code></td>
            <td>optional</td>
            <td>bool</td>
            <td>If set to true, only returns streams that can be embedded</td>
        </tr>
        <tr>
            <td><code>hls</code></td>
            <td>optional</td>
            <td>bool</td>
            <td>If set to true, only returns streams using HLS</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/streams?game=Diablo+III&channel=zisss,voyboy
```

### Example Response

```json
{
  "streams": [
    {
      "broadcaster": "fme",
      "_id": 5019229776,
      "preview": "http://static-cdn.jtvnw.net/previews-ttv/live_user_zisss-320x200.jpg",
      "game": "Diablo III",
      "channel": {
        "mature": null,
        "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/zisss-channel_background_image-06a9d8c1113e5b45.jpeg",
        "updated_at": "2013-03-04T05:27:27Z",
        "_id": 31795858,
        "status": "Barb sets giveaway and making 500m DH set... Join Zisspire, earn Zeny, collect prizes!",
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/zisss-profile_image-502d7c865c5e3a54-300x300.jpeg",
        "teams": [ ],
        "url": "http://www.twitch.tv/zisss",
        "display_name": "Zisss",
        "game": "Diablo III",
        "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/zisss-channel_header_image-997348d7f0658115-640x125.jpeg",
        "name": "zisss",
        "video_banner": null,
        "_links": {
          "chat": "https://api.twitch.tv/kraken/chat/zisss",
          "subscriptions": "https://api.twitch.tv/kraken/channels/zisss/subscriptions",
          "features": "https://api.twitch.tv/kraken/channels/zisss/features",
          "commercial": "https://api.twitch.tv/kraken/channels/zisss/commercial",
          "stream_key": "https://api.twitch.tv/kraken/channels/zisss/stream_key",
          "editors": "https://api.twitch.tv/kraken/channels/zisss/editors",
          "videos": "https://api.twitch.tv/kraken/channels/zisss/videos",
          "self": "https://api.twitch.tv/kraken/channels/zisss",
          "follows": "https://api.twitch.tv/kraken/channels/zisss/follows"
        },
        "created_at": "2012-07-01T21:09:58Z"
      },
      "name": "live_user_zisss",
      "viewers": 775,
      "_links": {
        "self": "https://api.twitch.tv/kraken/streams/zisss"
      }
    }
  ],
  "_links": {
    "summary": "https://api.twitch.tv/kraken/streams/summary",
    "followed": "https://api.twitch.tv/kraken/streams/followed",
    "next": "https://api.twitch.tv/kraken/streams?channel=zisss%2Cvoyboy&game=Diablo+III&limit=100&offset=100",
    "featured": "https://api.twitch.tv/kraken/streams/featured",
    "self": "https://api.twitch.tv/kraken/streams?channel=zisss%2Cvoyboy&game=Diablo+III&limit=100&offset=0"
  }
}
```

## `GET /streams/featured`

Returns a list of featured (promoted) stream objects.

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
            <td>If set to true, only returns streams using HLS</td>
        </tr>
    </tbody>
</table>

Note that the number of promoted streams varies from day to day, and there is no guarantee on how many streams will be promoted at a given time.

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/streams/featured
```

### Example Response

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
    
## `GET /streams/summary`

Returns a summary of current streams.

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
            <td>If set to true, only returns streams using HLS</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/streams/summary
```

### Example Response

```json
{
  "viewers": 194774,
  "_links": {
    "self": "https://api.twitch.tv/kraken/streams/summary"
  },
  "channels": 4144
}
```

## `GET /streams/followed`

[See the Users resource][users]

[users]: /v3_resources/users.md

## Embedding

[See here for embedding.][embedding]

[embedding]: /embedding.md#embedding-streams-vods-and-chat
