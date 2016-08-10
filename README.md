# phoenix-websocket-js
Helpful libraries to connect to a Phoenix-based Websocket (with Channels). 

## phoenix-common.js

This file is a ES5-compatible version of the JavaScript supplied with the Phoenix Framework. You can compile that for yourself from the original source at [phoenixframework/phoenix](https://github.com/phoenixframework/phoenix) when needed.

Here is how to use it:

```javascript
var phoenix = require("./phoenix-common.js")
var socket = new phoenix.Socket("wss://url.to.your.websocket.api", {
  transport: require("websocket").w3cwebsocket,
  params: {auth: "your-means-of-authentication"
}})

socket.connect()
socket.onError(function(err) {console.log("error:", err)})

var channel = socket.channel("your-topic", {
  some_param: true
})

channel.join()
	.receive("ok", function() {console.log("joined")})
	.receive("error", function(reason) {console.log("error:", reason)})

channel.on("message", function(message) {console.log("message", message)})
```
