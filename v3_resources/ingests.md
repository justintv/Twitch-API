# Ingests

***

These are RTMP ingest points. By directing an RTMP stream with your `stream_key` injected into the `url_template`, you will broadcast your content live on Twitch.

| Endpoint | Description |
| ---- | --------------- |
| [GET /ingests/](/v3_resources/ingests.md#get-ingests) | Get list of ingests |

## `GET /ingests/`

Returns a list of ingest objects.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' \
-X GET https://api.twitch.tv/kraken/ingests
```

### Example Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/ingests"
  },
  "ingests": [
    {
      "name": "EU: Amsterdam, NL",
      "default": false,
      "_id": 24,
      "url_template": "rtmp://live-ams.twitch.tv/app/{stream_key}",
      "availability": 1.0
    },
    ...
  ]
}
```

### Errors
`503 Service Unavailable` if error retrieving ingest status.
