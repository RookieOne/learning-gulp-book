# Uglify

For JavaScript files we also want to uglify them. Uglifying JavaScript involves changing variable and function names to reduce their size. So a variable named `customer` might be renamed to `x`. JavaScript engines don't care about descriptive names, only developers.

So how do we uglify JavaScript files with gulp?

I know what you are going to say: "Blah, blah, blah... there is a plugin." And you are correct.

~~~
> npm install gulp-uglify --save-dev
~~~
* For more information on `gulp-uglify`, check out https://www.npmjs.org/package/gulp-uglify/


Next, we need to add the uglification step to our `javascript` task.

*/gulpfile.js*
```js
var jsValidate = require('gulp-jsvalidate');
var notify = require('gulp-notify');
var uglify = require('gulp-uglify');

gulp.task('javascript', function () {
  console.log("Validate all the javascript files in the content/javascript folder");

  return gulp.src(["content/javascripts/**.js"])
      .pipe(jsValidate())
      .pipe(uglify())
      .pipe(concat('main.js'))
      .pipe(gulp.dest('build/javascripts'))
      .on("error", notify.onError(function(error) {
        return error.message;
      }))
});
```
