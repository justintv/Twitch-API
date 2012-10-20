# Twitch API

## Overview

The Twitch API allows websites to develop your own applications based on the rich feature set that we provide. This includes getting information about what streams are live, changing information about specific channels, or doing a SSO integration with Twitch itself. This documents lists the resources that the Twitch API provides. If you have any questions or need any help in using this API, please visit the [API Developers Group][] or [Github Issues][]

The Twitch API is comprised of two parts: the REST API itself and the [JavaScript SDK][] that allows for easy integration into any website. Most users will only need to use the JS SDK, but if you want a deeper integration (for example, for use with Python or PHP scripts) you may access the REST API directly. The [RESTful Integration Guide][] should help you if that describes your needs.


[API Developers Group]: https://groups.google.com/forum/?fromgroups#!forum/twitch-api
[JavaScript SDK]: /justintv/twitch-js-sdk
[Github Issues]: /justintv/Twitch-API/issues
[RESTful Integration Guide]: /justintv/Twitch-API/blob/master/RESTful-Integration-Guide.md

### Formats

The base URL for all API resources is `https://api.twitch.tv/kraken`.

All data is sent and received as [JSON][].

Blank fields are included as `null` instead of being omitted.

[JSON]: http://www.json.org/

### JSON-P

All API methods support [JSON-P][] by providing a `callback` parameter with the request.

```bash
curl https://api.twitch.tv/kraken?callback=foo
```

[JSON-P]: http://json-p.org/
### Errors

All error responses are in the following format, delivered with the corresponding status code:

```json
{
    "message":"Invalid Token",
    "status":401,
    "error":"Unauthorized"
}
```

When using JSON-P, the status code will always be `200` to allow browsers to parse it. Check the body of the response for the actual error data.

### MIME Types and API Versions

The returned MIME type from requests follows the format:

```bash
application/vnd.twitchtv[.version][+json]
```

Clients may specify the following MIME types:

```bash
application/json
application/vnd.twitchtv+json
application/vnd.twitchtv[.version]+json
```

This allows clients to get either the latest version of the API or a specific version. The current version of the API is `application/vnd.twitchtv.v1+json`

<a name="requests"/>
### Making Requests

When performing requests to the Twitch API, set the `Accept` HTTP header to the API version you prefer.

#### Example

For the latest version of the API:

    curl -i -H 'Accept: application/vnd.twitchtv+json' 'https://api.twitch.tv/kraken/channels/hebo?client_id=axjhfp777tflhy0yjb5sftsil' 

Specify a specific version (v1):

    curl -i -H 'Accept: application/vnd.twitchtv.v1+json' 'https://api.twitch.tv/kraken/channels/hebo?client_id=axjhfp777tflhy0yjb5sftsil' 

<a name="oauth"/>
<a name="wiki-auth"/>
## Authentication 

We use an OAuth 2.0, an authentication protocol designed to make accessing user accounts from third party clients easy and secure. Read the [authentication guide][] to see how to connect with Twitch users.

[authentication guide]: /justintv/Twitch-API/blob/master/authentication.md

## Resources

### Root

`/`

Basic information about the API and authentication status. If you are authenticated, the response includes the status of your token and links to other related resources.

#### Response

```json
{
  "token": {
    "authorization": {
      "scopes": ["user_read", "channel_read", "channel_commercial", "user_read"],
      "created_at": "2012-05-08T21:55:12Z",
      "updated_at": "2012-05-17T21:32:13Z"
    },
    "valid": true
  },
  "_links": {
    "channel": "https://api.twitch.tv/kraken/channel",
    "users": "https://api.twitch.tv/kraken/users/hebo",
    "user": "https://api.twitch.tv/kraken/user",
    "channels": "https://api.twitch.tv/kraken/channels/hebo",
    "chat": "https://api.twitch.tv/kraken/chat/hebo",
    "streams": "https://api.twitch.tv/kraken/streams",
    "ingests":"https://api.twitch.tv/kraken/ingests"
  }
}
```

### [Users](/justintv/Twitch-API/blob/master/resources/users.md)
### [Channels](/justintv/Twitch-API/blob/master/resources/channels.md)
### [Videos](/justintv/Twitch-API/blob/master/resources/videos.md)
### [Streams](/justintv/Twitch-API/blob/master/resources/streams.md)
### [Games](/justintv/Twitch-API/blob/master/resources/games.md)
### [Search](/justintv/Twitch-API/blob/master/resources/search.md)
### [Teams](/justintv/Twitch-API/blob/master/resources/teams.md)
### [Chat](/justintv/Twitch-API/blob/master/resources/chat.md)
### [Ingests](/justintv/Twitch-API/blob/master/resources/ingests.md)
### [Blocks](/justintv/Twitch-API/blob/master/resources/blocks.md)