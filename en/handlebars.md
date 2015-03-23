# Handlebars

For our next magic trick, we are going to generate html files from Handlebar templates.

We are first going to create our Handlebars template for our pages.

*/content/templates/index.hbs*
```html
<html>
<body>
  <h1>{{ title }}</h1>
</body>
</html>
```

This is where things get interesting. Instead of using a gulp plugin to manage the conversion, we are going to use another plugin `gulp-tap` to do some custom operations.

~~~
> npm install handlebars --save-dev
> npm install gulp-tap --save-dev
~~~

*/gulpfile.js*
```js
var tap = require('gulp-tap')
var Handlebars = require('Handlebars')

gulp.task('homepage', function() {
  gulp.src("content/templates/index.hbs")
    .pipe(tap(function(file, t) {
      var template = Handlebars.compile(file.contents.toString())
      var html = template({ title: "Gulp + Handlebars is easy"})
      file.contents = new Buffer(html, "utf-8")
    }))
    .pipe(gulp.dest("build/pages"))
})
```

Let's review the code above.

1. We load the specific `index.hbs` file.
2. Using `tap` we read the file's contents as a string.
3. We then compile that string as a Handlebars template
4. We pass in a JavaScript object with the data we want to pass into the Handlebars template. In this case, it is an object with a `title` property to be used by `{{ title }}`.
5. We take the html returned by Handlebars and return that as the file contents.

Now since we have traced the code and understand the steps, we can run the gulp task.

~~~
> gulp homepage
~~~

You should now be able to find the page we created.

*/build/pages/index.md*
```html
<html>
<body>
  <h1>{{ title }}</h1>
</body>
</html>
```

Hmm... it kept the markdown file extension. Let's fix that. Another plugin to the rescue!

~~~
> npm install gulp-rename --save-dev
~~~

We then use the `gulp-rename` plugin to rename the file extension from `.md` to `.html`.

```js
var tap = require('gulp-tap')
var Handlebars = require('Handlebars')

gulp.task('homepage', function() {
  gulp.src("content/templates/index.hbs")
    .pipe(tap(function(file, t) {
      var template = Handlebars.compile(file.contents.toString())
      var html = template({ title: "Gulp + Handlebars is easy"})
      file.contents = new Buffer(html, "utf-8")
    }))
    .pipe(rename(function(path) {
      path.extname = ".html"
    }))
    .pipe(gulp.dest("build/pages"))
})
```

~~~
> gulp homepage
~~~

And now we should have the desired `html` file extension.

*/build/pages/index.html*
~~~
<html>
<body>
  <h1>{{ title }}</h1>
</body>
</html>
~~~
