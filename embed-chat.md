# Embedding Twitch Chat

## Parameters
- `channel` : Channel the chat belongs to.
- `height`  : Chat window height.
- `width`   : Chat window width.

## Code

```html
<iframe frameborder="0" 
        scrolling="no" 
        id="chat_embed" 
        src="http://www.twitch.tv/{CHANNEL}/chat" 
        height="{HEIGHT}" 
        width="{WIDTH}">
</iframe>
```

## Example

```html
<iframe frameborder="0" scrolling="no" id="chat_embed" src="http://www.twitch.tv/hebo/chat" height="500" width="350"></iframe>
```
