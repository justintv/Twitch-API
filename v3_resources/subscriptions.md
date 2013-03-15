# Subscriptions

***

[Users][users] can subscribe to [channels][channels].

| Endpoint | Description |
| ---- | --------------- |
| [GET /channels/:channel/subscriptions](/v3_resources/subscriptions.md#get-channelschannelsubscriptions) | Get list of users subscribed to channel |
| [GET /channels/:channel/subscriptions/:user](/v3_resources/subscriptions.md#get-channelschannelsubscriptionsuser) | Check if channel has user subscribed |

[users]: /v3_resources/users.md
[channels]: /v3_resources/channels.md

## `GET /channels/:channel/subscriptions`

Returns a list of subscription objects sorted by subscription relationship creation date which contain users subscribed to `:channel`.

*__Authenticated__*, required scope: `channel_subscriptions`

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
            <td><code>direction</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Creation date sorting direction. Default is <code>asc</code>. Valid values are <code>asc</code> and <code>desc</code>.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/channels/test_channel/subscriptions
```

### Example Response

```json
{
  "_total": 3,
  "_links": {
    "next": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions?limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions?limit=25&offset=0"
  },
  "subscriptions": [
    {
      "_id": "88d4621871b7274c34d5c3eb5dad6780c8533318",
      "user": {
        "_id": 38248673,
        "logo": null,
        "staff": false,
        "created_at": "2012-12-06T00:32:36Z",
        "name": "testuser",
        "updated_at": "2013-02-06T21:27:46Z",
        "display_name": "testuser",
        "_links": {
          "self": "https://api.twitch.tv/kraken/users/testuser"
        }
      },
      "created_at": "2013-02-06T21:33:33Z",
      "_links": {
        "self": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions/testuser"
      }
    },
    ...
  ]
}
```

## `GET /channels/:channel/subscriptions/:user`

Returns a subscription object which includes the user if that user is subscribed. Requires authentication for `:channel`.

*__Authenticated__*, required scope: `channel_check_subscription`

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/channels/test_channel/subscriptions/testuser
```

### Example Response

If user is subscribed:

```json
{
  "_id": "88d4621871b7274c34d5c3eb5dad6780c8533318",
  "user": {
    "_id": 38248673,
    "logo": null,
    "staff": false,
    "created_at": "2012-12-06T00:32:36Z",
    "name": "testuser",
    "updated_at": "2013-02-06T21:27:46Z",
    "display_name": "testuser",
    "_links": {
      "self": "https://api.twitch.tv/kraken/users/testuser"
    }
  },
  "created_at": "2013-02-06T21:33:33Z",
  "_links": {
    "self": "https://api.twitch.tv/kraken/channels/test_channel/subscriptions/testuser"
  }
}
```

`404 Not Found` if user is not subscribed.
