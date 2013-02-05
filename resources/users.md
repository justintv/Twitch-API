# Users

These are the users of Twitch! They own a [stream][streams] that they can broadcast on a [channel][channels].

[streams]: /resources/streams.md
[channels]: /resources/channels.md

## Get a single user

`GET /users/:user`

Returns a user's metadata.

### Response

```json
{
  "name": "hebo",
  "created_at": "2011-03-19T15:42:22Z",
  "updated_at": "2012-06-14T00:14:27Z",
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/hebo"
  },
  "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/hebo-profile_image-6947308654ad603f-300x300.jpeg",
  "_id": 21229404,
  "display_name": "Hebo"
}
```

## Get the authenticated user <a id="user"/>

`GET /user`

(*Authenticated, Scope:user_read*)

### Response

```json
{
  "name": "cevtest12",
  "created_at": "2011-06-03T17:49:19Z",
  "updated_at": "2012-06-18T17:19:57Z",
  "_links": {
    "self": "https://api.twitch.tv/kraken/users/cevtest12"
  },
  "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/cevtest12-profile_image-62e8318af864d6d7-300x300.jpeg",
  "_id": 22761313,
  "display_name": "Cevtest12",
  "email": "asdf@asdf.com",
  "partnered": true
}
```

## Update the specified user.

`PATCH /user/:user/`

(**Not implemented** *Authenticated, Scope:user*)
