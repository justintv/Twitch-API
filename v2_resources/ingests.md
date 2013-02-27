# Ingests

These are RTMP Ingest points. By directing an RTMP stream with your `stream_key` injected into the `url_template`, you will broadcast your content live on Twitch.

## Get the list of Ingest points for Twitch.

`GET /ingests/`

Returns an array of ingests and their status.

### Example Request

```bash
curl -i https://api.twitch.tv/kraken/ingests
```

### Response

```json
{
  "_links": {
    "self": "https://api.twitch.tv/kraken/ingests"
  },
  "ingests": [
    {
      "name": "EU: Amsterdam, NL" ,
      "default": false ,
      "_id": 24 ,
      "url_template": "rtmp://live-ams.twitch.tv/app/{stream_key}",
      "availability":1.0
    },
    ...
  ]
}
```
