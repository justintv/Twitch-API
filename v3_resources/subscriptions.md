# Subscriptions

[Users][users] can subscribe to [channels][channels].

| Endpoint | Description |
| ---- | --------------- |
| [GET /channels/:channel/subscriptions](/v3_resources/subscriptions.md#get-channelschannelsubscriptions) | Get list of users subscribed to channel |
| [GET /channels/:channel/subscriptions/:user](/v3_resources/subscriptions.md#get-channelschannelsubscriptionsuser) | Check if channel has user subscribed |
| [GET /users/:user/subscriptions/:channel](/v3_resources/subscriptions.md#get-usersusersubscriptionschannel) | Check if user subscribes to channel |

[users]: /v3_resources/users.md
[channels]: /v3_resources/channels.md

## `GET /channels/:channel/subscriptions`

Returns a list of subscription objects sorted by subscription relationship creation date which contain users subscribed to `:channel`.

*__Authenticated__*, required scope: `channel_subscriptions`

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
            <td><code>direction</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Creation date sorting direction. Default is <code>asc</code>. Valid values are <code>asc</code> and <code>desc</code>.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/channels/test_channel/subscriptions
```

### Example Response

```json
{
  "_total": 3,
  "_links": {
    "next": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions?limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions?limit=25&offset=0"
  },
  "subscriptions": [
    {
      "_id": "88d4621871b7274c34d5c3eb5dad6780c8533318",
      "user": {
        "_id": 38248673,
        "logo": null,
        "type": "user",
        "bio": "I'm testuser",
        "created_at": "2012-12-06T00:32:36Z",
        "name": "testuser",
        "updated_at": "2013-02-06T21:27:46Z",
        "display_name": "testuser",
        "_links": {
          "self": "https://api.twitch.tv/kraken/users/testuser"
        }
      },
      "created_at": "2013-02-06T21:33:33Z",
      "_links": {
        "self": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions/testuser"
      }
    },
    ...
  ]
}
```

## `GET /channels/:channel/subscriptions/:user`

Returns a subscription object which includes the user if that user is subscribed. Requires authentication for `:channel`.

*__Authenticated__*, required scope: `channel_check_subscription`

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/channels/test_channel/subscriptions/testuser
```

### Example Response

If user is subscribed:

```json
{
  "_id": "88d4621871b7274c34d5c3eb5dad6780c8533318",
  "user": {
    "_id": 38248673,
    "logo": null,
    "type": "user",
    "bio": "I'm testuser",
    "created_at": "2012-12-06T00:32:36Z",
    "name": "testuser",
    "updated_at": "2013-02-06T21:27:46Z",
    "display_name": "testuser",
    "_links": {
      "self": "https://api.twitch.tv/kraken/users/testuser"
    }
  },
  "created_at": "2013-02-06T21:33:33Z",
  "_links": {
    "self": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions/testuser"
  }
}
```

`404 Not Found` if user is not subscribed.

## `GET /users/:user/subscriptions/:channel`

Returns a channel object that user subscribes to. Requires authentication for `:user`.

*__Authenticated__*, required scope: `user_subscriptions`

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/users/test_user/subscriptions/test_channel
```

### Example Response

If user is subscribed:

```json
{
"_links": {
  "self": "https://api.twitch.tv/kraken/users/test_user/subscriptions/test_channel"
},
  "channel": {
    "mature": false,
    "status": "test status",
    "broadcaster_language": "en",
    "display_name": "test_channel",
    "game": "Gaming Talk Shows",
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
  "_id": "ba93ea2a1046081cf8621e3811b435c403479aa2",
  "created_at": "2013-07-16T21:46:27Z"
}
```

`404 Not Found` if user is not subscribed.

`422 Unprocessable Entity` if channel has no subscription program.
