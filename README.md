# api documentation for  [youtube-dl (v1.11.1)](https://github.com/fent/node-youtube-dl)  [![npm package](https://img.shields.io/npm/v/npmdoc-youtube-dl.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-youtube-dl) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-youtube-dl.svg)](https://travis-ci.org/npmdoc/node-npmdoc-youtube-dl)
#### youtube-dl driver for node

[![NPM](https://nodei.co/npm/youtube-dl.png?downloads=true)](https://www.npmjs.com/package/youtube-dl)

[![apidoc](https://npmdoc.github.io/node-npmdoc-youtube-dl/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-youtube-dl_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-youtube-dl/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-youtube-dl/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-youtube-dl/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Roly Fentanes",
        "url": "https://github.com/fent"
    },
    "bugs": {
        "url": "https://github.com/fent/node-youtube-dl/issues"
    },
    "contributors": [
        {
            "name": "Przemyslaw Pluta",
            "email": "przemyslawplutadev@gmail.com",
            "url": "http://przemyslawpluta.com"
        }
    ],
    "dependencies": {
        "mkdirp": "^0.5.1",
        "request": "^2.69.0",
        "streamify": "~0.2.3"
    },
    "description": "youtube-dl driver for node",
    "devDependencies": {
        "vows": "*"
    },
    "directories": {
        "lib": "./lib"
    },
    "dist": {
        "shasum": "c8e3b74951182dc5c58a0d1cd5be54b356271bd2",
        "tarball": "https://registry.npmjs.org/youtube-dl/-/youtube-dl-1.11.1.tgz"
    },
    "gitHead": "22abe259ffaf49849276ae008ba5786c68c4763c",
    "homepage": "https://github.com/fent/node-youtube-dl",
    "keywords": [
        "youtube",
        "video",
        "download"
    ],
    "license": "MIT",
    "main": "./lib/youtube-dl.js",
    "maintainers": [
        {
            "name": "fent",
            "email": "roly426@gmail.com"
        },
        {
            "name": "przemyslawpluta",
            "email": "przemyslawplutadev@gmail.com"
        }
    ],
    "name": "youtube-dl",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/fent/node-youtube-dl.git"
    },
    "scripts": {
        "postinstall": "node ./scripts/download.js",
        "test": "vows ./test/*.js --spec",
        "update": "node ./scripts/download.js"
    },
    "version": "1.11.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module youtube-dl](#apidoc.module.youtube-dl)
1.  [function <span class="apidocSignatureSpan">youtube-dl.</span>exec (url, args, options, callback)](#apidoc.element.youtube-dl.exec)
1.  [function <span class="apidocSignatureSpan">youtube-dl.</span>getExtractors (descriptions, options, callback)](#apidoc.element.youtube-dl.getExtractors)
1.  [function <span class="apidocSignatureSpan">youtube-dl.</span>getFormats (url, args, callback)](#apidoc.element.youtube-dl.getFormats)
1.  [function <span class="apidocSignatureSpan">youtube-dl.</span>getInfo (url, args, options, callback)](#apidoc.element.youtube-dl.getInfo)
1.  [function <span class="apidocSignatureSpan">youtube-dl.</span>getSubs (url, options, callback)](#apidoc.element.youtube-dl.getSubs)
1.  object <span class="apidocSignatureSpan">youtube-dl.</span>util

#### [module youtube-dl.util](#apidoc.module.youtube-dl.util)
1.  [function <span class="apidocSignatureSpan">youtube-dl.util.</span>formatDuration (seconds)](#apidoc.element.youtube-dl.util.formatDuration)
1.  [function <span class="apidocSignatureSpan">youtube-dl.util.</span>parseOpts (args)](#apidoc.element.youtube-dl.util.parseOpts)



# <a name="apidoc.module.youtube-dl"></a>[module youtube-dl](#apidoc.module.youtube-dl)

#### <a name="apidoc.element.youtube-dl.exec"></a>[function <span class="apidocSignatureSpan">youtube-dl.</span>exec (url, args, options, callback)](#apidoc.element.youtube-dl.exec)
- description and source-code
```javascript
function exec(url, args, options, callback) {
  'use strict';
  return call(url, [], args, options, callback);
}
```
- example usage
```shell
...
24video
3sat
'''

### Call the 'youtube-dl' binary directly
This module doesn't have 'youtube-dl' download the video. Instead, it uses the 'url' key from the '--dump-json' CLI option to create
 a node stream. That way, it can be used like any other node stream.

If that, or none of the above support your use case, you can use 'ytdl.exec()' to call 'youtube-dl' however you like.

''' js
ytdl.exec(url, ['-x', '--audio-format', 'mp3'], {}, function(err, output) {
  if (err) throw err;
  console.log(output.join('\n'));
});
'''
...
```

#### <a name="apidoc.element.youtube-dl.getExtractors"></a>[function <span class="apidocSignatureSpan">youtube-dl.</span>getExtractors (descriptions, options, callback)](#apidoc.element.youtube-dl.getExtractors)
- description and source-code
```javascript
function getExtractors(descriptions, options, callback) {
  'use strict';
  if (typeof options === 'function') {
    callback = options;
    options = {};
  } else if (typeof descriptions === 'function') {
    callback = descriptions;
    options = {};
    descriptions = false;
  }

  var args = descriptions ?
    ['--extractor-descriptions'] : ['--list-extractors'];
  call(null, args, null, options, callback);
}
```
- example usage
```shell
...

'''

### Getting the list of extractors

''' js
var youtubedl = require('youtube-dl');
youtubedl.getExtractors(true, function(err, list) {
  console.log('Found ' + list.length + ' extractors');
  for (var i = 0; i < list.length; i++) {
    console.log(list[i]);
  }
});
'''
...
```

#### <a name="apidoc.element.youtube-dl.getFormats"></a>[function <span class="apidocSignatureSpan">youtube-dl.</span>getFormats (url, args, callback)](#apidoc.element.youtube-dl.getFormats)
- description and source-code
```javascript
function getFormats(url, args, callback) {
  'use strict';
  console.warn(''getFormats()' is deprecated. Please use 'getInfo()'');

  if (typeof args === 'function') {
    callback = args;
    args = [];
  }

  ytdl.getInfo(url, args, {}, function done(err, video_info) {
    if (err) { return callback(err); }

    var formats_info = video_info.formats || [video_info];
    var formats = formats_info.map(function mapIt(format) {
        return {
          id: video_info.id,
          itag: format.format_id,
          filetype: format.ext,
          resolution: format.format.split(' - ')[1].split(' (')[0],
        };
    });

    callback(null, formats);
  });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.youtube-dl.getInfo"></a>[function <span class="apidocSignatureSpan">youtube-dl.</span>getInfo (url, args, options, callback)](#apidoc.element.youtube-dl.getInfo)
- description and source-code
```javascript
function getInfo(url, args, options, callback) {
  'use strict';
  if (typeof options === 'function') {
    callback = options;
    options = {};
  } else if (typeof args === 'function') {
    callback = args;
    options = {};
    args = [];
  }
  var defaultArgs = ['--dump-json'];
  if (!args || args.indexOf('-f') < 0 && args.indexOf('--format') < 0 &&
      args.every(function(a) {
        return a.indexOf('--format=') !== 0;
      })) {
    defaultArgs.push('-f');
    defaultArgs.push('best');
  }

  call(url, defaultArgs, args, options, function done(err, data) {
    if (err) { return callback(err); }
    var info;
    try {
      info = data.map(parseInfo);
    } catch (err) {
      return callback(err);
    }

    callback(null, info.length === 1 ? info[0] : info);
  });
}
```
- example usage
```shell
...
### Getting video information

''' js
var youtubedl = require('youtube-dl');
var url = 'http://www.youtube.com/watch?v=WKsjaOqDXgg';
// Optional arguments passed to youtube-dl.
var options = ['--username=user', '--password=hunter2'];
youtubedl.getInfo(url, options, function(err, info) {
if (err) throw err;

console.log('id:', info.id);
console.log('title:', info.title);
console.log('url:', info.url);
console.log('thumbnail:', info.thumbnail);
console.log('description:', info.description);
...
```

#### <a name="apidoc.element.youtube-dl.getSubs"></a>[function <span class="apidocSignatureSpan">youtube-dl.</span>getSubs (url, options, callback)](#apidoc.element.youtube-dl.getSubs)
- description and source-code
```javascript
function getSubs(url, options, callback) {
  'use strict';
  if (typeof options === 'function') {
    callback = options;
    options = {};
  }

  var args = ['--skip-download'];
  args.push('--write' + (options.auto ? '-auto' : '') + '-sub');
  if (options.all) {
    args.push('--all-subs');
  }
  if (options.lang) {
    args.push('--sub-lang=' + options.lang);
  }
  if (!options.warrning) {
    args.push('--no-warnings');
  }

  call(url, args, [], { cwd: options.cwd }, function(err, data) {
    if (err) { return callback(err); }

    var files = [];
    for (var i = 0, len = data.length; i < len; i++) {
      var line = data[i];
      if (line.indexOf('[info] Writing video subtitles to: ') === 0) {
        files.push(line.slice(35));
      }
    }
    callback(null, files);
  });
}
```
- example usage
```shell
...
  // Downloads all the available subtitles.
  all: false,
  // Languages of subtitles to download, separated by commas.
  lang: 'en',
  // The directory to save the downloaded files in.
  cwd: __dirname,
};
youtubedl.getSubs(url, options, function(err, files) {
  if (err) throw err;

  console.log('subtitle files downloaded:', files);
});
'''

For more usage info on youtube-dl and the arguments you can pass to it, do 'youtube-dl -h' or go to the [youtube-dl documentation
][].
...
```



# <a name="apidoc.module.youtube-dl.util"></a>[module youtube-dl.util](#apidoc.module.youtube-dl.util)

#### <a name="apidoc.element.youtube-dl.util.formatDuration"></a>[function <span class="apidocSignatureSpan">youtube-dl.util.</span>formatDuration (seconds)](#apidoc.element.youtube-dl.util.formatDuration)
- description and source-code
```javascript
formatDuration = function (seconds) {
  var parts = [];
  parts.push(seconds % 60);
  var minutes = Math.floor(seconds / 60);
  if (minutes > 0) {
    parts.push(minutes % 60);
    var hours = Math.floor(minutes / 60);
    if (hours > 0) {
        parts.push(hours);
    }
  }
  return parts.reverse().join(':');
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.youtube-dl.util.parseOpts"></a>[function <span class="apidocSignatureSpan">youtube-dl.util.</span>parseOpts (args)](#apidoc.element.youtube-dl.util.parseOpts)
- description and source-code
```javascript
parseOpts = function (args) {
  var pos;
  for (var i = 0, len = badArgs.length; i < len; i++) {
    if ((pos = args.indexOf(badArgs[i])) !== -1) {
      args.splice(pos, 1);
    }
  }
  return args;
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
