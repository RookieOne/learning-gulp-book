# Handling Errors with Streams


What if the file was named incorrectly? What happens?

Change `index.html` to `OMG_WRONG_FILE.html` and rerun the script.

*/streams.js*
```javascript
var fs = require("fs")

var stream = fs.createReadStream(__dirname + "/content/pages/OMG_WRONG_FILE.html")
stream.on("data", function(chunk) {
  // just output chunk to terminal
  console.log(chunk.toString())
})
stream.on("end", function() {
  console.log("END")
})
```

Running the script this time results in:
```
> node streams.js
events.js:72
        throw er; // Unhandled 'error' event

Error: ENOENT, open '~/YOUR_DIRECTORY/OMG_WRONG_FILE.html'
```

If we read the error message carefully, then we can see that there is an `error` event we can listen to. So lets listen for that event.

*/streams.js*
```javascript
var fs = require("fs")

var stream = fs.createReadStream(__dirname + "/content/pages/index.html");
stream.on("data", function(chunk) {
  console.log(chunk.toString())
})
stream.on("end", function() {
  console.log("END")
})
stream.on("error", function(er) {
  console.log("error", er)
})
```

Now we rerun the script and see:

```
> node streams.js
error { [Error: ENOENT, open '/Users/jonathanbirkholz/js/gulptest/contents/OMG_WRONG_FILE.html']
  errno: 34,
  code: 'ENOENT',
  path: '~/YOUR_DIRECTORY/contents/OMG_WRONG_FILE.html' }
```

And that is it for now. We will come back and use some of what we learned later.
