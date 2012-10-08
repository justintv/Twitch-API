# Password Credentials Grant

The password credentials grant type allows you to request an access token for a user without using a browser by sending a user's username and password to the password grant endpoint.

This authorization flow allows clients that cannot use a browser to get an access token for Twitch users. Your application can present a username and password prompt to the user, but should not store a user's credentials any longer than is necessary to retrieve an access token.

Due to the sensitive nature of handling user passwords, this type of authorization flow is only permitted on a case-by-case basis. If you think your application is a good candidate, please contact us directly.

## Usage

First, register a [client application][]. The `redirect_uri` is only used for browser-based authorization flows, so you can set this to any domain you own.

[client application]: http://www.twitch.tv/settings?section=applications

Next, make a request to our token endpoint with user credentials to get an access token

    POST https://api.twitch.tv/kraken/oauth2/token

### Parameters

- `grant_type` (required): `password`
- `client_id` (required): The Client ID of your app that you received upon creation.
- `client_secret` (required): The Client Secret of your app.
- `username` (required): The username of the Twitch user.
- `password` (required): The password of the Twitch user.
- `scope` (required): A **space separated** list of [scopes](API#wiki-scope) your app is requesting approval for.

### Response

    {"scope":["user_read"],"access_token":"df4yofxyn2s7240ojfrh9chz8"}%  

### Example

    $ curl -X POST -d "client_id=<myclient>&client_secret=<myclientsecret>&username=<myuser>&password=<mypass>&scope=user_read&grant_type=password" https://api.twitch.tv/kraken/oauth2/token
    {"scope":["user_read"],"access_token":"df4yofxyn2s7640ojfrh9chz8"}%       