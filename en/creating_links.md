```javascript
gulp.task("read-pages", ["clean"], function() {
  Data.pages = []
  return gulp.src("contents/pages/**.md")
      .pipe(tap(function(file) {
        var contents = file.contents.toString()
        var index = contents.indexOf("---")
        if (index === -1) {
          return
        }
        var data = JSON.parse(contents.slice(0, index))
        data.url = "/pages/" + file.relative.replace(".md", ".html")
        console.log(data)
        Data.pages.push(data)
        contents = contents.slice(index+3, contents.length)
        file.contents = new Buffer(contents, "utf-8")
      }))
      .pipe(markdown())
      .pipe(gulp.dest("tmp/pages"))
})
```
