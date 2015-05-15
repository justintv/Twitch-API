# Authentication

This page will explain how to allow users from your service or application to access, update, and generally interact with their Twitch account.

We provide three ways for obtaining access to a Twitch account on behalf of the user. We use the [OAuth 2.0 protocol] for authentication, but only certain parts which we outline below.

When working with the Twitch API, you must follow some simple rules to protect user data. This page should help you understand how Twitch authenticates applications and users, and how to perform actions using our API on behalf of Twitch users.

[OAuth 2.0 protocol]:http://hueniverse.com/2010/05/introducing-oauth-2-0

### Developer Setup

To make an application that uses the Twitch API, you will first need to "Register your application" from the [connections tab][] of your Twitch settings page. When creating this app, you'll need to enter in your __redirect URI__, which is where users are redirected after having authorized your application.

Once you create a Developer Application, you are assigned a __client id__. Some authentication flows also require a __client secret__. You can generate one on the same page as the client ID. Client IDs are public and can be shared (e.g. embedded in the source of a web page), but client secrets are equivalent to a password for your application and must be kept _confidential_.

> Your client secret is like a password and we can't show it to you once you leave the page, so make sure to record it somewhere safe. Additionally, generating a new client secret will immediately invalidate the current one, which might make your API requests fail until your app is updated.

When authenticating on behalf of a user, you'll be granted an __access token__ that uniquely identifies to us your client and the user. There are a few ways to obtain access tokens, which are described below. An access token has an associated list of [scopes](#scope) that determine what permissions you are allowed on behalf of the authorized Twitch user.

[Connections tab]: http://www.twitch.tv/settings/connections


### Getting access tokens

There are two ways to get an access token:

  1. If you're making a web app that uses a server, you will probably want to use the [Authorization Code Flow](#auth-code).
  2. If you are making an app that doesn't use a server, such as a client-side JavaScript app or a mobile app, you'll use the [Implicit Grant Flow](#implicit-grant).

<a name="auth-code"></a>
#### Authorization Code Flow

Remember, you must keep your client secret _confidential_. Make sure to never expose it to users, even in an obscured form.

  1. Send the user you'd like to authenticate to this URL:
  
        https://api.twitch.tv/kraken/oauth2/authorize
            ?response_type=code
            &client_id=[your client ID]
            &redirect_uri=[your registered redirect URI]
            &scope=[space separated list of scopes]
            &state=[your provided unique token]

      > We support the `state` OAuth2 parameter, which is strongly recommended
      > for avoid cross-site scripting attacks. If included, it is appended to
      > the list of query parameters when redirecting the user to the
      > `redirect_uri`.
      
      This page will ask the user to sign up or log in with their Twitch account and allow them to choose whether to authorize your application or not.
      
  2. If the user authorizes your application, they will be redirected to the following URL:
  
        https://[your registered redirect URI]/?code=[CODE]
        
  3. On your server, you can now make the following request to obtain an access token:
  
     `POST https://api.twitch.tv/kraken/oauth2/token`
     
     POST Body (URL-encoded)
     
        client_id=[your client ID]
        &client_secret=[your client secret]
        &grant_type=authorization_code
        &redirect_uri=[your registered redirect URI]
        &code=[code received from redirect URI]
        &state=[your provided unique token]
     
  4. We'll respond with a JSON-encoded access token:
   
        {
          "access_token": "[user access token]",
          "scope":[array of requested scopes]
        }
  
  You can then use this access token to perform actions on behalf of an authenticated Twitch user as described in [Authenticated Requests](#authenticated-requests).
  
<a name="implicit-grant"></a>
#### Implicit Grant Flow

The Implicit Grant Flow doesn't require a server that must make requests to the API, so you can use this flow with JavaScript-only applications. If you're integrating Twitch into your website, you'll probably want to use the [Twitch JS SDK](https://github.com/justintv/twitch-js-sdk), which uses this flow and simplifies the integration.


  1. Send the user you'd like to authenticate to this URL:
  
        https://api.twitch.tv/kraken/oauth2/authorize
            ?response_type=token
            &client_id=[your client ID]
            &redirect_uri=[your registered redirect URI]
            &scope=[space separated list of scopes]

      This page will ask the user to sign up or log in with their Twitch account, and allow them to choose whether to authorize your application.
      
  2. If the user authorizes your application, they will be redirected to the following URL:
  
        https://[your registered redirect URI]/#access_token=[an access token]&scope=[authorized scopes]
        
      > Note that the access token is in the URL fragment, not the
      > query string, so it won't show up in HTTP requests to your server.
      > URL fragments can be accessed from JavaScript with
      > `document.location.hash`.

That's it! Your application can now make requests on behalf of the user by including your access token as specified in [Authenticated Requests](#authenticated-requests).

<a name="scope"></a>

### Scopes

When requesting authorization from users, the scope parameter allows you to specify which permissions your app requires. These scopes are ties to the access token you receive upon a successful authorization. Without specifying scopes, your app only has access to basic information about the authenticated user. You may specify any or all of the following scopes:

- `user_read`: Read access to non-public user information, such as email address.
- `user_blocks_edit`: Ability to ignore or unignore on behalf of a user.
- `user_blocks_read`: Read access to a user's list of ignored users.
- `user_follows_edit`: Access to manage a user's followed channels.
- `channel_read`: Read access to non-public channel information, including email address and stream key.
- `channel_editor`: Write access to channel metadata (game, status, etc).
- `channel_commercial`: Access to trigger commercials on channel.
- `channel_stream`: Ability to reset a channel's stream key.
- `channel_subscriptions`: Read access to all subscribers to your channel.
- `user_subscriptions`: Read access to subscriptions of a user.
- `channel_check_subscription`: Read access to check if a user is subscribed to your channel.
- `chat_login`: Ability to log into chat and send messages.

Scopes are specified as a *space separated* list in the url parameter `scope` when requesting authorization:

```bash
&scope=user_read+channel_read
```

You should only ask for permissions that you need, as users can view each requested permission when authorizing your app.

<a name="authenticated-requests"></a>
### Authenticated API Requests

When an API request requires authentication, you can send the access token you obtained above in any of the following ways:
 
  * Send token as header:

	    curl -H "Authorization: OAuth [access token]" https://api.twitch.tv/kraken/

  * Send token as URL parameter:

	    curl https://api.twitch.tv/kraken?oauth_token=[access token]

  * Send token in the HTTP body (cannot be used with `GET` and `DELETE` methods)
  
        curl -d 'oauth_token=[access token]' https://api.twitch.tv/kraken/channels/cevtest15/commercial
