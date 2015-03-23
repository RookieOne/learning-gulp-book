# Moving files

The first amazing thing we will do is learn to move files using gulp.

Let's make some files to move.

*/styles/some_styles.css*
```css
h1 {
  color: red;
}
```

*/styles/more_styles.css*
```css
p {
  font-size: 30px;
}
```

Our project structure should now look like:
```
/node_modules
/contents
  /styles
    main.css
    some_styles.css
gulpfile.js
package.json
```

Time to move some files!

Update our `gulpfile.js` from the previous section and instruct gulp to move all the files found in the `styles` folder to our `build/styles` folder.

*/gulpfile.js*
```javascript
var gulp = require('gulp');

gulp.task('default', [], function() {
  console.log("Moving all files in styles folder");
  gulp.src("styles/**.*")
      .pipe(gulp.dest('build/styles'));
});
```

If we review the code, we can see two main gulp operations.

1. `gulp.src` tells gulp what files to work on with this task.

2. `gulp.dest` tells gulp where to drop off files after this task is finished working on them.

What do we expect will happen when we run `gulp`?

If you guessed the files will be copied and moved to the `build/styles` folder, then give yourself a cookie.

When we run `gulp`, we should see:
```
> gulp
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'default'...
Moving all files in styles folder
Finished 'default' after 5.25 ms
```

Our project should now look like:
```
/build
  /styles
    some_styles.css
    more_styles.css
/node_modules
/contents
  /styles
    some_styles.css
    more_styles.css
gulpfile.js
package.json
```

Unimpressed? That just means you totally understand everything and are ready to move on with our great gulp adventure.
