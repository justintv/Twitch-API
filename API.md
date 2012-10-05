# Twitch API 2.0

## Overview

The Twitch API allows websites to develop your own applications based on the rich feature set that we provide. This includes getting information about what streams are live, changing information about specific channels, or doing a SSO integration with Twitch itself. This documents lists the resources that the Twitch API provides. If you have any questions or need any help in using this API, please visit the [API Developers Group][] or [Github Issues][]

The Twitch API is comprised of two parts: the REST API itself and the [JavaScript SDK][] that allows for easy integration into any website. Most users will only need to use the JS SDK, but if you want a deeper integration (for example, for use with Python or PHP scripts) you may access the REST API directly. The [RESTful Integration Guide](Restful-Integration-Guide) should help you if that describes your needs.


[API Developers Group]: https://groups.google.com/forum/?fromgroups#!forum/twitch-api
[JavaScript SDK]: /justintv/twitch-js-sdk
[Github Issues]: /justintv/Twitch-API/issues

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

### Making Requests <a id="request-requirements"/>

When performing requests to the Twitch API, include your [`client_id`](#oauth) as a URL parameter.

Also, set the `Accept` HTTP header to the API version you prefer.

#### Example

For the latest version of the API:

    curl -i -H 'Accept: application/vnd.twitchtv+json' 'https://api.twitch.tv/kraken/channels/hebo?client_id=axjhfp777tflhy0yjb5sftsil' 

Specify a specific version (`v1`):

    curl -i -H 'Accept: application/vnd.twitchtv.v1+json' 'https://api.twitch.tv/kraken/channels/hebo?client_id=axjhfp777tflhy0yjb5sftsil' 

## Rate Limits <a id="rate-limits"/>

Requests to the Twitch API may be subject to multiple rate limits. At present, there are two types of rate limits:

  - **anonymous** (requests without a `client_id`)
  - **identified** (requests with a `client_id`).

Should your request exceed these limits, the response will have a status code of `429 Too Many Requests`. The `Retry-After` header will contain the number of seconds until the rate limit for this request type will be reset--delay further calls from your app until then.

<table>
    <thead>
        <tr>
            <th>Type</th>
            <th>Limit</th>
            <th>Period</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Anonymous</td>
            <td>6</td>
            <td>1 minute (60 seconds)</td>
            <td>Requests without a `client_id` (per IP Address)</td>
        </tr>
        <tr>
            <td>Identified</td>
            <td>300</td>
            <td>1 minute (60 seconds)</td>
            <td>Requests with a `client_id` (per client_id)</td>
        </tr>
    </tbody>
</table>

## OAuth 2 <a id="oauth"/>

[OAuth 2][] is an authentication protocol designed to make accessing user accounts from third party clients easy and secure. An `access_token` given to your application allows you to perform actions on behalf of an authenticated Twitch user.

There are two ways to get access tokens, a browser-based flow for use on most applications, and a [password credentials flow](Password-Credentials-Grant), which works best on embedded applications which aren't able to integrate a browser (hardware streaming products, game consoles). The rest of this section covers the browser-based flow.

Before you can handle user authorization in your app, register a [client application][]. The specified `redirect_uri` will receive the result of all client authorizations in JSON: either an access token or a failure message. 

Next, direct users on your application to the [authorization endpoint][], where they will log in or register on Twitch and approve access for your application. You can include the following URL parameters:

- `response_type` (required): `token`.
- `client_id` (required): The Client ID of your app that you recieved upon creation.
- `redirect_uri` (required): The URL that clients will be forwarded to upon approval.
- `scope` (required): A **space separated** list of [scopes](#wiki-scope) your app is requesting approval for to be displayed to the user.
- `state` (recommended): A string that maintains state between the request and callback to `redirect_uri`. This can be useful for allowing your application to associate an authorization with a specific user request. 

An example authorization request:

```bash
https://api.twitch.tv/kraken/oauth2/authorize?redirect_uri=http://example.com&client_id=i29g16w8403x4s196d47tavi&response_type=token&scope=user_read+channel_read&state=user_dayjay
```

Once your application is authorized, the user will be forwarded to the specified `request_uri` with a URL fragment containing `access_token` and `scope` parameters. URL fragments can be accessed from JavaScript with `document.location.hash`.

```bash
http://example.com/#access_token=bb09tmrqbxbgvlny25pbm5kfs&scope=user_read+channel_read
```

That's it! Your application can now make requests on behalf of the user by including your access token as specified in [Authentication](#auth).

[OAuth 2]: http://hueniverse.com/2010/05/introducing-oauth-2-0
[client application]: http://www.twitch.tv/settings?section=applications
[authorization endpoint]: https://api.twitch.tv/kraken/oauth2/authorize

### Scopes <a name="scope"></a>

When requesting authorization from users, the scope parameter allows you to specify which permissions your app requires. Without specifying scopes, your app only has access to basic information about the authenticated user. You may specify any or all of the following scopes:

- `user_read`: Read access to non-public user information, such as email address.
- `user_blocks_edit`: Ability to ignore or unignore on behalf of a user.
- `user_blocks_read`: Read access to a user's list of ignored users.
- `user_followed`: Access to followed streams.
- `channel_read`: Read access to non-public channel information, including email address and stream key.
- `channel_editor`: Write access to channel metadata (game, status, other metadata).
- `channel_commercial`: Access to trigger commercials on channel.
- `channel_stream`: Ability to reset a channel's stream key.


Scopes are specified as a *space separated* list in the url parameter `scope` when requesting authorization:

```bash
&scope=user_read+channel_read
```

Your app should ask for the minimum permissions that allow you to perform needed actions. 

### Authentication <a name="wiki-auth"></a>

We do not allow username/password authentication. All clients must use OAuth 2.

Send token as header:

```bash
curl -H "Authorization: OAuth OAUTH-TOKEN" https://api.twitch.tv/kraken
```

Send token as URL parameter:

```bash
curl https://api.twitch.tv/kraken?oauth_token=OAUTH-TOKEN
```

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

### [Users](Users-Resource)
### [Channels](Channels-Resource)
### [Videos](Videos-Resource)
### [Streams](Streams-Resource)
### [Games](Games-Resource)
### [Search](Search-Resource)
### [Teams](Teams-Resource)
### [Chat](Chat-Resource)
### [Ingests](Ingests-Resource)
### [Blocks](Blocks-Resource)