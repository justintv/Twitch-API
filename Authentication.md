# Authentication

When working with the Twitch API, you must follow some simple rules to protect user data. This page should help you understand how Twitch authenticates applications and users, and how to perform actions on behalf of Twitch users.

We use the [OAuth 2.0 protocol] for authentication, but only certain parts. This page will explain the parts that we use and how they interact with the API.

[OAuth 2.0 protocol]:http://hueniverse.com/2010/05/introducing-oauth-2-0

### Developer Setup

To make an application that uses the Twitch API, you will first need to create a "Developer Application" from the [applications tab][] of your Twitch settings page. When creating the app, you'll need to enter in your __redirect uri__, which is where users get redirected after they have authorized your application.

After you have an application, you are assigned a __client id__. Some authentication flows require a __client secret__ as well, so you can generate one on the same page. Client ids are public and can be shared (e.g. embedded in the source of a web page), but client secrets are equivalent to a password for your application and _must_ be kept confidential.

> Since your client secret is like a password, we can't show it to you once you leave the page, so make sure to record it somewhere safe.
> Additionally, generating a new client secret will immediately invalidate the current one, which might make your API requests fail until your app is updated.

When authenticating on behalf of a user, you'll use an __access token__, which uniquely identifies your client and the user to us. There are a few ways to obtain access tokens, as described below. An access token has a list of [scopes](#scope) associated with it, which determine what permissions you are allowed on the authorized Twitch user.

[Applications tab]: http://www.twitch.tv/settings?section=applications


### Getting access tokens

There are three ways to get an __access token__:

  1. If you're making a web app that uses a server, you will probably want to use the [Authorization Code Flow](#wiki-auth-code).
  2. If you are making an app that doesn't use a server, such as a client-side JavaScript app or a mobile app, you'll use the [Implicit Grant Flow](#wiki-implicit-grant).
  3. If you're making a native app or are in a situation where it's very difficult to use a web browser, you may use the [Password Credentials Grant Flow](#password-credentials-grant)

<a name="auth-code"></a>
#### Authorization Code Flow

Remember, you must keep your client secret confidential, so make sure to never expose it to users, even in an obscured form.

  1. Send the user you'd like to authenticate to this URL:
  
        https://api.twitch.tv/kraken/oauth2/authorize
            ?response_type=code
            &client_id=[your client id]
            &redirect_uri=[your registered redirect uri]
            &scope=[list of scopes separated by spaces]

      > We also support the `state` parameter, which is strongly recommended
      > to avoid cross-site scripting attacks. If included, it is appended to
      > the list of query parameters when redirecting the user to the
      > `redirect_uri`.
      
      This page will ask the user to sign up or log in with their Twitch account, and allow them to choose whether to authorize your application.
      
  2. If the user authorizes your application, they will be redirected to the following URL:
  
        https://[your registered redirect URI]/?code=CODE
        
  3. On your server, you can now make the following request to obtain an __access token__:
  
     `POST https://api.twitch.tv/kraken/oauth2/token`
     
     POST Body (URL-encoded)
     
        client_id=[your client ID]
        &client_secret=[your client secret]
        &grant_type=authorization_code
        &redirect_uri=[your registered redirect URI]
        &code=[code received from redirect URI]

     
  4. We'll respond with a JSON-encoded access token:
   
        {
          "access_token": "[user access token]",
          "scope":[array of requested scopes]
        }
  
  You can then use this access token to perform actions on behalf of an authenticated Twitch user as described in [Authenticated Requests](#authenticated-requests).
  
<a id="implicit-grant"></a>
#### Implicit Grant Flow

The Implicit Grant Flow doesn't require a server that must make requests to the API, so you can use this flow with only JavaScript. If you're integrating Twitch into your website, you'll probably want to use the [Twitch JS SDK](https://github.com/justintv/twitch-js-sdk), which uses this flow and makes the integration simple.


  1. Send the user you'd like to authenticate to this URL:
  
        https://api.twitch.tv/kraken/oauth2/authorize
            ?response_type=token
            &client_id=[your client id]
            &redirect_uri=[your registered redirect uri]
            &scope=[list of scopes separated by spaces]

      This page will ask the user to sign up or log in with their Twitch account, and allow them to choose whether to authorize your application.
      
  2. If the user authorizes your application, they will be redirected to the following URL:
  
        https://[your registered redirect URI]/#access_token=[an access token]&scope=[authorized scopes]
        
      > Note that the access token is in the URL fragment, not the
      > querystring, so it won't show up in HTTP requests to your server.
      > URL fragments can be accessed from JavaScript with
      > `document.location.hash`.

That's it! Your application can now make requests on behalf of the user by including your access token as specified in [Authenticated Requests](#authenticated-requests).

<a name="password-credentials-grant"/>
#### Password Credentials Grant Flow
  
If you're building a native app that cannot use a web browser, the [Password Credentials Grant Flow]() might be appropriate. Due to the sensitive nature of user credentials, there are some extra rules and restrictions you have to follow, detailed on the [Password Credentials Grant Flow]() page.

[Password Credentials Grant Flow]: Password-Credentials-Grant
  
<a name="scope"></a>

### Scopes

When requesting authorization from users, the scope parameter allows you to specify which permissions your app requires. These scopes are ties to the access token you receive upon a successful authorization. Without specifying scopes, your app only has access to basic information about the authenticated user. You may specify any or all of the following scopes:

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

You should only ask for permissions that you need, as users can view each requested permission when authorizing your app.

<a name="authenticated-requests"></a>
### Authenticated API Requests

When an api requires authentication, you can send the access token you obtained above in any of the following ways:
 
  * Send token as header:

	    curl -H "Authorization: OAuth [access token]" https://api.twitch.tv/

  * Send token as URL parameter:

	    curl https://api.twitch.tv/kraken?oauth_token=[access token]

  * Send token in the HTTP body (Cannot be used with `GET` and `DELETE` methods)
  
        curl -d 'oauth_token=[access token]' https://api.twitch.tv/kraken/channels/cevtest15/commercial

  
  