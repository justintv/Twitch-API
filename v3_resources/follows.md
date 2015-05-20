# Follows

Status of follow relationships between [users][users] and [channels][channels].

| Endpoint | Description |
| ---- | --------------- |
| [GET /channels/:channel/follows](/v3_resources/follows.md#get-channelschannelfollows) | Get channel's list of following users |
| [GET /users/:user/follows/channels](/v3_resources/follows.md#get-usersuserfollowschannels) | Get a user's list of followed channels |
| [GET /users/:user/follows/channels/:target](/v3_resources/follows.md#get-usersuserfollowschannelstarget) | Get status of follow relationship between user and target channel |
| [PUT /users/:user/follows/channels/:target](/v3_resources/follows.md#put-usersuserfollowschannelstarget) | Follow a channel |
| [DELETE /users/:user/follows/channels/:target](/v3_resources/follows.md#delete-usersuserfollowschannelstarget) | Unfollow a channel |
| [GET /streams/followed](/v3_resources/users.md#get-streamsfollowed) | Get a list of streams user is following |

[users]: /v3_resources/users.md
[channels]: /v3_resources/channels.md

## `GET /channels/:channel/follows`

Returns a list of follow objects.

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
            <td>Creation date sorting direction. Default is <code>desc</code>. Valid values are <code>asc</code> and <code>desc</code>.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/channels/test_user1/follows
```

### Example Response

```json
{
  "_total": 1234,
  "_links": {
    "next": "https://api.twitch.tv/kraken/channels/test_user1/follows?direction=DESC&limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/channels/test_user1/follows?direction=DESC&limit=25&offset=0"
  },
  "follows": [
    {
      "created_at": "2013-06-02T09:38:45Z",
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/test_user2/follows/channels/test_user1"
      },
      "notifications": true,
      "user": {
        "_links": {
          "self": "https://api.twitch.tv/kraken/users/test_user2"
        },
        "type": "user",
        "bio": "test user's bio",
        "logo": null,
        "display_name": "test_user2",
        "created_at": "2013-02-06T21:21:57Z",
        "updated_at": "2013-02-13T20:59:42Z",
        "_id": 40091581,
        "name": "test_user2"
      }
    },
    ...
  ]
}
```

## `GET /users/:user/follows/channels`

Returns a list of follows objects.

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
            <td>Sorting direction. Default is <code>desc</code>. Valid values are <code>asc</code> and <code>desc</code>.</td>
        </tr>
        <tr>
            <td><code>sortby</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Sort key. Default is <code>created_at</code>. Valid values are <code>created_at</code> and <code>last_broadcast</code>.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/users/test_user1/follows/channels
```

### Example Response

```json
{
  "_links": {
    "next": "https://api.twitch.tv/kraken/users/test_user1/follows/channels?direction=DESC&limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/users/test_user1/follows/channels?direction=DESC&limit=25&offset=0"
  },
  "_total": 32,
  "follows": [
    {
      "created_at": "2013-06-02T09:38:45Z",
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel"
      },
      "notifications": true,
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
      }
    },
    ...
  ]
}
```

### Errors

`404 Not Found` if `:user` does not exist.

## `GET /users/:user/follows/channels/:target`

Returns `404 Not Found` if `:user` is not following `:target`. Returns a follow object otherwise.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel
```

### Example Response

`404 Not Found` if user is not following channel.

Otherwise,

```json
{
  "created_at": "2013-06-02T09:38:45Z",
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel"
  },
  "notifications": true,
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
  }
}
```

## `PUT /users/:user/follows/channels/:target`

Adds `:user` to `:target`'s followers. `:user` is the authenticated user's name and `:target` is the name of the channel to be followed.

*__Authenticated__*, required scope: `user_follows_edit`

### Parameters

| Name            | Required? | Type    | Description                                                                                                                                      |
|:----------------|:----------|:--------|:-------------------------------------------------------------------------------------------------------------------------------------------------|
| `notifications` | optional  | boolean | Whether `:user` should receive email/push notifications (depending on their notification settings) when `:target` goes live. Default is `false`. |

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X PUT https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel
```

### Example Response

```json
{
  "created_at": "2013-06-02T09:38:45Z",
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel"
  },
  "notifications": false,
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
  }
}
```

### Errors

`422 Unprocessable Entity` if update fails.

## `DELETE /users/:user/follows/channels/:target`

Removes `:user` from `:target`'s followers. `:user` is the authenticated user's name and `:target` is the name of the channel to be unfollowed.

*__Authenticated__*, required scope: `user_follows_edit`

### Example 

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X DELETE https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel
```

### Example Response

`204 No Content` if successful.

### Errors

`422 Unprocessable Entity` if delete fails.

## `GET /streams/followed`

[See the Users resource][users]

[users]: /v3_resources/users.md
