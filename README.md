# grunt-messageformat v0.0.1
> Generate compiled, localized string resources using MessageFormat

## Getting Started
This plugin requires Grunt `>=0.4.0`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-messageformat --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-messageformat');
```

This plugin will use [MessageFormat](https://github.com/SlexAxton/messageformat.js/) (https://github.com/SlexAxton/messageformat.js/) to process your locale files. Currently, locale files structured as JSON or as [Properties](http://en.wikipedia.org/wiki/.properties) files are suppored.

Each string is expected to follow the [ICU MessageFormat](http://userguide.icu-project.org/formatparse/messages#TOC-MessageFormat) syntax.

### Example JSON File

```json
{
  "test-msg-id": "This is my message",
  "results": "There {0, plural, one{ is one result } other{ are {0} results. }}."
}
```

Each string is referred to by it's ID, in this case `test-msg-id` is a very simple string. However `results` is a complex message with one numerical argument, and uses the ICU plural selector.

If this JSON file were named en.json, then it would be compiled as en.js, which will expose functions for each message id.

```javascript
var mfunc = require('en.js');
var oneResult = mfunc().results(1);
var manyResults = mfunc().results(48);
var noResults = mfunc().results(0);

// Output: "There is one result"
console.log(oneResult);

// Output: "There are 48 results"
console.log(manyResults);

// Output: "There are 0 results"
console.log(noResults);
```

You can use the prefix and suffix options to wrap your JS code in AMD-style defines, Node-friend module exports, licenses, or anything else you wish.

## msgfmt task
_Run this task with `grunt msgfmt` command._

Task targets, files and options may be specified according to the grunt [Configuring tasks](http://gruntjs.com/configuring-tasks) guide.

### options

#### prefix
Type: `string`
Default: ''

Prepend this string to the beginning of the compiled JS file

#### suffix
Type: `string`
Default: ''

Append this string to the beginning of the compiled JS file

#### format
Type: `string`
Default: ''

Specify the format of the resource file(s) being processed. Only `json` and `properties` are supported values.

If left blank, then the format will be inferred from the filename's extension.
