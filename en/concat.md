# Concat: Combining files into one

Printing `Hello` and moving files is rather boring. Let's do something productive.

When we create websites, we are always trying to deliver the best experience possible. This includes having our webpages displaying fast. Back in the day, this meant having all our styles in one css file.

While this made our webpages load faster, it made maintaining the css file a nightmare!

These days we can use multiple css files for better organization and then concat (meaning merge or combine) the files together into one large file.

We left our project looking like:

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

Right now, we have two separate css files in our `build/styles` folder. We are going to use a gulp plugin to concat all our css files in the `styles` folder.

Gulp contains some basic tasks, but the power of gulp is the customization you can bring into your build process by using plugins.
* For a list of all the gulp plugins available, go to http://gulpjs.com/plugins/

To concat the files together, we will need to install one of these plugins.
```
$ npm install gulp-concat --save-dev
```
* For more information on the `gulp-concat` plugin, visit https://www.npmjs.org/package/gulp-concat/.

We can then update our `default` gulp task to concat the files.

*/gulpfile.js*
```javascript
var gulp = require('gulp');
var concat = require('gulp-concat');

gulp.task('default', [], function() {
  console.log("Concating and moving all the css files in styles folder");
  gulp.src("contents/styles/**.css")
      .pipe(concat('main.css'))
      .pipe(gulp.dest('build/styles'));
});
```

Couple of things have changed, can you spot them?

First, we had to reference the gulp plugin with:
```javascript
var concat = require('gulp-concat');
```

We chose to label this `concat`. Obviously we could call it anything we want, but `concat` communicates what the plugin does to those reading our build script.

Second, we added another step to our task. In between the `src` and the `pipe(gulp.dest...)` steps, we added `pipe(concat(...))`.

Gulp works by streaming files from one process to another. This allows us to create complex build tasks out of small, simple steps. Composition == winning.

Now run our gulp task:

```
> gulp
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'default'...
Moving all the css files in styles folder
Finished 'default' after 6.09 ms
```

Our task will read all the css files in the `styles` folder, combine them into one `main.css` file, and then place that file in the `build/styles` folder.

Our project should now look like:

```
/build
  /styles
    main.css
    more_styles.css
    some_styles.css
/node_modules
/styles
  more_styles.css
  some_styles.css
gulpfile.js
package.json
```

Notice the `more_styles.css` and `some_styles.css` files are still in our build folder. :(

We don't want those chumps there anymore. In the next chapter we will learn how to get rid of those files.
