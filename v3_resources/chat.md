# Chat

Chat is where Twitch users can interact with each other while watching a [stream][streams].

[streams]: /v3_resources/streams.md

| Endpoint | Description |
| ---- | --------------- |
| [GET /chat/:channel](/v3_resources/chat.md#get-chatchannel) | Get links object to other chat endpoints |
| [GET /chat/:channel/badges](/v3_resources/chat.md#get-chatchannelbadges) | Get chat badges for channel |
| [GET /chat/emoticons](/v3_resources/chat.md#get-chatemoticons) | Get list of every emoticon object |
| [GET /chat/emoticon_images](/v3_resources/chat.md#get-chatemoticon_images) | Get list of emoticons |

## `GET /chat/:channel`

Returns a links object to all other chat endpoints.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/chat/kraken_test_user
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/chat/kraken_test_user",
    "emoticons":"https://api.twitch.tv/kraken/chat/kraken_test_user/emoticons",
    "badges": "https://api.twitch.tv/kraken/chat/kraken_test_user/badges"
  }
}
```

## `GET /chat/emoticons`

Returns a list of all emoticon objects for Twitch.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/chat/emoticons
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/chat/emoticons"
  },
  "emoticons": [
    {
      "regex": "\:-?\(",
      "images": [
        {
          "emoticon_set": null,
          "height": 18,
          "width": 24,
          "url": "http://static-cdn.jtvnw.net/jtv_user_pictures/chansub-global-emoticon-d570c4b3b8d8fc4d-24x18.png"
        },
        {
          "emoticon_set": 33,
          "height": 18,
          "width": 21,
          "url": "http://static-cdn.jtvnw.net/jtv_user_pictures/chansub-global-emoticon-c41c5c6c88f481cd-21x18.png"
        }
      ]
    },
    ...
  ]
}
```

## `GET /chat/emoticon_images`

Returns a list of emoticons.

_Note:_ You can query a user's list of usable emoticons with [`GET /users/:user/emotes`](users.md#get-usersuseremotes)

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
            <td><code>emotesets</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Emotes from a comma separated list of emote sets.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json'
-X GET https://api.twitch.tv/kraken/chat/emoticon_images
```

### Example Responses

Without specified emote sets:

```json
{
  "emoticons": [
    {
      "id": 25,
      "code": "Kappa",
      "emoticon_set": null
    },
    {
      "id": 2412,
      "code": "pipeKoppa",
      "emoticon_set": 469
    },
    ...
  ]
}
```

With specified emote sets:

```json
{
  "emoticon_sets": {
    "0": [
      {
        "id": 25,
        "code": "Kappa"
      },
      {
        "id": 1902,
        "code": "Keepo"
      },
      ...
    ],
    "469": [
      {
        "id": 2412,
        "code": "pipeKoppa"
      },
      {
        "id": 33152,
        "code": "pipeKappa"
      },
      ...
    ]
  }
}
```

## `GET /chat/:channel/badges`

Returns a list of chat badges that can be used in the `:channel`'s chat.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/chat/test_user1/badges
```

### Example Response

```json
{
  "global_mod": {
    "alpha": "http://chat-badges.s3.amazonaws.com/globalmod-alpha.png",
    "image": "http://chat-badges.s3.amazonaws.com/globalmod.png",
    "svg": "http://chat-badges.s3.amazonaws.com/globalmod.svg"
  },
  "admin": {
    "alpha": "http://chat-badges.s3.amazonaws.com/admin-alpha.png",
    "image": "http://chat-badges.s3.amazonaws.com/admin.png",
    "svg": "http://chat-badges.s3.amazonaws.com/admin.svg"
  },
  "broadcaster": {
    "alpha": "http://chat-badges.s3.amazonaws.com/broadcaster-alpha.png",
    "image": "http://chat-badges.s3.amazonaws.com/broadcaster.png",
    "svg": "http://chat-badges.s3.amazonaws.com/broadcaster.svg"
  },
  "mod": {
    "alpha": "http://chat-badges.s3.amazonaws.com/mod-alpha.png",
    "image": "http://chat-badges.s3.amazonaws.com/mod.png",
    "svg": "http://chat-badges.s3.amazonaws.com/mod.svg"
  },
  "staff": {
    "alpha": "http://chat-badges.s3.amazonaws.com/staff-alpha.png",
    "image": "http://chat-badges.s3.amazonaws.com/staff.png",
    "svg": "http://chat-badges.s3.amazonaws.com/staff.svg"
  },
  "turbo": {
    "alpha": "http://chat-badges.s3.amazonaws.com/turbo-alpha.png",
    "image": "http://chat-badges.s3.amazonaws.com/turbo.png",
    "svg": "http://chat-badges.s3.amazonaws.com/turbo.svg"
  },
  "subscriber": null,
  "_links": {
    "self": "https://api.twitch.tv/kraken/chat/test_user1/badges"
  }
}
```

## Embedding

[See here for embedding.][embedding]

[embedding]: /embed-chat.md#embedding-twitch-chat

## Connecting to IRC

[See here for connecting to IRC.][IRC]

[IRC]: /IRC.md
