# TwitchTV API 2.0

## Overview

This is a comprehensive description of the resources that make up the TwitchTV API. For support or issue help, visit the [API Developers Group][] or [Github Issues][]

The TwitchTV API is comprised of two parts: the REST API itself and the [JavaScript SDK][] that allows for easy integration into any website. Most users will only need to use the JS SDK, but if you want a deeper integration you may access the REST API directly.


[API Developers Group]: https://groups.google.com/forum/?fromgroups#!forum/justintv-api-developers
[JavaScript SDK]: /justintv/twitch-js-sdk
[Github Issues]: /justintv/twitch-js-sdk/issues

### Formats

The base URL for all API resources is `https://api.twitch.tv/kraken`.

All data is sent and received as JSON.

Blank fields are included as `null` instead of being omitted.

### JSON-P

All API methods support JSON-P by providing a `callback` parameter with the request.

    curl https://api.twitch.tv/kraken?callback=foo
    
### Errors

All error responses are in the following format, delivered with the corresponding status code:

    {
        "message":"Invalid Token",
        "status":401,
        "error":"Unauthorized"
    }

When using JSON-P, the status code will always be `200` to allow browsers to parse it. Check the body of the response for the actual error data.
### MIME Types

The returned MIME type from requests follows the format:

    application/vnd.twitchtv[.version].param[+json]

Clients may specify the following MIME types:

    application/json
    application/vnd.twitchtv+json
    application/vnd.twitchtv[.version]+json

This allows clients to get either the latest version of the API or a specific version.

## OAuth 2

[OAuth 2][] is an authentication protocol designed to make accessing user accounts easy and secure. 

Before you can handle user authorization in your app, register a [client application][]. The specified `redirect_uri` will receive the result of all client authorizations in JSON: either an access token or a failure message. 

Next, direct users on your application to the [authorization endpoint][], where they will log in or register on TwitchTV and approve access for your application. You can include the following URL parameters:

- `response_type` (required): `token`.
- `client_id` (required): The Client ID of your app that you recieved upon creation.
- `redirect_uri` (required): The URL that clients will be forwarded to upon approval.
- `scope` (required): A **space separated** list of [scopes](#wiki-scope) your app is requesting approval for to be displayed to the user.
- `state` (recommended): A string that maintains state between the request and callback to `redirect_uri`. This can be useful for allowing your application to associate an authorization with a specific user request. 

An example authorization request:

    https://api.twitch.tv/kraken/oauth2/authorize?redirect_uri=http://example.com&client_id=i29g16w8403x4s196d47tavi&response_type=token&scope=user_read+channel_read&state=user_dayjay

Once your application is authorized, the user will be forwarded to the specified `request_uri` with a URL fragment containing `access_token` and `scope` parameters. URL fragments can be accessed from JavaScript with `document.location.hash`.

    http://example.com/#access_token=bb09tmrqbxbgvlny25pbm5kfs&scope=user_read+channel_read

That's it! Your application can now make requests on behalf of the user by including your access token as specified in [Authentication](#auth).

[OAuth 2]: http://hueniverse.com/2010/05/introducing-oauth-2-0
[client application]: https://api.twitch.tv/kraken/oauth2/clients/new
[authorization endpoint]: https://api.twitch.tv/kraken/oauth2/authorize


### Scopes <a name="scope"></a>

When requesting authorization from users, the scope parameter allows you to specify which permissions your app requires. Without specifying scopes, your app only has access to basic information about the authenticated user. You may specify any or all of the following scopes:

- `user_read`: Read access to non-public user information, such as email address.
- `channel_read`: Read access to non-public channel information, including email address and stream key.
- **(Not Implemented)** `channel_editor`: Write access to channel metadata (title, game, status, other metadata). Cut VODs.
- `channel_commercial`: Access to trigger commercials on channel.


Scopes are specified as a *space separated* list in the url parameter `scope` when requesting authorization:

    &scope=user_read+channel_read

Your app should ask for the minimum permissions that allow you to perform needed actions. 

### Authentication <a name="wiki-auth"></a>

We do not allow username/password authentication. All clients must use OAuth 2.

Send token as header:

    curl -H "Authorization: token OAUTH-TOKEN" https://api.twitch.tv/kraken

Send token as URL parameter:

    curl https://api.twitch.tv/kraken?oauth_token=OAUTH-TOKEN

## Resources

### Root

`/`

Basic information about the API and authentication status. If you are authenticated, the response includes the status of your token and links to other related resources.

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
        "chat": "https://api.twitch.tv/kraken/chat/hebo"
      }
    }

### (**v2**) Following

`PUT /follows/:user` 

(**v2**, *Authenticated, Scope:user*) Follow the specified user.
 
`DELETE /follows/:user`

(**v2**, *Authenticated, Scope:user*) Unfollow the specified user.

