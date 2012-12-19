# grunt-qunit-junit

> JUnit compatible XML reporter for QUnit

**WARNING**: This plugin is currently dependant on a branch of `grunt-contrib-qunit`. This will be cleaned up in the near future, when more testing has been completed. [See the branch](https://github.com/sbrandwoo/grunt-contrib-qunit/tree/fail-events) for the changes.

This plugin produces XML reports for all QUnit tests that you run with grunt. The XML reports match those created by JUnit and are perfect for loading into Jenkins.

This plugin only works with grunt 0.4.x. If you are using 0.3.x, then I recommend the [grunt-junit plugin](https://github.com/johnbender/grunt-junit).


## Getting Started
_If you haven't used [grunt][] before, be sure to check out the [Getting Started][] guide._

From the same directory as your project's [Gruntfile][Getting Started] and [package.json][], install this plugin with the following command:

**WARNING**: This plugin has not yet been released, so the following commands won't work quite yet.

```bash
npm install grunt-qunit-junit --save-dev
```

Once that's done, add this line to your project's Gruntfile:

```js
grunt.loadNpmTasks('grunt-qunit-junit');
```

If the plugin has been installed correctly, running `grunt --help` at the command line should list the newly-installed plugin's task or tasks. In addition, the plugin should be listed in package.json as a `devDependency`, which ensures that it will be installed whenever the `npm install` command is run.

[grunt]: http://gruntjs.com/
[Getting Started]: https://github.com/gruntjs/grunt/blob/devel/docs/getting_started.md
[package.json]: https://npmjs.org/doc/json.html

## The "qunit_junit" task

### Overview
In your project's Gruntfile, add a section named `qunit_junit` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({

  qunit_junit: {
    options: {
      // Task-specific options go here.
    }
  },
})
```

### Options

#### options.dest
Type: `String`
Default value: `'_build/test-reports'`

Specify where the XML reports should be saved to.

### Usage Examples

To trigger the XML reporting, simply call the `qunit_junit` task before you call the `qunit` task. A report will be created for all tests run by QUnit.

Typically, you'll use it as part of a list of commands like this:

```js
grunt.registerTask('test', ['connect:server', 'qunit_junit', 'qunit']);
```

## Example reports

The following report is an example of a test class that was composed of 3 tests, one of which had a failure. The `classname` attribute is built from the path and name of the test file, and the QUnit module names are added to the `name` attribute.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<testsuites>
  <testsuite name="example.package.TestClass" errors="1" failures="1" tests="3">
    <testcase classname="example.package.TestClass" name="My module: First test" assertions="1">
    </testcase>
    <testcase classname="example.package.TestClass" name="My module: Second test" assertions="2">
    </testcase>
    <testcase classname="example.package.TestClass" name="My module: Third test" assertions="2">
      <error type="failed" message="Died on test #1: Can't find variable: other">
  at http://localhost:8000/vendor/qunit-1.10.0.js:343
    at http://localhost:8000/test/example/package/TestClass.test.js:29
    at http://localhost:8000/vendor/require-2.0.6.js:32
    at http://localhost:8000/vendor/require-2.0.6.js:21
    at http://localhost:8000/vendor/require-2.0.6.js:25
    at http://localhost:8000/vendor/require-2.0.6.js:7
    at http://localhost:8000/vendor/require-2.0.6.js:26
    at o (http://localhost:8000/vendor/require-2.0.6.js:7)
    at http://localhost:8000/vendor/require-2.0.6.js:26
    at http://localhost:8000/vendor/require-2.0.6.js:22
    at http://localhost:8000/vendor/require-2.0.6.js:25
    at http://localhost:8000/vendor/require-2.0.6.js:7
    at http://localhost:8000/vendor/require-2.0.6.js:26
    at o (http://localhost:8000/vendor/require-2.0.6.js:7)
    at http://localhost:8000/vendor/require-2.0.6.js:26
    at http://localhost:8000/vendor/require-2.0.6.js:22
    at http://localhost:8000/vendor/require-2.0.6.js:26
    at http://localhost:8000/vendor/require-2.0.6.js:19
    at W (http://localhost:8000/vendor/require-2.0.6.js:17)
    at http://localhost:8000/vendor/require-2.0.6.js:30
    at http://localhost:8000/vendor/require-2.0.6.js:3
      </error>
      <failure type="failed" message="Expected 2 assertions, but 1 were run">
      </failure>
    </testcase>
  </testsuite>
</testsuites>
```

Additionally, if a test run fails completely a report of the following form will be generated:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<testsuites>
  <testsuite name="example.AnotherClass" errors="1" failures="0" tests="1">
    <testcase classname="example.AnotherClass" name="main" assertions="1">
      <error type="timeout" message="Test timed out, possibly due to a missing QUnit.start() call."></error>
    </testcase>
  </testsuite>
</testsuites>
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [grunt][].

## Release History
_(Nothing yet)_
