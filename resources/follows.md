# Follows

### Get a list of followed channels

`GET /users/:user/follows/channels`

### Parameters

- `limit` (optional): The maximum number of channels to return, up to 100.
- `offset` (optional): The offset to begin listing channels, defaults to 0.

#### Response

```json
{
  "_links": {
    "next": "https://api.twitch.tv/kraken/users/hebo/follows/channels?limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/users/hebo/follows/channels?limit=25&offset=0"
  },
  "follows": [
    {
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/hebo/follows/channels/elsmurfoz"
      },
      "channel": {
        "banner": null,
        "_id": 1,
        "url": "http://www.twitch.tv/elsmurfoz",
        "mature": null,
        "teams": [

        ],
        "status": null,
        "logo": null,
        "name": "elsmurfoz",
        "video_banner": null,
        "display_name": "Elsmurfoz",
        "created_at": "2007-05-22T10:37:47Z",
        "game": null,
        "_links": {
          "stream_key": "https://api.twitch.tv/kraken/channels/elsmurfoz/stream_key",
          "self": "https://api.twitch.tv/kraken/channels/elsmurfoz",
          "videos": "https://api.twitch.tv/kraken/channels/elsmurfoz/videos",
          "commercial": "https://api.twitch.tv/kraken/channels/elsmurfoz/commercial",
          "chat": "https://api.twitch.tv/kraken/chat/elsmurfoz",
          "features": "https://api.twitch.tv/kraken/channels/elsmurfoz/features"
        },
        "updated_at": "2008-02-12T06:04:29Z",
        "background": null
      }
    },
    ...
  ]
}
```

## Get specified channel's followers

`GET /channels/:channel/follows`

Returns an array of users who follow the specified channel.

### Parameters

- `limit` (optional): The maximum number of games to return, up to 100.
- `offset` (optional): The offset to begin listing games, defaults to 0.

### Example Request

```bash
curl -i -H https://api.twitch.tv/kraken/channels/kraken_test_user1/follows
```

### Response

```json
{
  "_links": {
    "next": "https://api.twitch.tv/kraken/channels/kraken_test_user1/follows?limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/channels/kraken_test_user1/follows?limit=25&offset=0"
  },
  "follows": [
    {
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/kraken_test_user2/follows/channels/kraken_test_user1"
      },
      "user": {
        "_links": {
          "self": "https://api.twitch.tv/kraken/users/kraken_test_user2"
        },
        "staff": false,
        "logo": null,
        "display_name": "kraken_test_user2",
        "created_at": "2013-02-06T21:21:57Z",
        "updated_at": "2013-02-13T20:59:42Z",
        "_id": 40091581,
        "name": "kraken_test_user2"
      }
    },
    ...
  ]
}
```

### Get the status of a follow relationship

`GET /users/:user/follows/channels/:target`

In the above path, `:user` is the name of the user to check and `:target` is the name of the target channel.

#### Response

If the user is not following the channel:

    404 Not Found

If the user is following the channel:

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/hebo/follows/channels/funami"
  },
  "channel": {
    "name": "funami",
    "game": null,
    "created_at": "2011-05-01T14:50:12Z",
    "teams": [],
    "background": null,
    "updated_at": "2012-10-13T18:18:43Z",
    "banner": null,
    "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/funami-profile_image-9bd02ad8f4f5bc97-300x300.jpeg",
    "url": "http://www.twitch.tv/funami",
    "_links": {
      "stream_key": "https://api.twitch.tv/kraken/channels/funami/stream_key",
      "self": "https://api.twitch.tv/kraken/channels/funami",
      "chat": "https://api.twitch.tv/kraken/chat/funami",
      "commercial": "https://api.twitch.tv/kraken/channels/funami/commercial",
      "videos": "https://api.twitch.tv/kraken/channels/funami/videos",
      "features": "https://api.twitch.tv/kraken/channels/funami/features"
    },
    "_id": 22125774,
    "mature": true,
    "video_banner": null,
    "display_name": "Funami",
    "status": "Not Live"
  }
}
```

### Follow a user

`PUT /users/:user/follows/channels/:target`

_Authenticated_, require scope: `user_follows_edit`

In the above path, `:user` is the authenticated user's name and `:target` is the name of the channel to be followed.

#### Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/hebo/follows/channels/funami"
  },
  "channel": {
    "name": "funami",
    "game": null,
    "created_at": "2011-05-01T14:50:12Z",
    "teams": [],
    "background": null,
    "updated_at": "2012-10-13T18:18:43Z",
    "banner": null,
    "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/funami-profile_image-9bd02ad8f4f5bc97-300x300.jpeg",
    "_links": {
      "stream_key": "https://api.twitch.tv/kraken/channels/funami/stream_key",
      "self": "https://api.twitch.tv/kraken/channels/funami",
      "chat": "https://api.twitch.tv/kraken/chat/funami",
      "commercial": "https://api.twitch.tv/kraken/channels/funami/commercial",
      "videos": "https://api.twitch.tv/kraken/channels/funami/videos",
      "features": "https://api.twitch.tv/kraken/channels/funami/features"
    },
    "url": "http://www.twitch.tv/funami",
    "_id": 22125774,
    "mature": true,
    "video_banner": null,
    "display_name": "Funami",
    "status": "Not Live"
  }
}
```

### Unfollow a user

`DELETE /users/:user/follows/channels/:target`

_Authenticated_, required scope: `user_follows_edit`

In the above path, `:user` is the authenticated user's name and `:target` is the name of the channel to be followed.

#### Response

`204 No Content` if successful.
