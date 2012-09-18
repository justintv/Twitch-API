# Ingests

## Get the a list of Ingest points for Twitch.

These are RTMP Ingest points.

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

