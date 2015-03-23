# Hello Gulp

Let's start in a new node project in our folder and add a package.json.
```
$ npm init
```

*/package.json*
```javascript
{
  "name": "learning_gulp",
  "version": "0.0.0",
  "description": "A sample project to learn how Gulp works",
  "main": "index.js",
  "author": "YOUR_NAME_HERE",
  "license": "ISC"
}
```

Time to install gulp using `npm`. For this guide we will just install the package locally for development.

```
$ npm install gulp --save-dev
```

By default gulp looks for a `gulpfile.js` to run. Let's create a simple `gulpfile.js`.

*/gulpfile.js*
```javascript
var gulp = require('gulp');

gulp.task('default', [], function() {
  console.log("Hello Gulp! You are mighty fine.");
});
```

At your terminal run the gulp command.
~~~
$ gulp
~~~
You should see:
~~~
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'default'...
Hello Gulp! You are mighty fine.
Finished 'default' after 118 μs
~~~

Congratulations on your first gulp build script. Both you and the script are amazing!

Enough patting ourselves on the back. On to useful stuff.
