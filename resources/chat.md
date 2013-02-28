# Chat

***

Chat is where Twitch users can interact with each other while watching a [stream][streams].

[streams]: /resources/streams.md

| Endpoint | Description |
| ---- | --------------- |
| [GET /chat/:channel](/resources/chat.md#get-chatchannel) | Get links object to other chat endpoints |
| [GET /chat/emoticons](/resources/chat.md#get-chatemoticons) | Get list of every emoticon object |

## `GET /chat/:channel`

Returns a links object to all other chat endpoints.

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/chat/kraken_test_user
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
curl -i https://api.twitch.tv/kraken/chat/emoticons
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

## `GET /chat/:channel/emoticons` \** __DEPRECATED__ \**

Returns a list of emoticon objects that can be used in the `:channel`'s chat.

[DEPRECATED] - Emoticon sets are no longer tied to specific channels, so information returned from this endpoint is somewhat useless.

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/chat/test_user1/emoticons
```

### Example Response

```json
{
  "emoticons": [
    {
      "regex": "MeoW",
      "url": "http://static-cdn.jtvnw.net/jtv_user_pictures/chansub-test_user1-emoticon-30bc1522fa392415-28x32.png",
      "height": 32,
      "width": 28,
      "subscriber_only": true
    },
    {
      "regex": "\\&lt\\;3",
      "url": "http://static-cdn.jtvnw.net/jtv_user_pictures/chansub-global-emoticon-67cde8d0b7916e57-24x18.png",
      "height":18,
      "width":24,
      "subscriber_only": false
    }
    ...
  ],

  "_links": {
   "self": "https://api.twitch.tv/kraken/chat/test_user1/emoticons"
  }
}
```

## Embedding

[See here for embedding.][embedding]

[embedding]: /embedding.md#embedding-streams-vods-and-chat

## Connecting to IRC

[See here for connecting to IRC.][IRC]

[IRC]: /IRC.md
