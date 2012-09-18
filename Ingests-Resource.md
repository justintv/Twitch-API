# Ingests

## Get the list of Ingest points for twitch.

These are RTMP Ingest points. By directing an rtmp stream with your stream key as the final part of the URL, you will broadcast your content live on twitch.

`GET /ingests/`

### Response

    {
      "_links": {
        "self": "https://api.twitch.tv/kraken/ingests"
      },
      "ingests": [
        {
          "name": "EU: Amsterdam, NL" ,
          "default": false ,
          "_id": 24 ,
          "url": "rtmp://live-ams.twitch.tv/app",
          "availability":1.0
        }
      ]
    }

