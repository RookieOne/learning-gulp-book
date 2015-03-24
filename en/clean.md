# Cleaning our build folder

A normal part of a build process is a cleaning task to remove all the old files in the build folder.

For us, this means getting rid of the leftover `more_styles.css` and `some_styles.css` files in our `build/styles` folder.

To clean files, we will need another gulp plugin.
```
$ npm install gulp-rimraf --save-dev
```

* For more information on gulp-clean check out https://www.npmjs.org/package/gulp-rimraf
* This task used to be handled by `gulp-clean` but has been replaced by `gulp-rimraf`

Instead of adjusting our `default` task, lets create a new task to clean out the directory.

*/gulpfile.js*
```javascript
var gulp = require('gulp');
var concat = require('gulp-concat');
var clean = require('gulp-rimraf');

gulp.task('clean', [], function() {
  console.log("Clean all files in build folder");

  gulp.src("build", { read: false })
      .pipe(clean());
});

gulp.task('default', [], function() {
  console.log("Concating and moving all the css files in styles folder");
  gulp.src("contents/styles/**.css")
      .pipe(concat('main.css'))
      .pipe(gulp.dest('build/styles'));
});
```

So like before, we need to require `gulp-rimraf`.

This time though, we created a new task called `clean`. We tell this task to look at all the files in the `build` folder and then pipe them to our `clean` operation. This will delete the files.

To run our clean task from the command line, we just tell gulp which task to run:
```
$ gulp clean
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'clean'...
Clean all files in build folder
Finished 'clean' after 8.95 ms
```

What we would like is to run our `clean` task before we run our `default` task. That way our build folder will be nice and empty before we starting moving files there.

You might have been wondering what the empty array (`[]`) was before our `function`. This is where we specify dependency tasks. A *dependency task* is a task that needs to be completed before gulp can run the current task.

So for our scenario, our `clean` task is a dependency for `default`.

*/gulpfile.js*
```javascript
var gulp = require('gulp');
var concat = require('gulp-concat');
var clean = require('gulp-rimraf');

gulp.task('clean', [], function() {
  console.log("Clean all files in build folder");
  gulp.src("build/**.*")
      .pipe(clean());
});

gulp.task('default', ['clean'], function() {
  console.log("Concating and moving all the css files in styles folder");
  gulp.src("contents/styles/**.css")
      .pipe(concat('main.css'))
      .pipe(gulp.dest('build/styles'));
});
```

Now when we run our `default` gulp task, we should see that it runs the `clean` task before `default`.

```
> gulp
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'clean'...
Clean all files in build folder
Finished 'clean' after 9.03 ms
Starting 'default'...
Concating and moving all files from styles folder
Finished 'default' after 8.42 ms
```

The plot thickens! We continue to build on our past knowledge. Now we can specify dependent tasks creating a chain of operations.
