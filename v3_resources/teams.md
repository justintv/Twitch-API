# Teams

***

Teams are an organization of [channels][channels].

| Endpoint | Description |
| ---- | --------------- |
| [GET /teams](/v3_resources/teams.md#get-teams) | Get list of active team objects |
| [GET /teams/:team](/v3_resources/teams.md#get-teamsteam) | Get team object |

[channels]: /v3_resources/channels.md

## `GET /teams/`

Returns a list of active teams.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/teams
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
      "info": "<p>Team Info</p>",
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
    ...
  ]
}
```

## `GET /teams/:team/`

Returns a team object for `:team`.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/teams/eg
```

### Example Response

```json
{
  "info": "<p>Team Info</p>",
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
}
```
