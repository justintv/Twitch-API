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
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/streams/test_channel
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
    "game": "StarCraft II: Heart of the Swarm",
    "viewers": 2123,
    "created_at": "2015-02-12T04:42:31Z",
    "_id": 4989654544,
    "channel": {
      "mature": false,
      "status": "test status",
      "broadcaster_language": "en",
      "display_name": "test_channel",
      "game": "StarCraft II: Heart of the Swarm",
      "delay": 0,
      "language": "en",
      "_id": 12345,
      "name": "test_channel",
      "created_at": "2007-05-22T10:39:54Z",
      "updated_at": "2015-02-12T04:15:49Z",
      "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-94a42b3a13c31c02-300x300.jpeg",
      "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_header_image-08dd874c17f39837-640x125.png",
      "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_offline_image-b314c834d210dc1a-640x360.png",
      "background": null,
      "profile_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_banner-6936c61353e4aeed-480.png",
      "profile_banner_background_color": "null",
      "partner": true,
      "url": "http://www.twitch.tv/test_channel",
      "views": 49144894,
      "followers": 215780,
      "_links": {
        "self": "https://api.twitch.tv/kraken/channels/test_channel",
        "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows",
        "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
        "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
        "chat": "https://api.twitch.tv/kraken/chat/test_channel",
        "features": "https://api.twitch.tv/kraken/channels/test_channel/features",
        "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
        "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
        "teams": "https://api.twitch.tv/kraken/channels/test_channel/teams",
        "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos"
      }
    },
    "preview": {
      "small": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-80x45.jpg",
      "medium": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-320x180.jpg",
      "large": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-640x360.jpg",
      "template": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-{width}x{height}.jpg"
    },
    "_links": {
      "self": "https://api.twitch.tv/kraken/streams/test_channel"
    }
  }
}
```

## `GET /streams`

Returns a list of stream objects that are queried by a number of parameters sorted by number of viewers descending.

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
            <td><code>client_id</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Only shows streams from applications of <code>client_id</code>.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/streams?game=StarCraft+II%3A+Heart+of+the+Swarm&channel=test_channel,test_channel2
```

### Example Response

```json
{
  "_total": 12345,
  "streams": [
    {
      "game": "StarCraft II: Heart of the Swarm",
      "viewers": 2123,
      "created_at": "2015-02-12T04:42:31Z",
      "_id": 4989654544,
      "channel": {
        "mature": false,
        "status": "test status",
        "broadcaster_language": "en",
        "display_name": "test_channel",
        "game": "StarCraft II: Heart of the Swarm",
        "delay": 0,
        "language": "en",
        "_id": 12345,
        "name": "test_channel",
        "created_at": "2007-05-22T10:39:54Z",
        "updated_at": "2015-02-12T04:15:49Z",
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-94a42b3a13c31c02-300x300.jpeg",
        "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_header_image-08dd874c17f39837-640x125.png",
        "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_offline_image-b314c834d210dc1a-640x360.png",
        "background": null,
        "profile_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_banner-6936c61353e4aeed-480.png",
        "profile_banner_background_color": "null",
        "partner": true,
        "url": "http://www.twitch.tv/test_channel",
        "views": 49144894,
        "followers": 215780,
        "_links": {
          "self": "https://api.twitch.tv/kraken/channels/test_channel",
          "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows",
          "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
          "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
          "chat": "https://api.twitch.tv/kraken/chat/test_channel",
          "features": "https://api.twitch.tv/kraken/channels/test_channel/features",
          "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
          "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
          "teams": "https://api.twitch.tv/kraken/channels/test_channel/teams",
          "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos"
        }
      },
      "preview": {
        "small": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-80x45.jpg",
        "medium": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-320x180.jpg",
        "large": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-640x360.jpg",
        "template": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-{width}x{height}.jpg"
      },
      "_links": {
        "self": "https://api.twitch.tv/kraken/streams/test_channel"
      }
    },
    ...
  ],
  "_links": {
    "summary": "https://api.twitch.tv/kraken/streams/summary",
    "followed": "https://api.twitch.tv/kraken/streams/followed",
    "next": "https://api.twitch.tv/kraken/streams?channel=test_channel%2Ctest_channel2&game=StarCraft+II%3A+Heart+of+the+Swarm&limit=100&offset=100",
    "featured": "https://api.twitch.tv/kraken/streams/featured",
    "self": "https://api.twitch.tv/kraken/streams?channel=test_channel%2Ctest_channel2&game=StarCraft+II%3A+Heart+of+the+Swarm&limit=100&offset=0"
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
    </tbody>
</table>

Note that the number of promoted streams varies from day to day, and there is no guarantee on how many streams will be promoted at a given time.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/streams/featured
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
      "image": "http://s.jtvnw.net/jtv_user_pictures/hosted_images/TwitchPartnerSpotlight.png",
      "text": "<p>some html to describe this featured stream</p>",
      "title": "Twitch Partner Spotlight",
      "sponsored": false,
      "scheduled": true,
      "stream": {
        "game": "StarCraft II: Heart of the Swarm",
        "viewers": 2123,
        "created_at": "2015-02-12T04:42:31Z",
        "_id": 4989654544,
        "channel": {
          "mature": false,
          "status": "test status",
          "broadcaster_language": "en",
          "display_name": "test_channel",
          "game": "StarCraft II: Heart of the Swarm",
          "delay": 0,
          "language": "en",
          "_id": 12345,
          "name": "test_channel",
          "created_at": "2007-05-22T10:39:54Z",
          "updated_at": "2015-02-12T04:15:49Z",
          "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-94a42b3a13c31c02-300x300.jpeg",
          "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_header_image-08dd874c17f39837-640x125.png",
          "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_offline_image-b314c834d210dc1a-640x360.png",
          "background": null,
          "profile_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_banner-6936c61353e4aeed-480.png",
          "profile_banner_background_color": "null",
          "partner": true,
          "url": "http://www.twitch.tv/test_channel",
          "views": 49144894,
          "followers": 215780,
          "_links": {
            "self": "https://api.twitch.tv/kraken/channels/test_channel",
            "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows",
            "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
            "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
            "chat": "https://api.twitch.tv/kraken/chat/test_channel",
            "features": "https://api.twitch.tv/kraken/channels/test_channel/features",
            "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
            "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
            "teams": "https://api.twitch.tv/kraken/channels/test_channel/teams",
            "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos"
          }
        },
        "preview": {
          "small": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-80x45.jpg",
          "medium": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-320x180.jpg",
          "large": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-640x360.jpg",
          "template": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-{width}x{height}.jpg"
        },
        "_links": {
          "self": "https://api.twitch.tv/kraken/streams/test_channel"
        }
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
            <td><code>game</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Only show stats for the set game</td>
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
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/streams/summary
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
