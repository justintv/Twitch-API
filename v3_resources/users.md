# Users

These are members of the Twitch community who have a Twitch account. If broadcasting, they can own a [stream][streams] that they can broadcast on their [channel][channels]. If mainly viewing, they might [follow][follows] or [subscribe][subscriptions] to channels.

| Endpoint | Description |
| ---- | --------------- |
| [GET /users/:user](/v3_resources/users.md#get-usersuser) | Get user object |
| [GET /user](/v3_resources/users.md#get-user) | Get user object |
| [GET /streams/followed](/v3_resources/users.md#get-streamsfollowed) | Get list of streams user is following |
| [GET /videos/followed](/v3_resources/users.md#get-videosfollowed) | Get list of videos belonging to channels user is following |

[streams]: /v3_resources/streams.md
[channels]: /v3_resources/channels.md
[follows]: /v3_resources/follows.md
[subscriptions]: /v3_resources/subscriptions.md

## `GET /users/:user`

Returns a user object.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/users/test_user1
```

### Example Response

```json
{
  "type": "user",
  "name": "test_user1",
  "created_at": "2011-03-19T15:42:22Z",
  "updated_at": "2012-06-14T00:14:27Z",
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/test_user1"
  },
  "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_user1-profile_image-6947308654ad603f-300x300.jpeg",
  "_id": 21229404,
  "display_name": "test_user1",
  "bio": "test bio woo I'm a test user"
}
```

## `GET /user`

Returns a user object.

*__Authenticated__*, required scope: `user_read`

*__Gotcha__* If the user's Twitch registered Email Address is not verified, 'null' will be returned.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/user
```

### Example Response

```json
{
  "type": "user",
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
  "partnered": true,
  "bio": "test bio woo I'm a test user",
  "notifications": {
    "email": true,
    "push": false
  }
}
```

## `GET /streams/followed`

Returns a list of stream objects that the authenticated user is following.

*__Authenticated__*, required scope: `user_read`

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
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/streams/followed
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/streams/followed?limit=25&offset=0",
    "next": "https://api.twitch.tv/kraken/streams/followed?limit=25&offset=25"
  },
  "_total": 123,
  "streams": [...]
}
```

## `GET /videos/followed`

Returns a list of video objects from channels that the authenticated user is following.

*__Authenticated__*, required scope: `user_read`

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
            <td>Maximum number of objects in array. Default is 10. Maximum is 100.</td>
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
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/videos/followed
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/videos/followed?limit=10&offset=0",
    "next": "https://api.twitch.tv/kraken/videos/followed?limit=10&offset=25"
  },
  "videos": [...]
}
```
