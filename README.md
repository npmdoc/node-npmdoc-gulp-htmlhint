# api documentation for  [gulp-htmlhint (v0.3.1)](https://github.com/bezoerb/gulp-htmlhint)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-htmlhint.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-htmlhint) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-htmlhint.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-htmlhint)
#### A plugin for Gulp

[![NPM](https://nodei.co/npm/gulp-htmlhint.png?downloads=true)](https://www.npmjs.com/package/gulp-htmlhint)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-htmlhint/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gulp-htmlhint_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-htmlhint/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-htmlhint/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-htmlhint/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Ben Zörb",
        "url": "https://github.com/bezoerb"
    },
    "bugs": {
        "url": "https://github.com/bezoerb/gulp-htmlhint/issues"
    },
    "dependencies": {
        "gulp-util": "^3.0.0",
        "htmlhint": "^0.9.5",
        "strip-json-comments": "^2.0.0",
        "through2": "^2.0.0"
    },
    "description": "A plugin for Gulp",
    "devDependencies": {
        "htmlhint-stylish": "^1.0.0",
        "jshint": "^2.6.3",
        "mocha": "^2.2.1",
        "should": "^8.1.1",
        "vinyl-fs": "^2.3.1",
        "xo": "^0.12.1"
    },
    "directories": {
        "test": "test"
    },
    "dist": {
        "shasum": "68604533da2b3f8c5972b43b516606255218dd1e",
        "tarball": "https://registry.npmjs.org/gulp-htmlhint/-/gulp-htmlhint-0.3.1.tgz"
    },
    "engines": {
        "node": ">=0.8.0",
        "npm": ">=1.2.10"
    },
    "gitHead": "6f321b315c7d66ac44a02bb308423f7e9d5430fe",
    "homepage": "https://github.com/bezoerb/gulp-htmlhint",
    "keywords": [
        "gulpplugin"
    ],
    "license": "MIT",
    "licenses": [
        {
            "type": "MIT"
        }
    ],
    "main": "./index.js",
    "maintainers": [
        {
            "name": "bezoerb",
            "email": "ben@sommerlaune.com"
        }
    ],
    "name": "gulp-htmlhint",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/bezoerb/gulp-htmlhint.git"
    },
    "scripts": {
        "test": "xo && mocha test/*.js"
    },
    "version": "0.3.1",
    "xo": {
        "space": 4
    }
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-htmlhint](#apidoc.module.gulp-htmlhint)
1.  [function <span class="apidocSignatureSpan">gulp-htmlhint.</span>addRule (rule)](#apidoc.element.gulp-htmlhint.addRule)
1.  [function <span class="apidocSignatureSpan">gulp-htmlhint.</span>failReporter (opts)](#apidoc.element.gulp-htmlhint.failReporter)
1.  [function <span class="apidocSignatureSpan">gulp-htmlhint.</span>reporter (customReporter)](#apidoc.element.gulp-htmlhint.reporter)



# <a name="apidoc.module.gulp-htmlhint"></a>[module gulp-htmlhint](#apidoc.module.gulp-htmlhint)

#### <a name="apidoc.element.gulp-htmlhint.addRule"></a>[function <span class="apidocSignatureSpan">gulp-htmlhint.</span>addRule (rule)](#apidoc.element.gulp-htmlhint.addRule)
- description and source-code
```javascript
addRule = function (rule) {
    'use strict';
    return HTMLHint.addRule(rule);
}
```
- example usage
```shell
...
    gutil.log(data.message);
    gutil.log(data.evidence);
});
};

htmlhintPlugin.addRule = function (rule) {
'use strict';
return HTMLHint.addRule(rule);
};

htmlhintPlugin.reporter = function (customReporter) {
'use strict';
var reporter = defaultReporter;

if (typeof customReporter === 'function') {
...
```

#### <a name="apidoc.element.gulp-htmlhint.failReporter"></a>[function <span class="apidocSignatureSpan">gulp-htmlhint.</span>failReporter (opts)](#apidoc.element.gulp-htmlhint.failReporter)
- description and source-code
```javascript
failReporter = function (opts) {
    'use strict';
    opts = opts || {};
    return through2.obj(function (file, enc, cb) {
        // something to report and has errors
        var error;
        if (file.htmlhint && !file.htmlhint.success) {
            if (opts.suppress === true) {
                error = new PluginError('gulp-htmlhint', {
                    message: 'HTMLHint failed.',
                    showStack: false
                });
            } else {
                var errorCount = file.htmlhint.errorCount;
                var plural = errorCount === 1 ? '' : 's';
                var msg = c.cyan(errorCount) + ' error' + plural + ' found in ' + c.magenta(file.path);
                var messages = [msg].concat(getMessagesForFile(file).map(function (m) {
                    return m.message;
                }));

                error = new PluginError('gulp-htmlhint', {
                    message: messages.join(os.EOL),
                    showStack: false
                });
            }
        }
        cb(error, file);
    });
}
```
- example usage
```shell
...
It also prints a summary of all errors in the first bad file.

'''javascript
var htmlhint = require("gulp-htmlhint");

gulp.src("./src/*.html")
	.pipe(htmlhint())
	.pipe(htmlhint.failReporter())
'''

Optionally, you can pass the 'htmlhint.failReporter' a config object

__Plugin options:__

- *suppress*
...
```

#### <a name="apidoc.element.gulp-htmlhint.reporter"></a>[function <span class="apidocSignatureSpan">gulp-htmlhint.</span>reporter (customReporter)](#apidoc.element.gulp-htmlhint.reporter)
- description and source-code
```javascript
reporter = function (customReporter) {
    'use strict';
    var reporter = defaultReporter;

    if (typeof customReporter === 'function') {
        reporter = customReporter;
    }

    if (typeof customReporter === 'string') {
        if (customReporter === 'fail') {
            return htmlhintPlugin.failReporter();
        }

        reporter = require(customReporter);
    }

    if (typeof reporter === 'undefined') {
        throw new Error('Invalid reporter');
    }

    return through2.obj(function (file, enc, cb) {
        // Only report if HTMLHint ran and errors were found
        if (file.htmlhint && !file.htmlhint.success) {
            reporter(file);
        }

        cb(null, file);
    });
}
```
- example usage
```shell
...

### Default reporter
'''javascript
var htmlhint = require("gulp-htmlhint");

gulp.src("./src/*.html")
	.pipe(htmlhint())
	.pipe(htmlhint.reporter())
'''


### Fail reporter

Use this reporter if you want your task to fail in case of a HTMLHint Error.
It also prints a summary of all errors in the first bad file.
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
