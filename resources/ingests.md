# Ingests

## Get the list of Ingest points for twitch.

These are RTMP Ingest points. By directing an rtmp stream with your stream_key injected into the url_template, you will broadcast your content live on twitch.

`GET /ingests/`

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
    }
  ]
}
```
