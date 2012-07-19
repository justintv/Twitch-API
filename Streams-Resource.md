# Streams

## Get the specified channel's stream

`GET /streams/:channel/`

### Response

`200 OK` with an empty array if the channel is not currently live

`200 OK` with the stream object if the channel is currently live

    [{
      "game": "StarCraft II: Wings of Liberty",
      "name": "live_user_eg_idra",
      "created_at": "Thu Jul 19 10:47:15 2012",
      "channel_id": 15769195,
      "updated_at": "Thu Jul 19 14:21:58 2012",
      "viewers": 10583,
      "_id": 171375380,
      "_links": {
        "self": "https://api.twitch.tv/kraken/streams/live_user_eg_idra"
      },
      "delay_length": 0,
      "broadcaster": "fme",
      "geo": "US",
      "channel": {
        "name": "eg_idra",
        "game": "StarCraft II: Wings of Liberty",
        "created_at": "2010-09-19T11:16:48Z",
        "teams": [{
          "name": "eg",
          "created_at": "2011-10-11T23:59:43Z",
          "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-banner_image-8089b058e6ffe4cd-640x125.png",
          "updated_at": "2012-01-15T19:43:40Z",
          "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-background_image-089a407eb59fe3b2.png",
          "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-team_logo_image-53eaf029dad7d5c9-300x300.png",
          "_id": 2,
          "_links": {
            "self": "https://api.twitch.tv/kraken/teams/eg"
          },
          "info": "Team Info\n",
          "display_name": "Evil Geniuses"
        }, {
          "name": "omgtv",
          "created_at": "2012-01-15T19:41:46Z",
          "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-omgtv-banner_image-63324444323bb5f8-640x125.png",
          "updated_at": "2012-01-16T23:39:30Z",
          "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-omgtv-background_image-fcd3992cd0294280.jpeg",
          "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-omgtv-team_logo_image-9e400bef45ccb191-300x300.png",
          "_id": 158,
          "_links": {
            "self": "https://api.twitch.tv/kraken/teams/omgtv"
          },
          "info": "This is the listing page for all the streams of the amazing people involved with OneMoreGame.TV!  From our show hosts to our production and site staff, check out their personal streams if you dare!\n\n\n",
          "display_name": "OneMoreGame.TV Crew"
        }],
        "updated_at": "2012-07-19T17:47:16Z",
        "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/eg_idra-channel_header_image-c195fd4d66ded5b7-640x125.jpeg",
        "_links": {
          "stream_key": "https://api.twitch.tv/kraken/channels/eg_idra/stream_key",
          "self": "https://api.twitch.tv/kraken/channels/eg_idra",
          "chat": "https://api.twitch.tv/kraken/chat/eg_idra",
          "commercial": "https://api.twitch.tv/kraken/channels/eg_idra/commercial",
          "features": "https://api.twitch.tv/kraken/channels/eg_idra/features"
        },
        "_id": 15769195,
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/eg_idra-profile_image--300x300.",
        "mature": null,
        "display_name": "EG_IdrA",
        "status": "Starcraft 2 [720p] w/ EG Idra"
      },
      "status": "Starcraft 2 [720p] w/ EG Idra",
      "partner": true
    }]
