## Overview

Twitch Pubsub System (TPS) is a system that allows backend services to broadcast realtime messages to clients. Example applications include:

* An instant messaging service sending a instant messages between friends.
* A backend video system pushing realtime viewer count updates to video players.
* A presence system broadcasting a user's online status to all their friends.

These example applications share a common pattern. On application load, the application fetches a complete snapshot of its state and uses a TPS connection to receive updates to this state. These updates act as 'diffs' to the initial state.

Clients establish a [WebSocket](https://en.wikipedia.org/wiki/WebSocket) connection to our server, listen on topics they care about, and receive messages on those topics in realtime.  Each command or message sent between the client and server is a JSON string encapsulated in one WebSocket frame.

These JSON messages differ depending on message/command type but are typically of the form:
```json
{
  "type": "<type_string>",
  "data": "<json blob>",
}
```

**Terminology**

* A **client** is an end-user session of the Twitch application or a third-party application's integration point.
* A **server** is a Twitch machine which clients connect to for TPS service.
* A **message** is a piece of data which backend services broadcast to interested clients via TPS.  TPS never introspects or mutates messages.
* A **command** is an action that a client issues to the server that modifies the state of the client connection.
* A **topic** is a logical partition of messages that clients may subscribe to for receiving messages.

## Connection management

Clients establish a secure WebSocket connection to `wss://pubsub-edge.twitch.tv`.  To keep the server from closing their connection, clients must send a `PING` command at least once every 5 minutes.  If a client does not receive a `PONG` message within 10 seconds of issuing a `PING` command, it should reconnect to the server. See details in the Best Practices section below.

Clients must `LISTEN` on at least one topic within 15 seconds of establishing the connection or they will be disconnected by the server.

Clients may receive a `RECONNECT` message at any time.  This indicates that the server is about to restart (typically for maintenance) and will disconnect the client within 30 seconds.  During this time, we recommend that clients reconnect to the server. Otherwise, the client will be forcibly disconnected.

### Example connection messages

##### `PING`

```json
// Sent from client to server
{
  "type": "PING"
}
```

##### `PONG`

```json
// Sent from server to client in response to a PING
{
  "type": "PONG"
}
```

##### `RECONNECT`

```json
// Sent from server to client
{
  "type": "RECONNECT"
}
```

## Subscribing to topics

Once a client has established a connection, they can `LISTEN` on topics they care about.  Clients can `LISTEN` on many topics at once and add new topics at any time by issuing new `LISTEN` commands.  Once a client no longer cares about a particular set of topics, they can issue `UNLISTEN` commands to stop receiving messages on those topics.  Some topics can be `LISTEN`ed to by any clients while others require OAuth tokens.

##### Request Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50px">Type</th>
            <th width="100%">Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>type</code></td>
            <td>required</td>
            <td>string</td>
            <td>Set to 'LISTEN' or 'UNLISTEN'.</td>
        </tr>
        <tr>
            <td><code>nonce</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Random string to identify the response associated with this request.</td>
        </tr>
        <tr>
            <td><code>data</code></td>
            <td>required</td>
            <td>JSON</td>
            <td>Wraps the `topics` and `auth_token` fields.</td>
        </tr>
        <tr>
            <td><code>topics</code></td>
            <td>required</td>
            <td>string[]</td>
            <td>A list of topics to listen on.</td>
        </tr>
        <tr>
            <td><code>auth_token</code></td>
            <td>required for some topics</td>
            <td>string</td>
            <td>OAuth token required for listening on some topics.</td>
        </tr>
    </tbody>
</table>

##### Response Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th width="50px">Type</th>
            <th width="100%">Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>type</code></td>
            <td>string</td>
            <td>Set to 'RESPONSE'.</td>
        </tr>
        <tr>
            <td><code>nonce</code></td>
            <td>string</td>
            <td>The same nonce passed into the client request.</td>
        </tr>
        <tr>
            <td><code>error</code></td>
            <td>string</td>
            <td>The error message associated with the request or empty string if there is no error.</td>
        </tr>
    </tbody>
</table>

### Example request and response
```json
// Request from client to server
{
  "type": "LISTEN",
  "nonce": "44h1k13746815ab1r2",
  "data": {
    "topics": ["whispers.test_account","video-playback.lirik"],
    "auth_token": "...",
  }
}
// Response from server to client
{
  "type": "RESPONSE",
  "nonce": "44h1k13746815ab1r2",
  "error": "",
}
```

## Receiving messages

Clients that have listened on a set of topics will receive message streams to those topics.

##### Message Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th width="50px">Type</th>
            <th width="100%">Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>type</code></td>
            <td>string</td>
            <td>Set to 'MESSAGE'.</td>
        </tr>
        <tr>
            <td><code>data</code></td>
            <td>JSON</td>
            <td>Wraps the `topic` and `message` fields.</td>
        </tr>
        <tr>
            <td><code>topic</code></td>
            <td>string</td>
            <td>The topic the message is being sent on.</td>
        </tr>
        <tr>
            <td><code>message</code></td>
            <td>string</td>
            <td>The body of the message.</td>
        </tr>
    </tbody>
</table>

### Example message
```json
{
  "type": "MESSAGE",
  "data": {
    "topic": "video-playback.lirik",
    "message": "..."
  }
}
```

## Best Practices and API limits

#### Handling connection failures

*  When a client encounters a situation where it must reconnect to the server, it should first establish a new successful WebSocket connection and then issue a `LISTEN` command that contains the set of topics that the application expects to receive messages on.
*  If a client fails to connect to the server or is disconnected from the server, it should reconnect to the server using an exponential backoff.  Our official client implementation initially waits one second (plus a small random jitter - see below) to retry a failed connection and doubles the backoff period on subsequent failures, up to a maximum backoff threshold of 2 minutes.  This prevents some "stampeding herd" situations where many clients simultaneously connect to the server.
*  If a client uses timers to issue `PING` commands, it should add a small random jitter to the timer.  This prevents some situations where many clients issue `PING` commands simultaneously.
*  After a client reconnects to the server, some applications should fetch fresh state in order to compensate for any missed messages while the connection was broken.  For instance, our Whispers application fetches new messages on reconnect (as it does on initial page load) in case the user received any new messages while the connection was down.

#### Limits

*  Clients can currently listen on up to 10 topics per connection. Attemping to listen on any more topics will result in an error message.
*  We recommend that a single client IP address establishes no more than 10 instantaneous connections.
*  The previous two limits are likely to be relaxed for approved third-party applications as we start to better understand third-party requirements.
*  Malicious or careless applications that result in abnormally high server load may be blacklisted from establishing connections.
*  If clients are slow to read messages from their connection and the server is instantaneously buffering more than 30 messages to an individual client, the client will be disconnected.

#### Authentication

Some topics require an OAuth token to `LISTEN` on.  These topics typically have a particular required scope and, in some cases, a whitelisted set of client IDs that may `LISTEN` to them.