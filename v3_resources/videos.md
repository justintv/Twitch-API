# Videos

***

Videos are broadcasts or chapters owned by a [channel][channels]. Broadcasts are unedited videos that are saved after a streaming session. Chapters are videos edited from broadcasts by the channel's owner.

| Endpoint | Description |
| ---- | --------------- |
| [GET /videos/:id](/v3_resources/videos.md#get-videosid) | Get video object|
| [GET /videos/top](/v3_resources/videos.md#get-videostop) | Get top videos by number of views |
| [GET /channels/:channel/videos](/v3_resources/videos.md#get-channelschannelvideos) | Get list of video objects belonging to channel |

[channels]: /v3_resources/channels.md

## `GET /videos/:id/`

Returns a video object.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/videos/a328087483
```

### Example Response

```json
{
  "recorded_at": "2012-08-09T20:49:47Z",
  "title": "VanillaTV - Sweden vs Russia - ETF2L Nations Cup - Snakewater [Map3] - Part 3",
  "url": "http://www.twitch.tv/vanillatv/b/328087483",
  "_id": "a328087483",
  "_links": {
      "self": "https://api.twitch.tv/kraken/videos/a328087483",
      "owner": "https://api.twitch.tv/kraken/channels/vanillatv"
  },
  "views": 93,
  "description": "VanillaTV - Sweden vs Russia - ETF2L Nations Cup - Snakewater [Map3] - Part 3",
  "length": 204,
  "game": null,
  "preview": "http://static-cdn.jtvnw.net/jtv.thumbs/archive-328087483-320x240.jpg"
}
```

## `GET /videos/top`

Returns a list of videos created in a given time period sorted by number of views, most popular first.

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>limit</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Maximum number of objects in array. Default is 25. Maximum is 100.</td>
        </tr>
        <tr>
            <td><code>offset</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Object offset for pagination. Default is 0.</td>
        </tr>
        <tr>
            <td><code>game</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Returns only videos from <code>game</code>.</td>
        </tr>
        <tr>
            <td><code>period</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Returns only videos created in time period. Valid values are <code>week</code>, <code>month</code>, or <code>all</code>. Default is <code>week</code>.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/videos/top?game=League+of+Legends&period=month
```

### Example Response

```json
{
  "_links": {
    "next": "https://api.twitch.tv/kraken/videos/top?game=League+of+Legends&limit=10&offset=10&period=month",
    "self": "https://api.twitch.tv/kraken/videos/top?game=League+of+Legends&limit=10&offset=0&period=month"
  },
  "videos": [
    {
      "recorded_at": "2013-03-13T09:51:31Z",
      "preview": "http://static-cdn.jtvnw.net/jtv.thumbs/archive-377199700-320x240.jpg",
      "description": "dat trist jump",
      "url": "http://www.twitch.tv/chaoxlol/c/2023831",
      "title": "Almost the great escape",
      "channel": {
        "name": "chaoxlol",
        "display_name": "chaoxlol"
      },
      "length": 71,
      "game": "League of Legends",
      "views": 66436,
      "_id": "c2023831",
      "_links": {
        "channel": "https://api.twitch.tv/kraken/channels/chaoxlol",
        "self": "https://api.twitch.tv/kraken/videos/c2023831"
      }
    },
    ...
  ]
}
```

## `GET /channels/:channel/videos`

Returns an list of videos ordered by time of creation, starting with the most recent from `:channel`.

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>limit</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Maximum number of objects in array. Default is 25. Maximum is 100.</td>
        </tr>
        <tr>
            <td><code>offset</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Object offset for pagination. Default is 0.</td>
        </tr>
        <tr>
            <td><code>broadcasts</code></td>
            <td>optional</td>
            <td>bool</td>
            <td>Returns only broadcasts when <code>true</code>. Otherwise only highlights are returned. Default is <code>false</code>.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/channels/vanillatv/videos?limit=10
```

### Example Response

```json
{
  "videos": [
      {
          "title": "ETF2L Week 1: Epsilon vs. Dignitas",
          "recorded_at": "2011-10-02T19:57:06Z",
          "_id": "a296529186",
          "_links": {
              "self": "https://api.twitch.tv/kraken/videos/a296529186",
              "owner": "https://api.twitch.tv/kraken/channels/vanillatv"
          },
          "url": "http://www.twitch.tv/vanillatv/b/296529186",
          "views": 1,
          "preview": "http://static-cdn.jtvnw.net/jtv.thumbs/archive-296529186-320x240.jpg",
          "length": 23,
          "game": "Team Fortress 2"
          "description": null
      },
      {
          "title": "ETF2L Week 1: Epsilon vs. Dignitas",
          "recorded_at": "2011-10-02T19:01:23Z",
          "_id": "a296526250",
          "_links": {
              "self": "https://api.twitch.tv/kraken/videos/a296526250",
              "owner": "https://api.twitch.tv/kraken/channels/vanillatv"
          },
          "url": "http://www.twitch.tv/vanillatv/b/296526250",
          "views": 1,
          "preview": "http://static-cdn.jtvnw.net/jtv.thumbs/archive-296526250-320x240.jpg",
          "length": 1296,
          "game": "Team Fortress 2",
          "description": null
      },
      ...
  ],
  "_links": {
      "self": "https://api.twitch.tv/kraken/channels/vanillatv/videos?limit=10&offset=0",
      "next": "https://api.twitch.tv/kraken/channels/vanillatv/videos?limit=10&offset=10"
  }
}
```

## Embedding

[See here for embedding.][embedding]

[embedding]: /embedding.md#embedding-streams-vods-and-chat
