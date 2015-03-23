# Streams

Before we continue, I think a brief detour to cover some basics of Node streams would be helpful.

Lets create a simple Node script to read that `index.html` file we just created.


First we require the file system library `fs`.

*/streams.js*
```javascript
var fs = require("fs")
```

Next we will create a read stream from that file.

*/streams.js*
```javascript
var stream = fs.createReadStream(__dirname + "/content/pages/index.html")
```
`__dirname` is a helper that returns the absolute path of the code file being run.


Node reads files asynchronously. This is normally where we could dive into what "non-blocking I/O" means vs threads, etc. This is a book about gulp though so I will keep this detour basic.

For our purposes, this means that we have to listen to **events** from the stream to be able to read the file.

The events we are going to listen to are `data` and `end`.

`data` fires when a chunk of the file has been read and returned. **This chunk is not always the entire file.** In fact, you should assume it is not the entire file.

*/streams.js*
```javascript
stream.on("data", function(chunk) {
  // just output chunk to terminal
  console.log(chunk.toString())
})
```

`end` fires when the file has been completly read.

*/streams.js*
```javascript
stream.on("end", function() {
  console.log("END")
})
```

Now altogether, `streams.js` looks like:

*/streams.js*
```javascript
var fs = require("fs")

var stream = fs.createReadStream(__dirname + "/content/pages/index.html")
stream.on("data", function(chunk) {
  // just output chunk to terminal
  console.log(chunk.toString())
})
stream.on("end", function() {
  console.log("END")
})
```

Now if you run the node script in the terminal, you should see:

```
> node streams.js
<!DOCTYPE html>
<html>
<head>
  <title>Learning Gulp</title>
</head>
<body>
  <h1>Hello Gulp!</h1>
</body>
</html>
END
```
