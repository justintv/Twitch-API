# Bits events over PubSub
Using the Twitch PubSub system (TPS), you can listen to Bits events occurring in a channel by subscribing to the Bits event topic. When connecting, you'll need to provide authentication via an OAuth token from the channel where you're 
listening. For general information about TPS (including rate limits and best practices), check out the [Twitch PubSub System documentation](https://github.com/justintv/Twitch-API/tree/master/PubSub).

## Subscribing to a Bits topic
You can subscribe to a Bits topic for a channel by sending a simple JSON message. The topic has a specific format: `channel-bitsevents.<channel_id>`. When 
subscribing to the Bits topic for a channel, you must supply an OAuth token linked to the channel_id for the topic. Any scope will suffice for subscribing. 

In full, you would send a request that looks like the following:

```json
{
  "type": "LISTEN",
  "nonce": "...",
  "data": {
    "topics": ["channel-bitsevents.XXXXXXXX"],
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

## Receiving a Bits event message
When a message for your subscription is published, you will receive a message containing the applicable data. The message will look like the following:

```json
{
    "type": "MESSAGE",
    "data": {
        "topic": "channel-bitsevents.XXXXXXXX",
        "message": {
            "user_name": "dallasnchains",
            "channel_name": "twitch",
            "user_id": "...",
            "channel_id": "...",
            "time": "2015-12-19T16:39:57-08:00",
            "chat_message": "Omg that baneling bust was Kreygasm cheer10 cheer10 cheer100",
            "bits_used": 120,
            "total_bits_used": 620,
            "context": "cheer"
            }
    }
}
```

##### Response Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th width="50px">Type</th>
            <th width="100%">Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>username</code></td>
            <td>string</td>
            <td>Login name of the person who used Bits.</td>
        </tr>
        <tr>
            <td><code>channel_name</code></td>
            <td>string</td>
            <td>Channel name of where Bits were used.</td>
        </tr>
        <tr>
            <td><code>user_id</code></td>
            <td>string</td>
            <td>ID of the user who used Bits.</td>
        </tr>
        <tr>
            <td><code>channel_id</code></td>
            <td>string</td>
            <td>ID of the channel where Bits were used.</td>
        </tr>
        <tr>
            <td><code>time</code></td>
            <td>string</td>
            <td>Time of the event in RFC 3339 format.</td>
        </tr>
        <tr>
            <td><code>chat_message</code></td>
            <td>string</td>
            <td>Chat message sent with the Bits used.</td>
        </tr>
        <tr>
            <td><code>bits_used</code></td>
            <td>int</td>
            <td>Number of Bits used.</td>
        </tr>
        <tr>
            <td><code>total_bits_used</code></td>
            <td>int</td>
            <td>All-time total number of Bits used on this channel by the user.</td>
        </tr>
        <tr>
            <td><code>context</code></td>
            <td>string</td>
            <td>Event type associated with this Bits usage (e.g. cheer).</td>
        </tr>
    </tbody>
</table>