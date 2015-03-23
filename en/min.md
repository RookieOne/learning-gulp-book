# Min: Honey I shrunk my CSS

Now since we have our css in a single file, we can continue to increase the performance of our site by minifying our css. Minifying is the process of eliminating all the unneccessary formatting in a css file. Human's need white space to more easily read the styles. A browser doesn't care about spacesand tabs (also known as white space) so we can make the file smaller by removing them.

You should start seeing a pattern when using gulp.... because for this we need to use a plugin. :P

```
> npm install gulp-minify-css --save-dev
```
* For more information on `gulp-minify-css`, check out https://www.npmjs.org/package/gulp-minify-css/

*/gulpfile.js*
```javascript
var gulp = require("gulp")
var clean = require("gulp-clean")
var concat = require("gulp-concat")
var cssmin = require("gulp-minify-css")

gulp.task("clean", [], function() {
  return gulp.src("build/**/**.*").pipe(clean())
})

gulp.task("default", ["clean"], function() {
  return gulp.src("styles/**.*")
          .pipe(concat("main.min.css"))
          .pipe(cssmin())
          .pipe(gulp.dest("build/styles"))
})
```


```javascript
> gulp
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'clean'...
Finished 'clean' after 13 ms
Starting 'default'...
Finished 'default' after 17 ms
```
