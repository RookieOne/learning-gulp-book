# Min: Honey I shrunk my CSS

Now since we have our css in a single file, we can continue to increase the performance of our site by minifying our css. Minifying is the process of eliminating all the unnecessary formatting in a css file. Human's need spaces and tabs (also known as white space) to more easily read the styles. A browser doesn't care about white space so we can make the file smaller by removing them.

You should start seeing a pattern when using gulp.... because for this we need to use a plugin. :P

```
$ npm install gulp-minify-css --save-dev
```
* For more information on `gulp-minify-css`, check out https://www.npmjs.org/package/gulp-minify-css/

*/gulpfile.js*
```javascript
var gulp = require("gulp");
var clean = require("gulp-rimraf");
var concat = require("gulp-concat");
var cssmin = require("gulp-minify-css");

gulp.task("clean", [], function() {
  return gulp.src("build/**/**.*").pipe(clean());
});

gulp.task("default", ["clean"], function() {
  return gulp.src("contents/styles/**.*")
          .pipe(concat("main.min.css"))
          .pipe(cssmin())
          .pipe(gulp.dest("build/styles"));
});
```


```javascript
> gulp
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'clean'...
Finished 'clean' after 13 ms
Starting 'default'...
Finished 'default' after 17 ms
```

Our `build/styles/main.min.css` should now look like:

```css
p{font-size:30px}h1{color:red}
```

We have successfully moved our `css` files, concat'd them together, and now minified them into a tiny, optimized package.
