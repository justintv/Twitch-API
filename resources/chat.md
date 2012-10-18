# Chat

## Get the specified channel's chat

`GET /chat/:channel`

### Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/chat/kraken_test_user",
    "emoticons":"https://api.twitch.tv/kraken/chat/kraken_test_user/emoticons"
  }
}
```

## Get a chat's emoticons

`GET /chat/:channel/emoticons`

Get the emoticons that can be used in a chat.

### Response

```json
{
  "emoticons": [
    {
      "regex": "MeoW",
      "url": "http://static-cdn.jtvnw.net/jtv_user_pictures/chansub-crs_crumbzz-emoticon-30bc1522fa392415-28x32.png",
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
   "self": "https://api.twitch.tv/kraken/chat/kraken_test_user/emoticons"
  }
}
```
