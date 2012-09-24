# Blocks

## Get the list of users that the authenticated user has blocked

`GET /users/:login/blocks`

(*Authenticated, Scope:user_blocks_read*)

### Response

```json
[
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
},
...
]
```

## Block a user on behalf of the authenticated user

`PUT /users/:login/blocks/:user`

(*Authenticated, Scope:user_blocks_edit*)

## Unblock a user on behalf of the authenticated user

`DELETE /users/:login/blocks/:user`

(*Authenticated, Scope:user_blocks_edit*)
