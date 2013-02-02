# Twitch API

## Overview

The Twitch API enables you to develop your own applications using the rich feature set that we provide. Features include retrieving data about what streams are live, changing information about specific channels, and doing an SSO integration with Twitch. The following pages list the resources that the Twitch API provides. If you have any questions or need help in using this API, please visit the [API Developers Group][] or [Github Issues][].

The Twitch API is comprised of two parts: the REST API and a [JavaScript SDK][] that allows for easy integration of the Twitch features into any website. Most users will only need to use the JS SDK, but if you want a deeper integration (for example, for use with Python or PHP scripts), you may access the REST API directly. The [RESTful Integration Guide][] provides additional information for using REST API.

[API Developers Group]: https://groups.google.com/forum/?fromgroups#!forum/twitch-api
[JavaScript SDK]: /../../../twitch-js-sdk
[Github Issues]: /../../issues
[RESTful Integration Guide]: /RESTful-Integration-Guide.md

### Formats

The base URL for all API resources is `https://api.twitch.tv/kraken`.

All data is sent and received as [JSON][]. Blank fields are included as `null` instead of being omitted.

[JSON]: http://www.json.org/

### JSON-P

All API methods support [JSON-P][] by providing a `callback` parameter with the request.

```bash
curl -i https://api.twitch.tv/kraken?callback=foo
```

[JSON-P]: http://json-p.org/

### Self-Describing API

The API is self-describing and can be explored from the base URL:

```bash
curl -i https://api.twitch.tv/kraken
```

Every JSON response includes a `_links` object which allows you to navigate the API without having to hardcode any of our URLs.

```json
{
    "_links": {
        "teams": "https://api.twitch.tv/kraken/teams",
        "channel": "https://api.twitch.tv/kraken/channel",
        "user": "https://api.twitch.tv/kraken/user",
        "ingests": "https://api.twitch.tv/kraken/ingests",
        "streams": "https://api.twitch.tv/kraken/streams",
        "search": "https://api.twitch.tv/kraken/search"
    },
    ...
}
```

### API Versions and MIME Types

We allow clients to use any version of our API. Versioning is per-method so for example you can have v1 of `/channels` and v2 of `/users`. If a version is not specified, the latest version will be used, which is currently **v2**. We *strongly* recommend specifying a version, otherwise version updates might break your application if you've defaulted your requests to use the latest version.

When specifying a version for a request to the Twitch API, set the `Accept` HTTP header to the API version you prefer. This is done by appending a version specifier to our vendor specific MIME type. Responses will have an `x-api-version` header that will indicate which version you received.

Clients may specify the following MIME types:

```bash
application/json
application/vnd.twitchtv+json
application/vnd.twitchtv[.version]+json
```

The returned MIME type from requests is always

```bash
application/json
```

<a name="requests"/>
### Example Requests

For the latest version of the API:

    curl -i -H 'Accept: application/vnd.twitchtv+json' 'https://api.twitch.tv/kraken/channels/hebo?client_id=axjhfp777tflhy0yjb5sftsil' 
    
    HTTP/1.1 200 OK
    ...
    x-api-version: 2
    ...
    Front-End-Https: on
    
    { ...

Specify a specific version (v1):

    curl -i -H 'Accept: application/vnd.twitchtv.v1+json' 'https://api.twitch.tv/kraken/channels/hebo?client_id=axjhfp777tflhy0yjb5sftsil' 
    
    HTTP/1.1 200 OK
    ...
    x-api-version: 1
    ...
    Front-End-Https: on
    
    { ...

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

<a name="oauth"/>
<a name="wiki-auth"/>
## Authentication 

We use an OAuth 2.0, an authentication protocol designed to make accessing user accounts from third party clients easy and secure. Read our [authentication guide][] to see how to connect with Twitch users from your own service.

[authentication guide]: /authentication.md

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
    "user_name": "hebo",
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

### [Users](/resources/users.md)
### [Channels](/resources/channels.md)
### [Videos](/resources/videos.md)
### [Streams](/resources/streams.md)
### [Games](/resources/games.md)
### [Search](/resources/search.md)
### [Teams](/resources/teams.md)
### [Chat](/resources/chat.md)
### [Ingests](/resources/ingests.md)
### [Blocks](/resources/blocks.md)
