# Root

| Endpoint | Description |
| ---- | --------------- |
| [GET /](/v2_resources/root.md#get-) | Get top level links object and authorization status |

## `GET /`

Basic information about the API and authentication status. If you are authenticated, the response includes the status of your token and links to other related resources.

### Example Request

```bash
curl -i -H 'Authorization: OAuth [access token]' https://api.twitch.tv/kraken
```

### Example Response

```json
{
  "token": {
    "authorization": {
      "scopes": ["user_read", "channel_read", "channel_commercial", "user_read"],
      "created_at": "2012-05-08T21:55:12Z",
      "updated_at": "2012-05-17T21:32:13Z"
    },
    "user_name": "test_user1",
    "valid": true
  },
  "_links": {
    "channel": "https://api.twitch.tv/kraken/channel",
    "users": "https://api.twitch.tv/kraken/users/test_user1",
    "user": "https://api.twitch.tv/kraken/user",
    "channels": "https://api.twitch.tv/kraken/channels/test_user1",
    "chat": "https://api.twitch.tv/kraken/chat/test_user1",
    "streams": "https://api.twitch.tv/kraken/streams",
    "ingests":"https://api.twitch.tv/kraken/ingests"
  }
}
```
