# Creating a webpage

Moving CSS and JavaScript files is all well and good, but we do actually want webpages right?

Let's start our webpage generation with a simple `index.html` file.

*/contents/index.html*
```
<!DOCTYPE html>
<html>
<body>
  <h1>Hello Gulp!</h1>
</body>
</html>
```

We will then create a simple `homepage` task to move the `index.html` file to our build directory.

```javascript
gulp.task("homepage", ["clean"], function() {
  return gulp.src("contents/index.html")
          .pipe(gulp.dest("build"))
})
```

Hmmm, it would be nice to be able to preview our website as we generate the content. Let's do that next.
