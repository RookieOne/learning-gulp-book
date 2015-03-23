# Testing

We all know we test our JavaScript. ... you do test your JavaScript right?

Well... you should and with gulp + Karma + Jasmine it is super easy.

First if you have not installed Karma and Jasmine, then do so now.
~~~
> npm install karma-jasmine --save-dev
~~~

Next we will install the `gulp-jasmine` plugin for gulp.

~~~
> npm install gulp-jasmine --save-dev
~~~

We can then create a `test` task to run all the specs found in a `specs` folder we will create.

*/gulpfile.js*
~~~
var jasmine = require("gulp-jasmine");

gulp.task('test', function () {
    gulp.src('content/specs/**.js')
        .pipe(jasmine());
});
~~~

Let's create a basic (failing) test to see that it is working.

*/contents/specs/test.js*
~~~
describe("OMG a JavaScript Test", function() {
  it("should pass", function() {
    expect(true).toBe(false);
  });
});
~~~

~~~
> gulp test
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'test'...
Finished 'test' after 11 ms
F

Failures:

  1) OMG a JavaScript Test should pass
   Message:
     Expected true to be false.
   Stacktrace:
     Error: Expected true to be false.
    at null.<anonymous>

Finished in 0.004 seconds
1 test, 1 assertion, 1 failure
~~~

Now it is time to refactor. We will make the extremely difficult change from `false` to `true`.

~~~
describe("OMG a JavaScript Test", function() {
  it("should pass", function() {
    expect(true).toBe(true);
  });
});
~~~

And run our test suite again.

~~~
Using gulpfile ~/YOUR_DIRECTORY/gulpfile.js
Starting 'test'...
Finished 'test' after 11 ms
.

Finished in 0.003 seconds
1 test, 1 assertion, 0 failures
~~~

Time to refactor? Well, we want refactor our test suite. What we will do is improve our testing by adding a `test-watch` task to run as we edit our JavaScript files.

*/gulpfile.js*
~~~
gulp.task('test-watch', function () {
    gulp.watch(['content/specs/**.js', 'content/javascripts/**.js'], ['test'])
});
~~~

Now when we edit our JavaScript files or our Jasmine specs, the tests will run.

Congratulations, we are offical JavaScript testing wizards.
