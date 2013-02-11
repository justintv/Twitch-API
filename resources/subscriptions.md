# Subscriptions

## Get a list of subscribers to specified channel

`GET /channels/:channel/subscriptions`

_Authenticated_, required scope: `channel_subscriptions`

### Parameters

- `limit` (optional): The maximum number of streams to return, up to 100.
- `offset` (optional): The offset to begin listing streams, defaults to 0.

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/channels/hebo/subscriptions
```

### Response

```json
{
  "_total": 3,
  "_links": {
    "next": "https://api.twitch.tv/kraken/channels/hebo/subscriptions?limit=25&offset=25",
    "self": "https://api.twitch.tv/kraken/channels/hebo/subscriptions?limit=25&offset=0"
  }
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
        "self": "https://api.twitch.tv/kraken/channels/hebo/subscriptions/testuser"
      }
    },
    ...
  ]
}
```

## Check if specified channel has user as subscriber

`GET /channels/:channel/subscriptions/:user`

Returns a subscription which includes the user if that user is subscribed. Requires authentication for `:channel`.

_Authenticated_, required scope: `channel_check_subscription`

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/channels/hebo/subscriptions/testuser
```

### Response

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
    "self": "https://api.twitch.tv/kraken/channels/hebo/subscriptions/testuser"
  }
}
```

If user is not subscribed:

```json
{
  "message":"testuser has no subscriptions to hebo",
  "status":404,
  "error":"Not Found"
}
```
