# Users

***

These are members of the Twitch community who have a Twitch account. If broadcasting, they can own a [stream][streams] that they can broadcast on their [channel][channels]. If mainly viewing, they might [follow][follows] or [subscribe][subscriptions] to channels.

| Endpoint | Description |
| ---- | --------------- |
| [GET /users/:user](/v3_resources/users.md#get-usersuser) | Get user object |
| [GET /user](/v3_resources/users.md#get-user) | Get user object |
| [GET /streams/followed](/v3_resources/users.md#get-streamsfollowed) | Get list of streams user is following |

[streams]: /v3_resources/streams.md
[channels]: /v3_resources/channels.md
[follows]: /v3_resources/follows.md
[subscriptions]: /v3_resources/subscriptions.md

## `GET /users/:user`

Returns a user object.

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/test_user1
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
  "display_name": "test_user1"
}
```

## `GET /user`

Returns a user object.

*__Authenticated__*, required scope: `user_read`

### Example Request

```bash
curl -i -H 'Authorization: OAuth [access token]' https://api.twitch.tv/kraken/user
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
  "display_name": "test_user1",
  "email": "asdf@asdf.com",
  "partnered": true
}
```

## `GET /streams/followed`

Returns a list of stream objects that the authenticated user is following.

*__Authenticated__*, required scope: `user_read`

### Example Request

```bash
curl -i -H 'Authorization: OAuth [access token]' https://api.twitch.tv/kraken/streams/followed
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/streams/followed?limit=25&offset=0",
    "next": "https://api.twitch.tv/kraken/streams/followed?limit=25&offset=25"
  },
  "streams": [...]
}
```
