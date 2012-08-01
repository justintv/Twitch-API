# Channels

## Get the specified channel

`GET /channels/:channel/`

### Response

    {
      "name": "towelliee",
      "game": "World of Warcraft: Cataclysm",
      "created_at": "2011-02-24T01:38:43Z",
      "teams": [{
        "name": "tgn",
        "created_at": "2011-12-23T06:30:14Z",
        "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-tgn-background_image-1d969c0af8187732.jpeg",
        "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-tgn-banner_image-f221dbf018f33148-640x125.png",
        "updated_at": "2012-04-25T17:30:49Z",
        "_id": 134,
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-tgn-team_logo_image-b710eca274634d81-300x300.png",
        "_links": {
          "self": "https://api.twitch.tv/kraken/teams/tgn"
        },
        "info": "Building a career path for YouTubers! See http://tgn.tv\n\n",
        "display_name": "TGN"
      }],
      "title": "Towelliee HD Gaming",
      "updated_at": "2012-06-18T05:22:53Z",
      "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/towelliee-channel_header_image-7d10ec1bfbef2988-640x125.png",
      "_links": {
        "self": "https://api.twitch.tv/kraken/channels/towelliee",
        "chat": "https://api.twitch.tv/kraken/chat/towelliee",
        "commercial": "https://api.twitch.tv/kraken/channels/towelliee/commercial"
      },
      "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/towelliee-profile_image-7243b004a2ec3720-300x300.png",
      "_id": 20694610,
      "mature": true,
      "display_name": "Towelliee"
    }
## Get the authenticated channel

`GET /channel`

(*Authenticated, Scope:channel_read*) Get the channel associated with the authenticated user. Includes the channel stream key.

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
      "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/towelliee-channel_header_image-7d10ec1bfbef2988-640x125.png",
      "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/towelliee-profile_image-7243b004a2ec3720-300x300.png",
      "id": 21229404,
      "mature": false,
      "login": "hebo",
      "email": "james@justin.tv"
    }

## Update the specified channel

`PUT /channels/:channel/`

(Authenticated, Scope:channel_editor)

### Parameters

Form-encoded or JSON parameters specifying the properties to change. At present, the following properties are supported:

- `status` 
- `game`  

&nbsp;

    {
        "channel": {
        "status": "Playing cool new game!",
        "game": "Diablo"
        }
    }

### Response

`200 OK` with the updated channel object if successful.

## Run a commercial on the specified channel

`POST /channels/:channel/commercial`

(Authenticated, Scope:channel_commercial)

### Parameters

  -`length` (**Default: 30**): Length of the commercial break in seconds from 30 to 90. You may only trigger a commercial longer than 30 seconds once every 15 minutes.

### Response

`204 No Content` if successful.