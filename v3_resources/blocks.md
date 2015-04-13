# Blocks

Stores and updates information about a [user's][users] block list.

| Endpoint | Description |
| ---- | --------------- |
| [GET /users/:login/blocks](/v3_resources/blocks.md#get-usersloginblocks) | Get user's block list |
| [PUT /users/:user/blocks/:target](/v3_resources/blocks.md#put-usersuserblockstarget) | Add target to user's block list |
| [DELETE /users/:user/blocks/:target](/v3_resources/blocks.md#delete-usersuserblockstarget) | Delete target from user's block list |

[users]: /v3_resources/users.md

## `GET /users/:user/blocks`

Returns a list of blocks objects on `:user`'s block list. List sorted by recency, newest first.

*__Authenticated__*, required scope: `user_blocks_read`

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
-X GET https://api.twitch.tv/kraken/users/test_user1/blocks
```

### Example Response

```json
{
  "_links": {
    "next": "https://api.twitch.tv/kraken/users/test_user1/test_user1?limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/users/test_user1/test_user1?limit=25&offset=0"
  },
  "blocks": [
    {
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/test_user1/blocks/test_user_troll"
      },
      "updated_at": "2013-02-07T01:04:43Z",
      "user": {
        "_links": {
          "self": "https://api.twitch.tv/kraken/users/test_user_troll"
        },
        "updated_at": "2013-02-06T22:44:19Z",
        "display_name": "test_user_troll",
        "type": "user",
        "bio": "I'm a troll.. Kappa",
        "name": "test_user_troll",
        "_id": 13460644,
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_user_troll-profile_image-9e4de45c9e6744ac-300x300.png",
        "created_at": "2010-06-30T08:26:49Z"
      },
      "_id": 970887
    },
    ...
  ]
}
```

## `PUT /users/:user/blocks/:target`

Adds `:target` to `:user`'s block list. `:user` is the authenticated user and `:target` is user to be blocked. Returns a blocks object.

*__Authenticated__*, required scope: `user_blocks_edit`

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X PUT https://api.twitch.tv/kraken/users/test_user1/blocks/test_user_troll
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/test_user1/blocks/test_user_troll"
  },
  "updated_at": "2013-02-07T01:04:43Z",
  "user": {
    "_links": {
      "self": "https://api.twitch.tv/kraken/users/test_user_troll"
    },
    "updated_at": "2013-01-18T22:33:55Z",
    "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_user_troll-profile_image-c3fa99f314dd9477-300x300.jpeg",
    "type": "user",
    "bio": "I'm a troll.. Kappa",
    "display_name": "test_user_troll",
    "name": "test_user_troll",
    "_id": 22125774,
    "created_at": "2011-05-01T14:50:12Z"
  },
  "_id": 287813
}
```

## `DELETE /users/:user/blocks/:target`

Removes `:target` from `:user`'s block list. `:user` is the authenticated user and `:target` is user to be unblocked.

*__Authenticated__*, required scope: `user_blocks_edit`

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X DELETE https://api.twitch.tv/kraken/users/test_user1/blocks/test_user_troll
```

### Example Response

`204 No Content` if successful.

### Errors

`404 Not Found` if `:target` not on `:user`'s block list.

`422 Unprocessable Entity` if delete failed.
