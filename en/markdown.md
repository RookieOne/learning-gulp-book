# Markdown

Now for something atypical. We are going to use gulp + Handlebars to create our own Jekyll-like CMS system.

First, we want to be able to process markdown files and create html files.

SURPRISE! gulp plugin.

~~~
$ npm install gulp-markdown --save-dev
~~~
* For more information on `gulp-markdown`, check out https://www.npmjs.org/package/gulp-markdown/

We will read all the markdown files in the `content/pages` folder and generate html files.

*/gulpfile.js*
```js
var markdown = require('gulp-markdown')

gulp.task('generate_pages', function() {
  gulp.src('content/pages/**.md')
    .pipe(markdown())
    .pipe(gulp.dest("build/pages"))
})
```

... that is it.
