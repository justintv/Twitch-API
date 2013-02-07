# Blocks

Stores and updates information about a [user's][users] block list.

[users]: /resources/users.md

### Get a list of blocked users

`GET /users/:login/blocks`

_Authenticated_, required scope: `user_blocks_read`

Returns an array of users on the authenticated user's block list. This is sorted by recency (newest blocks first).

#### Example Response

```bash
curl -i https://api.twitch.tv/kraken/users/hebo/blocks
```

#### Response

```json
{
  "_links": {
    "next": "https://api.twitch.tv/kraken/users/hebo/blocks?limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/users/hebo/blocks?limit=25&offset=0"
  },
  "blocks": [
    {
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/hebo/blocks/flarerdb"
      },
      "updated_at": "2013-02-07T01:04:43Z",
      "user": {
        "_links": {
          "self": "https://api.twitch.tv/kraken/users/flarerdb"
        },
        "updated_at": "2013-02-06T22:44:19Z",
        "display_name": "FlareRDB",
        "staff": false,
        "name": "flarerdb",
        "_id": 13460644,
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/flarerdb-profile_image-9e4de45c9e6744ac-300x300.png",
        "created_at": "2010-06-30T08:26:49Z"
      },
      "_id": 970887
    }
  ]
}
```

### Block a user

`PUT /users/:user/blocks/:target`

_Authenticated_, required scope: `user_blocks_edit`

Adds user to authenticated user's block list. In the above path, `:user` is the authenticated user's name and `:target` is the name of the user to be blocked.

#### Example Request

```bash
curl -i -X PUT https://api.twitch.tv/kraken/users/hebo/blocks/funami
```

#### Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/hebo/blocks/funami"
  },
  "updated_at": "2013-02-07T01:04:43Z",
  "user": {
    "_links": {
      "self": "https://api.twitch.tv/kraken/users/funami"
    },
    "updated_at": "2013-01-18T22:33:55Z",
    "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/funami-profile_image-c3fa99f314dd9477-300x300.jpeg",
    "staff": false,
    "display_name": "Funami",
    "name": "funami",
    "_id": 22125774,
    "created_at": "2011-05-01T14:50:12Z"
  },
  "_id": 287813
}
```

### Unblock a user

`DELETE /users/:user/blocks/:target`

_Authenticated_, required scope: `user_blocks_edit`

Removes user from authenticated user's block list. In the above path, `:user` is the authenticated user's name and `:target` is the login of the user to be blocked.

#### Example Request

```bash
curl -i -X DELETE https://api.twitch.tv/kraken/users/hebo/blocks/funami
```

#### Response

`204 No Content` if successful.
