# Markdown + Handlebars = Pages


```js
gulp.task('generate_pages', ['handlebars'], function() {
  return gulp.src(["content/templates/pages.hbs"])
    .pipe(tap(function(file) {
      var template = Handlebars.compile(file.contents.toString())

      gulp.src(["content/pages/**.md"])
        .pipe(markdown())
        .pipe(tap(function(file) {
          var data = {
            content: file.contents.toString()
          }
          var html = template(data)
          file.contents = new Buffer(html, "utf-8")
        }))
        .pipe(gulp.dest('build/pages'));
    }))
});
```
