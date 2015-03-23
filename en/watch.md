# Watch

TODO: change to show more with watch


Now for something super amazing. Instead of running the gulp task explicitly, lets have gulp run our tasks when the files change.

Guess what? ... there isn't a plugin for this. It is just part of gulp.

We will create a gulp `watch` task to watch our `styles` folder and run our `default` task on file change.

*/gulpfile.js*
```javascript
...
gulp.task('watch', [], function() {
  return gulp.watch(['contents/**.*'], ['default']);
})
...
```

At the terminal type:
~~~
> gulp watch
~~~

If you update any of the css files in the styles folder, you should see gulp run the `default` task.

~~~
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'watch'...
Finished 'watch' after 7.22 ms
Starting 'clean'...
Finished 'clean' after 5.41 ms
Starting 'default'...
Finished 'default' after 1.74 ms
~~~
