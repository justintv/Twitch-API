# Channel Feed

| Endpoint | Description |
| ---- | --------------- |
| [GET /feed/:channel/posts](/v3_resources/channel_feed.md#get-feedchannelposts) | Get channel feed posts |
| [POST /feed/:channel/posts](/v3_resources/channel_feed.md#post-feedchannelposts) | Create post |
| [GET /feed/:channel/posts/:id](/v3_resources/channel_feed.md#get-feedchannelpostsid) | Get post |
| [DELETE /feed/:channel/posts/:id](/v3_resources/channel_feed.md#delete-feedchannelpostsid) | Delete post |
| [POST /feed/:channel/posts/:id/reactions](/v3_resources/channel_feed.md#post-feedchannelpostsidreactions) | Create reaction to post |
| [DELETE /feed/:channel/posts/:id/reactions](/v3_resources/channel_feed.md#delete-feedchannelpostsidreactions) | Delete reaction |

[users]: /v3_resources/users.md

## `GET /feed/:channel/posts`

Returns a list of posts that belong to the channel's feed. Uses limit and cursor pagination.

*__Authenticated__*, optional scope: `channel_feed_read`

If authentication is provided, the user_ids array in the reaction body contains the requesting user's user_id if they have reacted to the corresponding post.

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>limit</code></td>
            <td>optional</td>
            <td>integer</td>
            <td>Maximum number of objects in array. Default is 10. Maximum is 100.</td>
        </tr>
        <tr>
            <td><code>cursor</code></td>
            <td>optional</td>
            <td>string</td>
            <td>Cursor value to begin next page</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/feed/bangbangalang/posts?limit=1
```

### Example Response

```json
{
  "_total": 8,
  "_cursor": "1454101643075611000",
  "posts": [{
    "id": "20",
    "created_at": "2016-01-29T21:07:23.075611Z",
    "deleted": false,
    "emotes": [ ],
    "reactions": {
      "endorse": {
        "count": 2,
        "user_ids": [ ]
      }
    },
    "body": "Kappa post",
    "user": {
      "display_name": "bangbangalang",
      "_id": 104447238,
      "name": "bangbangalang",
      "type": "user",
      "bio": "i like turtles and cats",
      "created_at": "2015-10-15T19:52:17Z",
      "updated_at": "2016-01-29T21:06:42Z",
      "logo": null,
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/bangbangalang"
      }
    }
  }]
}
```

## `POST /feed/:channel/posts`

Create a post for a channel's feed.

Use `share=true` to tweet out the post on the user's twitter (if connected).

*__Authenticated__*, required scope: `channel_feed_edit`

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>content</code></td>
            <td>required</td>
            <td>string</td>
            <td>Content of the post</td>
        </tr>
        <tr>
            <td><code>share</code></td>
            <td>optional</td>
            <td>boolean</td>
            <td>When set to true, shares the post, with a link to the post URL, on the channel's Twitter if it's connected.</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X POST https://api.twitch.tv/kraken/feed/bangbangalang/posts \
-d '{"content":"Hello this is post"}'
```

### Example Response

```json
{
  "post": {
    "id": "21",
    "created_at": "2016-01-29T21:07:23.075611Z",
    "deleted": false,
    "emotes": [ ],
    "reactions": {},
    "body": "New post",
    "user": {
      "display_name": "bangbangalang",
      "_id": 104447238,
      "name": "bangbangalang",
      "type": "user",
      "bio": "i like turtles and cats",
      "created_at": "2015-10-15T19:52:17Z",
      "updated_at": "2016-01-29T21:06:42Z",
      "logo": null,
      "_links": {
        "self": "https://api.twitch.tv/kraken/users/bangbangalang"
      }
    }
  },
  "tweet": "http://twitter.com/blah/status/23469487ruo4"
}
```

## `GET /feed/:channel/posts/:id`

Returns a post belonging to the channel.

*__Authenticated__*, optional scope: `channel_feed_read`

If authentication is provided, the user_ids array in the reaction body contains the requesting user's user_id if they have reacted to the post.

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X GET https://api.twitch.tv/kraken/feed/bangbangalang/posts/20
```

### Example Response

```json
{
  "id": "20",
  "created_at": "2016-01-29T21:07:23.075611Z",
  "deleted": false,
  "emotes": [ ],
  "reactions": {
    "endorse": {
      "count": 2,
      "user_ids": [104447238]
    }
  },
  "body": "Kappa post",
  "user": {
    "display_name": "bangbangalang",
    "_id": 104447238,
    "name": "bangbangalang",
    "type": "user",
    "bio": "i like turtles and cats",
    "created_at": "2015-10-15T19:52:17Z",
    "updated_at": "2016-01-29T21:06:42Z",
    "logo": null,
    "_links": {
      "self": "https://api.twitch.tv/kraken/users/bangbangalang"
    }
  }
}
```

## `DELETE /feed/:channel/posts/:id`

Delete a post.

*__Authenticated__*, required scope: `channel_feed_edit`

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X DELETE https://api.twitch.tv/kraken/feed/bangbangalang/posts/20
```

## `POST /feed/:channel/posts/:id/reactions`

Create a reaction to a post.

*__Authenticated__*, required scope: `channel_feed_edit`

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>emote_id</code></td>
            <td>required</td>
            <td>string</td>
            <td>Single emote id (ex: "25" => Kappa) or the string "endorse"</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X POST https://api.twitch.tv/kraken/feed/bangbangalang/posts/21/reactions?emote_id=25
```

### Example Response

```json
{
  "id": "25",
  "created_at": "2016-01-29T21:07:23.075611Z",
  "emote_id": "25",
  "user": {
    "display_name": "bangbangalang",
    "_id": 104447238,
    "name": "bangbangalang",
    "type": "user",
    "bio": "i like turtles and cats",
    "created_at": "2015-10-15T19:52:17Z",
    "updated_at": "2016-01-29T21:06:42Z",
    "logo": null,
    "_links": {
      "self": "https://api.twitch.tv/kraken/users/bangbangalang"
    }
  }
}
```

## `DELETE /feed/:channel/posts/:id/reactions`

Delete a reaction to a post.

*__Authenticated__*, required scope: `channel_feed_edit`

Deletes a reaction by the requesting user on the target post.

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th width="50">Type</th>
            <th width=100%>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>emote_id</code></td>
            <td>required</td>
            <td>string</td>
            <td>Single emote id (ex: "25" => Kappa) or the string "endorse"</td>
        </tr>
    </tbody>
</table>

### Example Request

```bash
curl -H 'Accept: application/vnd.twitchtv.v3+json' -H 'Authorization: OAuth <access_token>' \
-X DELETE https://api.twitch.tv/kraken/feed/bangbangalang/posts/21/reactions?emote_id=25
```


