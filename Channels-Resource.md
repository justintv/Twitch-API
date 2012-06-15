
# Channels

## Get the specified channel

`GET /channels/:channel/`

### Response

    {
      "game": "World of Warcraft: Mists of Pandaria",
      "_id": 20694610,
      "created_at": "2011-02-24T01:38:43Z",
      "mature": true,
      "updated_at": "2012-04-02T17:46:23Z",
      "title": "Towelliee HD Gaming",
      "teams": [{
        "_id": 134,
        "created_at": "2011-12-23T06:30:14Z",
        "updated_at": "2012-01-08T23:48:52Z",
        "info": "Building a career path for YouTubers! See http://tgn.tv\n\n",
        "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-tgn-background_image-6c4e34a8def09253.jpeg",
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-tgn-team_logo_image-d2b677d4f1ecc008-300x300.png",
        "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-tgn-banner_image-8607f365e2d69e22-640x125.png",
        "_links": {
          "self": "https://api.twitch.tv/kraken/teams/tgn"
        },
        "display_name": "TGN",
        "name": "tgn"
      }],
      "_links": {
        "self": "https:/api.twitch.tv/kraken/channels/towelliee",
        "chat":"https:/api.twitch.tv/kraken/chat/towelliee",
        "commercial":"https:/api.twitch.tv/kraken/channels/towelliee/commercial"
      },
      "display_name": "Towelliee",
      "name": "towelliee"
    }

## Get the authenticated channel

`GET /channel`

(*Authenticated, Scope:channel*) Get the channel associated with the authenticated user. Includes the channel stream key.

    {
      "game": "Diablo II: Lord of Destruction",
      "name": "Hebo",
      "stream_key": "live_21229404_abcdefg",
      "created_at": "2011-03-19T15:42:22Z",
      "title": "Cev",
      "updated_at": "2012-03-14T03:30:41Z",
      "teams": [{
        "name": "staff",
        "created_at": "2011-10-25T23:55:47Z",
        "updated_at": "2011-11-14T19:48:21Z",
        "background": null,
        "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-staff-banner_image-1e028d6b6aec8e6a-640x125.jpeg",
        "logo": null,
        "_links": {
          "self": "https://api.twitch.tv/kraken/teams/staff"
        },
        "_id": 10,
        "info": "We save the world..",
        "display_name": "TwitchTV Staff"
      }],
      "_links": {
        "self": "https:/api.twitch.tv/kraken/channels/hebo",
        "chat":"https:/api.twitch.tv/kraken/chat/hebo",
        "commercial":"https:/api.twitch.tv/kraken/channels/hebo/commercial"
      },
      "id": 21229404,
      "mature": false,
      "login": "hebo",
      "email": "james@justin.tv"
    }

## Update the specified channel

`PATCH /channel`

(**Not implemented**)

## Run a commercial on the specified channel

`POST /channels/:channel/commercial`

### Parameters

  -`length` (**Default: 30**): Length of the commercial break in seconds from 30 to 90. You may only trigger a commercial longer than 30 seconds once every 15 minutes.

### Response

`204 No Content` if successful.