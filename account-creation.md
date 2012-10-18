# Account Creation API

The account creation API allows you to create Twitch user accounts programmatically. Due to the potential for abuse, this permission is given to applications on an invite-only basis. Additionally, all requests must include a secret key to verify your client and be performed from an authorized IP Address.

Once you create an account, you can use the [Password Credentials Grant Flow][] to get an access token for the user, allowing you to perform actions on their behalf.

[Password Credentials Grant Flow]: password-credentials.md

## Usage

First, register a [client application][]. You'll send the `client id` when making requests to the API.

Next, you'll need a `client secret` for your app, which you will send with your requests for verification.

The `client secret` is an alphanumeric string, equivalent to a password, that's tied to your `client id`. Generate this on your client page, and never reveal this to anyone or transmit it over an insecure protocol.

Additionally, this account creation permission is tied to specific IP addresses, so let us know which IP address ranges to whitelist.


[client application]: http://www.twitch.tv/settings?section=applications


Now you can make requests to our account creation endpoint with your client credentials to create new users

```bash
POST https://api.twitch.tv/kraken/users
```

### Parameters

- `client_id` (required): The _client id_ of your app that you recieved upon creation.
- `client_secret` (required): The _client secret_ associated with your client.
- `username` (required): The username of the Twitch user you wish to create.
- `password` (required): The password of the Twitch user you wish to create.
- `email` (required): The email address of the Twitch user you wish to create.

### Response

#### Success

`201 Created` with the `Location` HTTP header set to the url of the newly created user.

#### Failures

`422 Unprocessable Entity` if the user could not be created with the provided attributes (login taken, password too short). The `message` property in the response provides more detail.

```json
{
  "error": "Unprocessable Entity",
  "status": 422,
  "message": "Login has already been taken"
}
```

`403 Forbidden` if you do not have permission to perform an account creation, typically due to an incorrect client id and secret combination, or this request is being performed from an unauthorized IP address.

```json
{
  "error": "Unauthorized",
  "status": 401,
  "message": "Invalid client secret abc123"
}
```

`400 Bad Request` if your request is missing required parameters or is otherwise invalid.

### Example

    $ curl -X POST -d 'login=newuser&password=12345&email=my@email.com' \
      'https://api.twitch.tv/kraken/users?client_id=[your client id]&client_secret=[your client secret]'     
