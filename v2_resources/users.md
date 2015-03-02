# Users

These are members of the Twitch community who have a Twitch account. If broadcasting, they can own a [stream][streams] that they can broadcast on their [channel][channels]. If mainly viewing, they might [follow][follows] or [subscribe][subscriptions] to channels.

| Endpoint | Description |
| ---- | --------------- |
| [GET /users/:user](/v2_resources/users.md#get-usersuser) | Get user object |
| [GET /user](/v2_resources/users.md#get-user) | Get user object |
| [GET /streams/followed](/v2_resources/users.md#get-streamsfollowed) | Get list of streams user is following |

[streams]: /v2_resources/streams.md
[channels]: /v2_resources/channels.md
[follows]: /v2_resources/follows.md
[subscriptions]: /v2_resources/subscriptions.md

## `GET /users/:user`

Returns a user object.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v2+json' \
-X GET https://api.twitch.tv/kraken/users/test_user1
```

### Example Response

```json
{
  "name": "test_user1",
  "created_at": "2011-03-19T15:42:22Z",
  "updated_at": "2012-06-14T00:14:27Z",
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/test_user1"
  },
  "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_user1-profile_image-6947308654ad603f-300x300.jpeg",
  "_id": 21229404,
  "staff": false,
  "display_name": "test_user1"
}
```

## `GET /user`

Returns a user object.

*__Authenticated__*, required scope: `user_read`

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v2+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/user
```

### Example Response

```json
{
  "name": "test_user1",
  "created_at": "2011-06-03T17:49:19Z",
  "updated_at": "2012-06-18T17:19:57Z",
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/test_user1"
  },
  "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_user1-profile_image-62e8318af864d6d7-300x300.jpeg",
  "_id": 22761313,
  "staff": false,
  "display_name": "test_user1",
  "email": "asdf@asdf.com",
  "partnered": true,
  "notifications": {
    "email": true,
    "push": false
  }
}
```

## `GET /streams/followed`

Returns a list of stream objects that the authenticated user is following.

*__Authenticated__*, required scope: `user_read`

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v2+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/streams/followed
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/streams/followed?limit=25&offset=0",
    "next": "https://api.twitch.tv/kraken/streams/followed?limit=25&offset=25"
  },
  "streams": [
    {
      "broadcaster": "fme",
      "_id": 5019229776,
      "preview": "http://static-cdn.jtvnw.net/previews-ttv/live_user_test_channel-320x200.jpg",
      "game": "Diablo III",
      "channel": {
        "mature": false,
        "partner": true,
        "broadcaster_language": "en",
        "background": null,
        "updated_at": "2013-03-04T05:27:27Z",
        "_id": 31795858,
        "status": "Barb sets giveaway and making 500m DH set... Join Zisspire, earn Zeny, collect prizes!",
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-502d7c865c5e3a54-300x300.jpeg",
        "teams": [ ],
        "url": "http://www.twitch.tv/test_channel",
        "display_name": "test_channel",
        "game": "Diablo III",
        "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_header_image-997348d7f0658115-640x125.jpeg",
        "name": "test_channel",
        "video_banner": null,
        "_links": {
          "chat": "https://api.twitch.tv/kraken/chat/test_channel",
          "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
          "features": "https://api.twitch.tv/kraken/channels/test_channel/features",
          "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
          "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
          "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
          "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos",
          "self": "https://api.twitch.tv/kraken/channels/test_channel",
          "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows"
        },
        "created_at": "2012-07-01T21:09:58Z"
      },
      "name": "live_user_test_channel",
      "viewers": 775,
      "_links": {
        "self": "https://api.twitch.tv/kraken/streams/test_channel"
      }
    },
    ...
  ]
}
```
