# Validate JavaScript

The web runs on more than HTML and CSS. It runs on JavaScript!

Let's perform some common JavaScript build operations with gulp.

We will first look into validating our JavaScript using gulp.

And yes... there is a plugin for that.

```
> npm install gulp-jsvalidate --save-dev
```

* For more information on `gulp-jsvalidate` check out https://github.com/sindresorhus/gulp-jsvalidate

We will now create a new `javascript` task in our `gulpfile.js`. At first, all we will do is validate our javascript in a new `content/javascripts` folder.

*Add to /gulpfile.js*
```js
...
var jsValidate = require('gulp-jsvalidate');
...

...
gulp.task('javascript', function () {
    return gulp.src("content/javascripts/**.js")
        .pipe(jsValidate());
});
...
```

Time to test out our new task and plugin.

Create a javascript file and make a syntax error.

*/contests/javascript/somejs.js*
```js
function OMG() {
  var x * 2;
  return x + 10;
}
```

Now when we run our `javascript` task, we will get an error message in the terminal.

```
> gulp javascript
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'javascript'...
'javascript' errored after 14 ms gulp-jsvalidate: Line 3: Unexpected token *
```

When we fix the error and then run our gulp task, we won't get that error message.

*/contests/javascript/somejs.js*
```js
function OMG() {
  var x = 2;
  return x + 10;
}
```

```
> gulp javascript
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'javascript'...
Finished 'javascript' after 14 ms
```

Sweet! Gulp can now check if our JavaScript is valid. But the error message in the console is rather bland, lets find a better way to tell us that we messed up.
