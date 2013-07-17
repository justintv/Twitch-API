# Subscriptions

***

[Users][users] can subscribe to [channels][channels].

| Endpoint | Description |
| ---- | --------------- |
| [GET /channels/:channel/subscriptions](/v2_resources/subscriptions.md#get-channelschannelsubscriptions) | Get list of users subscribed to channel |
| [GET /channels/:channel/subscriptions/:user](/v2_resources/subscriptions.md#get-channelschannelsubscriptionsuser) | Check if channel has user subscribed |
| [GET /users/:user/subscriptions/:channel](/v2_resources/subscriptions.md#get-usersusersubscriptionschannel) | Check if user subscribes to channel |

[users]: /v2_resources/users.md
[channels]: /v2_resources/channels.md

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
curl -H 'Accept: application/vnd.twitchtv.v2+json' -H 'Authorization: OAuth <access_token>' \
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
        "staff": false,
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
curl -H 'Accept: application/vnd.twitchtv.v2+json' -H 'Authorization: OAuth <access_token>' \
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
    "staff": false,
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
curl -H 'Accept: application/vnd.twitchtv.v2+json' -H 'Authorization: OAuth <access_token>' \
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
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-db450d501aa3e884-300x300.jpeg",
        "_links": {
            "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
            "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
            "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
            "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos",
            "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
            "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows",
            "teams": "https://api.twitch.tv/kraken/channels/test_channel/teams",
            "self": "https://api.twitch.tv/kraken/channels/test_channel",
            "chat": "https://api.twitch.tv/kraken/chat/test_channel",
            "features": "https://api.twitch.tv/kraken/channels/test_channel/features"
        },
        "updated_at": "2013-07-16T22:58:51Z",
        "background": null,
        "status": "Game Dev Tycoon Time!",
        "game": "Game Dev Tycoon",
        "profile_banner": null,
        "banner": null,
        "display_name": "test_channel",
        "_id": 188563,
        "url": "https://www.twitch.tv/test_channel",
        "video_banner": null,
        "delay": 0,
        "name": "test_channel",
        "mature": true,
        "created_at": "2007-11-29T05:17:53Z"
    },
    "_id": "ba93ea2a1046081cf8621e3811b435c403479aa2",
    "created_at": "2013-07-16T21:46:27Z"
}
```

`404 Not Found` if user is not subscribed.
