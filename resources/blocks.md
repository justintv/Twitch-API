# Blocks (Unstable)

**Warning:** This API method is currently experimental and the format may change without warning.

### Get a list of blocked users

`GET /users/:login/blocks`

_Authenticated_, required scope: `user_blocks_read`

#### Response

```json
{
  "blocks": [
    {
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/hebo/blocks/funami"
      },
      "user": {
        "name": "funami",
        "created_at": "2011-05-01T14:50:12Z",
        "updated_at": "2012-10-13T18:18:43Z",
        "_id": 22125774,
        "_links": {
          "self": "https://api.twitch.tv/kraken/users/funami"
        },
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/funami-profile_image-9bd02ad8f4f5bc97-300x300.jpeg",
        "staff": false,
        "display_name": "Funami"
      }
    }
  ],
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/hebo/blocks"
  }
}
```

### Block a user

`PUT /users/:user/blocks/:target`

_Authenticated_, required scope: `user_blocks_edit`

In the above path, `:user` is the authenticated user's name and `:target` is the login of the user to be blocked

#### Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/hebo/blocks/funami"
  },
  "user": {
    "name": "funami",
    "created_at": "2011-05-01T14:50:12Z",
    "updated_at": "2012-10-13T18:18:43Z",
    "staff": false,
    "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/funami-profile_image-9bd02ad8f4f5bc97-300x300.jpeg",
    "_id": 22125774,
    "_links": {
      "self": "https://api.twitch.tv/kraken/users/funami"
    },
    "display_name": "Funami"
  }
}
```

### Unblock a user

`DELETE /users/:user/blocks/:target`

_Authenticated_, required scope: `user_blocks_edit`

In the above path, `:user` is the authenticated user's name and `:target` is the login of the user to be blocked

#### Response

`204 No Content` if successful.
