# Chat

***

Chat is where Twitch users can interact with each other while watching a [stream][streams].

[streams]: /v3_resources/streams.md

| Endpoint | Description |
| ---- | --------------- |
| [GET /chat/:channel](/v3_resources/chat.md#get-chatchannel) | Get links object to other chat endpoints |
| [GET /chat/emoticons](/v3_resources/chat.md#get-chatemoticons) | Get list of every emoticon object |

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
  }
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

## Embedding

[See here for embedding.][embedding]

[embedding]: /embedding.md#embedding-streams-vods-and-chat

## Connecting to IRC

[See here for connecting to IRC.][IRC]

[IRC]: /IRC.md
