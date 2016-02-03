# Channels

Channels serve as the home location for a [user's][users] content. Channels have a [stream][streams], can run commercials, store [videos][], display information and status, and have a customized page including banners and backgrounds.

| Endpoint | Description |
| ---- | --------------- |
| [GET /channels/:channel](/v3_resources/channels.md#get-channelschannel) | Get channel object|
| [GET /channel](/v3_resources/channels.md#get-channel) | Get channel object |
| [GET /channels/:channel/videos](/v3_resources/channels.md#get-channelschannelvideos) | Get channel's list of videos |
| [GET /channels/:channel/follows](/v3_resources/channels.md#get-channelschannelfollows) | Get channel's list of following users |
| [GET /channels/:channel/editors](/v3_resources/channels.md#get-channelschanneleditors) | Get channel's list of editors |
| [PUT /channels/:channel](/v3_resources/channels.md#put-channelschannel) | Update channel object |
| [DELETE /channels/:channel/stream_key](/v3_resources/channels.md#delete-channelschannelstream_key) | Reset channel's stream key |
| [POST /channels/:channel/commercial](/v3_resources/channels.md#post-channelschannelcommercial) | Start a commercial on channel |
| [GET /channels/:channel/teams](/v3_resources/channels.md#get-channelschannelteams) | Get list of teams channel belongs to |

[users]: /v3_resources/users.md
[streams]: /v3_resources/streams.md
[videos]: /v3_resources/videos.md

## `GET /channels/:channel/`

Returns a channel object.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/channels/test_channel
```

### Example Response

```json
{
  "mature": false,
  "status": "test status",
  "broadcaster_language": "en",
  "display_name": "test_channel",
  "game": "Gaming Talk Shows",
  "delay": null,
  "language": "en",
  "_id": 12345,
  "name": "test_channel",
  "created_at": "2007-05-22T10:39:54Z",
  "updated_at": "2015-02-12T04:15:49Z",
  "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-94a42b3a13c31c02-300x300.jpeg",
  "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_header_image-08dd874c17f39837-640x125.png",
  "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_offline_image-b314c834d210dc1a-640x360.png",
  "background": null,
  "profile_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_banner-6936c61353e4aeed-480.png",
  "profile_banner_background_color": "null",
  "partner": true,
  "url": "http://www.twitch.tv/test_channel",
  "views": 49144894,
  "followers": 215780,
  "_links": {
    "self": "https://api.twitch.tv/kraken/channels/test_channel",
    "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows",
    "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
    "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
    "chat": "https://api.twitch.tv/kraken/chat/test_channel",
    "features": "https://api.twitch.tv/kraken/channels/test_channel/features",
    "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
    "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
    "teams": "https://api.twitch.tv/kraken/channels/test_channel/teams",
    "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos"
  }
}
```

## `GET /channel`

Returns a channel object of authenticated user. Channel object includes stream key.

*__Authenticated__*, required scope: `channel_read`

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/channel
```

### Example Response

```json
{
  "mature": false,
  "status": "test status",
  "broadcaster_language": "en",
  "display_name": "test_channel",
  "game": "Gaming Talk Shows",
  "delay": null,
  "language": "en",
  "_id": 12345,
  "name": "test_channel",
  "created_at": "2007-05-22T10:39:54Z",
  "updated_at": "2015-02-12T04:15:49Z",
  "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-94a42b3a13c31c02-300x300.jpeg",
  "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_header_image-08dd874c17f39837-640x125.png",
  "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_offline_image-b314c834d210dc1a-640x360.png",
  "background": null,
  "profile_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_banner-6936c61353e4aeed-480.png",
  "profile_banner_background_color": "null",
  "partner": true,
  "url": "http://www.twitch.tv/test_channel",
  "views": 49144894,
  "followers": 215780,
  "_links": {
    "self": "https://api.twitch.tv/kraken/channels/test_channel",
    "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows",
    "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
    "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
    "chat": "https://api.twitch.tv/kraken/chat/test_channel",
    "features": "https://api.twitch.tv/kraken/channels/test_channel/features",
    "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
    "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
    "teams": "https://api.twitch.tv/kraken/channels/test_channel/teams",
    "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos"
  },
  "email": "test_channel@twitch.tv",
  "stream_key": "live_5439587_s8df7s9d7g6dsfggsdfg"
}
```

## `GET /channels/:channel/videos`

See the [Videos](videos.md#get-channelschannelvideos) resource.

## `GET /channels/:channel/follows`

See the [Follows](follows.md#get-channelschannelfollows) resource.

## `GET /channels/:channel/editors`

Returns a list of user objects who are editors of `:channel`.

*__Authenticated__*, required scope: `channel_read`

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/channels/test_channel/editors
```

### Example Response

```json
{
  "_links": {
    "self": "http://api.twitch.tv/kraken/channels/test_channel/editors"
  },
  "users": [
    {
      "_links": {
        "self": "http://staging.twitch.tv/kraken/users/test_channel_editor"
      },
      "created_at": "2013-02-06T21:21:57Z",
      "name": "test_channel_editor",
      "updated_at": "2013-02-13T20:59:42Z",
      "_id": 40091581,
      "display_name": "test_channel_editor",
      "logo": null,
      "type": "user",
      "bio": "I am a test editor"
    },
    ...
  ]
}
```

## `PUT /channels/:channel/`

Update channel's properties.

*__Authenticated__*, required scope: `channel_editor`

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
            <td><code>status</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Channel's title.</td>
        </tr>
        <tr>
            <td><code>game</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Game category to be classified as.</td>
        </tr>
        <tr>
            <td><code>delay</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Channel delay in seconds. Requires the channel owner's OAuth token.</td>
        </tr>
        <tr>
            <td><code>channel_feed_enabled</code></td>
            <td>optional</td>
            <td>boolean</td>
            <td>Whether the channel's feed is enabled. Requires the channel owner's OAuth token.</td>
        </tr>
    </tbody>
</table>

Form-encoded or JSON parameters specifying the properties to change. These should be under a `channel` object:

```json
{
  "channel": {
    "status": "Playing cool new game!",
    "game": "Diablo",
    "delay": 60,
    "channel_feed_enabled": false
    }
}
```

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-d "channel[status]=Playing+cool+new+game!&channel[game]=Diablo&channel[delay]=0" \
-X PUT https://api.twitch.tv/kraken/channels/test_channel
```

### Example Response

```json
{
  "mature": false,
  "status": "Playing cool new game!",
  "broadcaster_language": "en",
  "display_name": "test_channel",
  "game": "Diablo",
  "delay": null,
  "language": "en",
  "_id": 12345,
  "name": "test_channel",
  "created_at": "2007-05-22T10:39:54Z",
  "updated_at": "2015-02-12T04:15:49Z",
  "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-94a42b3a13c31c02-300x300.jpeg",
  "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_header_image-08dd874c17f39837-640x125.png",
  "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_offline_image-b314c834d210dc1a-640x360.png",
  "background": null,
  "profile_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_banner-6936c61353e4aeed-480.png",
  "profile_banner_background_color": "null",
  "partner": true,
  "url": "http://www.twitch.tv/test_channel",
  "views": 49144894,
  "followers": 215780,
  "_links": {
    "self": "https://api.twitch.tv/kraken/channels/test_channel",
    "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows",
    "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
    "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
    "chat": "https://api.twitch.tv/kraken/chat/test_channel",
    "features": "https://api.twitch.tv/kraken/channels/test_channel/features",
    "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
    "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
    "teams": "https://api.twitch.tv/kraken/channels/test_channel/teams",
    "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos"
  }
}
```

### Errors

`422 Unprocessable Entity` if trying to set `delay` for a channel that is not partnered.

## `DELETE /channels/:channel/stream_key`

Resets channel's stream key.

*__Authenticated__*, required scope: `channel_stream`

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X DELETE https://api.twitch.tv/kraken/channels/test_channel/stream_key
```

### Example Response

```json
{
  "mature": false,
  "status": "test status",
  "broadcaster_language": "en",
  "display_name": "test_channel",
  "game": "Gaming Talk Shows",
  "delay": null,
  "language": "en",
  "_id": 12345,
  "name": "test_channel",
  "created_at": "2007-05-22T10:39:54Z",
  "updated_at": "2015-02-12T04:15:49Z",
  "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_image-94a42b3a13c31c02-300x300.jpeg",
  "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_header_image-08dd874c17f39837-640x125.png",
  "video_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-channel_offline_image-b314c834d210dc1a-640x360.png",
  "background": null,
  "profile_banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/test_channel-profile_banner-6936c61353e4aeed-480.png",
  "profile_banner_background_color": "null",
  "partner": true,
  "url": "http://www.twitch.tv/test_channel",
  "views": 49144894,
  "followers": 215780,
  "_links": {
    "self": "https://api.twitch.tv/kraken/channels/test_channel",
    "follows": "https://api.twitch.tv/kraken/channels/test_channel/follows",
    "commercial": "https://api.twitch.tv/kraken/channels/test_channel/commercial",
    "stream_key": "https://api.twitch.tv/kraken/channels/test_channel/stream_key",
    "chat": "https://api.twitch.tv/kraken/chat/test_channel",
    "features": "https://api.twitch.tv/kraken/channels/test_channel/features",
    "subscriptions": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions",
    "editors": "https://api.twitch.tv/kraken/channels/test_channel/editors",
    "teams": "https://api.twitch.tv/kraken/channels/test_channel/teams",
    "videos": "https://api.twitch.tv/kraken/channels/test_channel/videos"
  },
  "email": "test_channel@twitch.tv",
  "stream_key": "live_5439587_s8df7s9d7g6dsfggsdfg"
}
```

## `POST /channels/:channel/commercial`

Start commercial on channel.

*__Authenticated__*, required scope: `channel_commercial`

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
            <td><code>length</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Length of commercial break in seconds. Default value is 30. Valid values are 30, 60, 90, 120, 150, and 180. You can only trigger a commercial once every 8 minutes.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-d "length=30" -X POST https://api.twitch.tv/kraken/channels/test_channel/commercial
```

### Example Response

`204 No Content` if successful.

### Errors

`422 Unprocessable Entity` if commercial length not allowed, a commercial was ran less than 8 minutes ago, or the channel is not partnered.

## `GET /channels/:channel/teams`

Returns a list of team objects `:channel` belongs to.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/channels/test_channel/teams
```

### Example Response

```json
{
  "_links": {
    "self": "http://api.twitch.tv/kraken/channels/test_channel/teams"
  },
  "teams": [
    {
      "_links": {
        "self": "https://api.twitch.tv/kraken/teams/staff"
      },
      "_id": 10,
      "name": "staff",
      "info": "We save the world..\n\n\n",
      "display_name": "Twitch Staff",
      "created_at": "2011-10-25T23:55:47Z",
      "updated_at": "2013-05-24T00:17:12Z",
      "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-staff-team_logo_image-e26f89ac4f424216-300x300.png",
      "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-staff-banner_image-c81e25b281c06e8f-640x125.png",
      "background": null
    },
    ...
  ]
}
```
