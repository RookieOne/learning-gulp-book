# Creating a simple Connect server

Let's use node and the `connect` library to create a local server to serve our webpages we generate with our build.

This way we can see what the webpages will look like as we development.

~~~
$ npm install connect --save-dev
$ npm install serve-static --save-dev
~~~

The http server we will create is going to be very basic. It will just serve the static files found in the `build` directory.

We will add a `logger` function to output the request path for every request.

We will also add an `errorHandler` function so we can see what errors we get in the terminal.

*/server.js*
~~~
var connect = require("connect");
var serveStatic = require('serve-static');

var app = connect();

function logger(req, res, next) {
  console.log("%s %s", req.method, req.url);
  next();
}

function errorHandler(err, req, res, next) {
  console.log("Error!");
  res.statusCode = 500;
  res.setHeader("Content-Type", "application/json");
  res.end(JSON.stringify(err));
}

app.use(logger);
app.use(serveStatic(__dirname + "/build"))
app.use(errorHandler);
app.listen(3000);

~~~

To start the server, type in the terminal:
~~~
$ node server.js
~~~
