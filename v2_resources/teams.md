# Teams

***

Teams are an organization of [channels][channels].

| Endpoint | Description |
| ---- | --------------- |
| [GET /teams](/v2_resources/teams.md#get-teams) | Get list of active team objects |
| [GET /teams/:team](/v2_resources/teams.md#get-teamsteam) | Get team object |

[channels]: /v2_resources/channels.md

## `GET /teams/`

Returns a list of active teams.

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/teams
```

### Example Response

```json
{
  "_links": {
    "next": "https://api.twitch.tv/kraken/teams?limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/teams?limit=25&offset=0"
  },
  "teams": [
    {
      "info": "I love working for Twitch!\n\n",
      "_links": {
        "self": "https://api.twitch.tv/kraken/teams/testteam"
      },
      "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-testteam-background_image-c72e038f428c9c7d.png",
      "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-testteam-banner_image-cc318b0f084cb67c-640x125.jpeg",
      "name": "testteam",
      "_id": 1,
      "updated_at": "2012-11-14T01:30:00Z",
      "display_name": "test",
      "created_at": "2011-10-11T22:49:05Z",
      "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-testteam-team_logo_image-46943237490be5e7-300x300.jpeg"
    },
    {
      "info": "Team Info\n",
      "_links": {
        "self": "https://api.twitch.tv/kraken/teams/eg"
      },
      "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-background_image-da36973b6d829ac6.png",
      "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-banner_image-1ad9c4738f4698b1-640x125.png",
      "name": "eg",
      "_id": 2,
      "updated_at": "2012-10-03T01:48:25Z",
      "display_name": "Evil Geniuses",
      "created_at": "2011-10-11T23:59:43Z",
      "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-team_logo_image-9107b874d4c3fc3b-300x300.jpeg"
    },
    ...
  ]
}
```

## `GET /teams/:team/`

Returns a team object for `:team`.

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/teams/eg
```

### Example Response

```json
{
  "_id": 2,
  "created_at": "2011-10-11T23:59:43Z",
  "info": "Team Info\n",
  "updated_at": "2012-01-15T19:43:40Z",
  "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-background_image-089a407eb59fe3b2.png",
  "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-banner_image-8089b058e6ffe4cd-640x125.png",
  "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-team_logo_image-53eaf029dad7d5c9-300x300.png",
  "_links": {
    "self": "https://api.twitch.tv/kraken/teams/eg"
  },
  "display_name": "Evil Geniuses",
  "name": "eg"
}
```