### [Users](Users-Resource)

### Channels

`GET /channel`

(*Authenticated, Scope:channel*) Get the channel associated with the authenticated user. Includes the channel stream key.

    {
      "game": "Diablo II: Lord of Destruction",
      "name": "Hebo",
      "stream_key": "live_21229404_abcdefg",
      "created_at": "2011-03-19T15:42:22Z",
      "title": "Cev",
      "updated_at": "2012-03-14T03:30:41Z",
      "teams": [{
        "name": "staff",
        "created_at": "2011-10-25T23:55:47Z",
        "updated_at": "2011-11-14T19:48:21Z",
        "background": null,
        "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-staff-banner_image-1e028d6b6aec8e6a-640x125.jpeg",
        "logo": null,
        "_links": {
          "self": "https://api.twitch.tv/kraken/teams/staff"
        },
        "_id": 10,
        "info": "We save the world..",
        "display_name": "TwitchTV Staff"
      }],
      "_links": {
        "self": "https:/api.twitch.tv/kraken/channels/hebo",
        "chat":"https:/api.twitch.tv/kraken/chat/hebo",
        "commercial":"https:/api.twitch.tv/kraken/channels/hebo/commercial"
      },
      "id": 21229404,
      "mature": false,
      "login": "hebo",
      "email": "james@justin.tv"
    }

`GET /channels/:channel/`

Get the specified channel.

    {
      "game": "World of Warcraft: Mists of Pandaria",
      "_id": 20694610,
      "created_at": "2011-02-24T01:38:43Z",
      "mature": true,
      "updated_at": "2012-04-02T17:46:23Z",
      "title": "Towelliee HD Gaming",
      "teams": [{
        "_id": 134,
        "created_at": "2011-12-23T06:30:14Z",
        "updated_at": "2012-01-08T23:48:52Z",
        "info": "Building a career path for YouTubers! See http://tgn.tv\n\n",
        "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-tgn-background_image-6c4e34a8def09253.jpeg",
        "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-tgn-team_logo_image-d2b677d4f1ecc008-300x300.png",
        "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-tgn-banner_image-8607f365e2d69e22-640x125.png",
        "_links": {
          "self": "https://api.twitch.tv/kraken/teams/tgn"
        },
        "display_name": "TGN",
        "name": "tgn"
      }],
      "_links": {
        "self": "https:/api.twitch.tv/kraken/channels/towelliee",
        "chat":"https:/api.twitch.tv/kraken/chat/towelliee",
        "commercial":"https:/api.twitch.tv/kraken/channels/towelliee/commercial"
      },
      "display_name": "Towelliee",
      "name": "towelliee"
    }

`PATCH /channel`

(**v2**)

`POST /channels/:channel/commercial`

Trigger a commercial for the specified channel.

#### Parameters

  -`length` (**Default: 30**): Length of the commercial break in seconds from 30 to 90. You may only trigger a commercial longer than 30 seconds once every 15 minutes.

#### Response

`204 No Content` if successful.

### Teams

`GET /teams/:team/`

Get the specified team.

    {
      "_id": 2,
      "created_at": "2011-10-11T23:59:43Z",
      "info": "Team Info\n",
      "updated_at": "2012-01-15T19:43:40Z",
      "background": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-background_image-089a407eb59fe3b2.png",
      "banner": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-banner_image-8089b058e6ffe4cd-640x125.png",
      "logo": "http://static-cdn.jtvnw.net/jtv_user_pictures/team-eg-team_logo_image-53eaf029dad7d5c9-300x300.png",
      "_links": {
        "self": "https://api.twitch.tv/kraken/teams/eg"
      },
      "display_name": "Evil Geniuses",
      "name": "eg"
    }

### Chat

`GET /chat/:channel`

Get the chat associated with the channel.

    {
      "_links": {
        "self": "https://api.twitch.tv/kraken/chat/kraken_test_user",
        "emoticons":"https://api.twitch.tv/kraken/chat/kraken_test_user/emoticons"
      }
    }

`GET /chat/:channel/emoticons`

Get the emoticons that can be used in a chat.

    {
      "emoticons": [
        {
          "regex": "MeoW",
          "url": "http://static-cdn.jtvnw.net/jtv_user_pictures/chansub-crs_crumbzz-emoticon-30bc1522fa392415-28x32.png",
          "height": 32,
          "width": 28,
          "subscriber_only": true
        },
        {
          "regex": "\\&lt\\;3",
          "url": "http://static-cdn.jtvnw.net/jtv_user_pictures/chansub-global-emoticon-67cde8d0b7916e57-24x18.png",
          "height":18,
          "width":24,
          "subscriber_only": false
        }
        ...
      ],

      "_links": {
       "self": "https://api.twitch.tv/kraken/chat/kraken_test_user/emoticons"
      }
    }