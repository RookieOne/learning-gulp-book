# Notify

In the previous section, we used gulp to validate our JavaScript. The error message would appear in the console. While this is awesome, there is a chance we could miss it.

Let's use notifications to display a pop up window when we have a JavaScript error.

There is a gulp plugin to send notifications. True story.

~~~
> npm install gulp-notify
~~~

* For more information on `gulp-notify` check out https://www.npmjs.org/package/gulp-notify/
* For Windows, be sure to install Growl for Windows (http://www.growlforwindows.com/gfw/default.aspx)

Remember that gulp uses node's streaming. It shouldn't be a surprise that when `gulp-jsvalidate` finds an error, it emits an `error` event.

All we need to do is handle the event and use `gulp-notify` to send a notification with the error message.

*/gulpfile.js*
```js
...
var notify = require('gulp-notify');
...

...
gulp.task('javascript', function () {
  console.log("Validate all the javascript files in the content/javascript folder");

  return gulp.src(["content/javascripts/**.js"])
      .pipe(jsValidate())
      .on("error", notify.onError(function(error) {
        return error.message;
      }))
});
...
```
