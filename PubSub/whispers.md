# Whisper events over PubSub
Using the Twitch PubSub system (TPS), you can listen to Whisper events by subscribing to the Whisper event topic. When connecting, you'll need to provide authentication via an OAuth token from the channel where you're
listening. For general information about TPS (including rate limits and best practices), check out the [Twitch PubSub System documentation](https://github.com/justintv/Twitch-API/tree/master/PubSub).

## Subscribing to a Whisper topic
You can subscribe to a Whisper topic for a channel by sending a simple JSON message. The topic has a specific format: `whispers.<user_id>`. When
subscribing to the Whisper topic for a channel, you must supply an OAuth token linked to the user_id for the topic using the `chat_login` scope.

In full, you would send a request that looks like the following:

```json
{
  "type": "LISTEN",
  "nonce": "...",
  "data": {
    "topics": ["whispers.XXXXXXXX"],
    "auth_token": "...",
  }
}
```

After your initial request, you'll receive a response message with the error if applicable.
```json
{
  "type": "RESPONSE",
  "nonce": "...",
  "error": "..."
}
```

The `nonce` field will match the request `nonce`. The `error` field will be an empty string if there is no error. If there is an error, it can be one of
ERR_BADMESSAGE, ERR_BADAUTH, ERR_SERVER, ERR_BADTOPIC.

## Receiving a Whispers event message
When a message for your subscription is published, you will receive a message containing the applicable data. The message will look like the following. The data and message fields are JSON strings and will need to be escaped.

```json
{
   "type":"MESSAGE",
   "data":{
      "topic":"whispers.45963323",
      "message":{
         "type":"whisper_received",
         "data":{
            "id":41
         },
         "thread_id":"39141793_45963323",
         "body":"hello",
         "sent_ts":1479160009,
         "from_id":39141793,
         "tags":{
            "login":"xangold",
            "display_name":"Xangold",
            "color":"#8A2BE2",
            "user_type":"staff",
            "turbo":true,
            "emotes":[

            ],
            "badges":[
               {
                  "id":"staff",
                  "version":"1"
               },
               {
                  "id":"turbo",
                  "version":"1"
               }
            ]
         },
         "recipient":{
            "id":45963323,
            "username":"xantest",
            "display_name":"xantest",
            "color":"",
            "user_type":"",
            "turbo":false,
            "badges":[

            ]
         },
         "nonce":"6GVBTfBXNj7d71BULYKjpiKapegDI1"
      },
      "data_object":{
         "id":41,
         "thread_id":"39141793_45963323",
         "body":"hello",
         "sent_ts":1479160009,
         "from_id":39141793,
         "tags":{
            "login":"xangold",
            "display_name":"Xangold",
            "color":"#8A2BE2",
            "user_type":"staff",
            "turbo":true,
            "emotes":[

            ],
            "badges":[
               {
                  "id":"staff",
                  "version":"1"
               },
               {
                  "id":"turbo",
                  "version":"1"
               }
            ]
         },
         "recipient":{
            "id":45963323,
            "username":"xantest",
            "display_name":"xantest",
            "color":"",
            "user_type":"",
            "turbo":false,
            "badges":[

            ]
         },
         "nonce":"6GVBTfBXNj7d71BULYKjpiKapegDI1"
      }
   }
}
```