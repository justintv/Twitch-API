# Users

## Get a single user

`GET /users/:user`

### Response

    {
      "_id": 21229404,
      "created_at": "2011-03-19T15:42:22Z",
      "updated_at": "2012-03-30T20:20:36Z",
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/hebo"
      },
      "display_name": "Hebo",
      "name": "hebo"
    }

## Get the authenticated user

`GET /user`

(*Authenticated, Scope:user_read*)

### Response

    {
      "_id": 22765025,
      "created_at": "2011-06-03T22:01:03Z",
      "email": "james+test15@justin.tv",
      "updated_at": "2012-02-07T02:24:32Z",
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/cevtest15"
      },
      "display_name": "Cevtest15",
      "name": "cevtest15"
    }

## Update the specified user.

`PATCH /user/:user/`

(**Not implemented** *Authenticated, Scope:user*)
