# Follows

Status of follow relationships between [users][users] and [channels][channels].

| Endpoint | Description |
| ---- | --------------- |
| [GET /channels/:channel/follows](/v2_resources/follows.md#get-channelschannelfollows) | Get channel's list of following users |
| [GET /users/:user/follows/channels](/v2_resources/follows.md#get-usersuserfollowschannels) | Get a user's list of followed channels |
| [GET /users/:user/follows/channels/:target](/v2_resources/follows.md#get-usersuserfollowschannelstarget) | Get status of follow relationship between user and target channel |
| [PUT /users/:user/follows/channels/:target](/v2_resources/follows.md#put-usersuserfollowschannelstarget) | Follow a channel |
| [DELETE /users/:user/follows/channels/:target](/v2_resources/follows.md#delete-usersuserfollowschannelstarget) | Unfollow a channel |
| [GET /streams/followed](/v2_resources/users.md#get-streamsfollowed) | Get a list of streams user is following |

[users]: /v2_resources/users.md
[channels]: /v2_resources/channels.md

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
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v2+json' \
-X GET https://api.twitch.tv/kraken/channels/test_user1/follows
```

### Example Response

```json
{
  "_links": {
    "next": "https://api.twitch.tv/kraken/channels/test_user1/follows?limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/channels/test_user1/follows?limit=25&offset=0"
  },
  "follows": [
    {
      "created_at": "2015-02-12T01:13:35Z",
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/test_user2/follows/channels/test_user1"
      },
      "notifications": true,
      "user": {
        "_links": {
          "self": "https://api.twitch.tv/kraken/users/test_user2"
        },
        "staff": false,
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
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v2+json' \
-X GET https://api.twitch.tv/kraken/users/test_user1/follows/channels
```

### Example Response

```json
{
  "_links": {
    "next": "https://api.twitch.tv/kraken/users/test_user1/follows/channels?limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/users/test_user1/follows/channels?limit=25&offset=0"
  },
  "follows": [
    {
      "created_at": "2015-02-07T07:36:33Z",
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel"
      },
      "notifications": true,
      "channel": {
        "banner": null,
        "_id": 123456,
        "url": "http://www.twitch.tv/test_channel",
        "teams": [],
        "status": null,
        "logo": null,
        "name": "test_channel",
        "video_banner": null,
        "mature": false,
        "display_name": "test_channel",
        "created_at": "2007-05-22T10:37:47Z",
        "game": null,
        "_links": {
          "self": "https://api.twitch.tv/kraken/channels/test_channel",
          "chat": "https://api.twitch.tv/kraken/chat/test_channel",
          "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos",
          "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
          "follows":"https://api.twitch.tv/kraken/channels/test_channel/follows",
          "stream_key":"https://api.twitch.tv/kraken/channels/test_channel/stream_key",
          "features":"https://api.twitch.tv/kraken/channels/test_channel/features",
          "subscriptions":"https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
          "editors":"https://api.twitch.tv/kraken/channels/test_channel/editors"
        },
        "updated_at": "2008-02-12T06:04:29Z",
        "background": null
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
curl -H 'Accept: application/vnd.twitchtv.v2+json' \
-X GET https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel
```

### Example Response

`404 Not Found` if user is not following channel.

Otherwise,

```json
{
  "created_at": "2015-02-07T07:36:33Z",
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel"
  },
  "notifications": true,
  "channel": {
    "name": "test_channel",
    "game": null,
    "created_at": "2011-05-01T14:50:12Z",
    "teams": [],
    "background": null,
    "updated_at": "2012-10-13T18:18:43Z",
    "banner": null,
    "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-9bd02ad8f4f5bc97-300x300.jpeg",
    "url": "http://www.twitch.tv/test_channel",
    "_links": {
      "self": "https://api.twitch.tv/kraken/channels/test_channel",
      "chat": "https://api.twitch.tv/kraken/chat/test_channel",
      "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos",
      "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
      "follows":"https://api.twitch.tv/kraken/channels/test_channel/follows",
      "stream_key":"https://api.twitch.tv/kraken/channels/test_channel/stream_key",
      "features":"https://api.twitch.tv/kraken/channels/test_channel/features",
      "subscriptions":"https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
      "editors":"https://api.twitch.tv/kraken/channels/test_channel/editors"
    },
    "_id": 22125774,
    "mature": true,
    "video_banner": null,
    "display_name": "test_channel",
    "status": "Not Live"
  }
}
```

## `PUT /users/:user/follows/channels/:target`

Adds `:user` to `:target`'s followers. `:user` is the authenticated user's name and `:target` is the name of the channel to be followed.

*__Authenticated__*, required scope: `user_follows_edit`

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v2+json' -H 'Authorization: OAuth <access_token>' \
-X PUT https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel
```

### Example Response

```json
{
  "created_at": "2015-02-07T07:36:33Z",
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel"
  },
  "notifications": true,
  "channel": {
    "name": "test_channel",
    "game": null,
    "created_at": "2011-05-01T14:50:12Z",
    "teams": [],
    "background": null,
    "updated_at": "2012-10-13T18:18:43Z",
    "banner": null,
    "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-9bd02ad8f4f5bc97-300x300.jpeg",
    "_links": {
      "self": "https://api.twitch.tv/kraken/channels/test_channel",
      "chat": "https://api.twitch.tv/kraken/chat/test_channel",
      "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos",
      "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
      "follows":"https://api.twitch.tv/kraken/channels/test_channel/follows",
      "stream_key":"https://api.twitch.tv/kraken/channels/test_channel/stream_key",
      "features":"https://api.twitch.tv/kraken/channels/test_channel/features",
      "subscriptions":"https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
      "editors":"https://api.twitch.tv/kraken/channels/test_channel/editors"
    },
    "url": "http://www.twitch.tv/test_channel",
    "_id": 22125774,
    "mature": true,
    "video_banner": null,
    "display_name": "test_channel",
    "status": "Not Live"
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
curl -H 'Accept: application/vnd.twitchtv.v2+json' -H 'Authorization: OAuth <access_token>' \
-X DELETE https://api.twitch.tv/kraken/users/test_user1/follows/channels/test_channel
```

### Example Response

`204 No Content` if successful.

### Errors

`422 Unprocessable Entity` if delete fails.

## `GET /streams/followed`

[See the Users resource][users]

[users]: /v2_resources/users.md
