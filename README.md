# grunt-contrib-jade [![Build Status](https://secure.travis-ci.org/gruntjs/grunt-contrib-jade.png?branch=master)](http://travis-ci.org/gruntjs/grunt-contrib-jade)

> Compile Jade files to HTML.

### Overview

Inside your `grunt.js` file add a section named `jade`. This section specifies files to compile and the options passed to [jade](https://github.com/visionmedia/jade#public-api).

#### Parameters

##### files ```object```

This defines what files this task will process and should contain key:value pairs.

The key (destination) should be an unique filepath (supports [grunt.template](https://github.com/gruntjs/grunt/blob/master/docs/api_template.md)) and the value (source) should be a filepath or an array of filepaths (supports [minimatch](https://github.com/isaacs/minimatch)).

Note: When the value contains an array of multiple filepaths, the contents are concatenated in the order passed.

##### options ```object```

This controls how this task (and its helpers) operate and should contain key:value pairs, see options below.

#### Options

##### data ```object```

Sets the data passed to ```jade``` during template compilation. Any data can be passed to the template (including ```grunt``` templates).

##### pretty ```boolean```

Configure ```jade``` to output pretty HTML.

##### client ```boolean```

Setting ```client``` to true will allow jade templates to be compiled as JavaScript templates instead of HTML.

##### templatePath ```string```

If client is set to true, templatePath will act as the template path for compilation of JavaScript templates. Defaults to templates.

##### templatesArray ```string```

If client is set to true, templatesArray will ast as the window object in which to store the jade templates. Defaults to JadeTemplates.

#### Config Examples

``` javascript
jade: {
  compile: {
    options: {
      data: {
        debug: false
      }
    },
    files: {
      "path/to/dest.html": ["path/to/templates/*.jade", "another/path/tmpl.jade"]
    }
  }
}
```

If you want to generate a JavaScript template instead of HTML:
``` javascript
jade: {
  compile: {
    options: {
      templatePath : 'templates',
      templatesArray : 'JadeTemplates',
      client : true
    },
    files: {
      "path/to/dest.html": ["path/to/templates/*.jade", "another/path/tmpl.jade"]
    }
  }
}
```

If you want to generate a debug file and a release file from the same template:

``` javascript
jade: {
  debug: {
    options: {
      data: {
        debug: true
      }
    },
    files: {
      "debug.html": "test.jade"
    }
  },
  release: {
    options: {
      data: {
        debug: false
      }
    },
    files: {
      "release.html": "test.jade"
    }
  }
}
```

If you want to use `grunt` template in `options.data`:

``` javascript
jade: {
  debug: {
    options: {
      data: {
        debug: true,
        timestamp: "<%= new Date().getTime() %>"
      }
    },
    files: {
      "debug.html": "test.jade"
    }
  }
}
```

or you can use `grunt` helpers (grunt object was exposed at template context):

```js
jade: {
  debug: {
    options: {
      data: {
        debug: true,
        timestamp: "<%= grunt.template.today() %>"
      }
    },
    files: {
      "debug.html": "test.jade"
    }
  }
}
```

Use the `pretty` option to output indented HTML:

```js
jade: {
  debug: {
    options: {
      pretty: true
    },
    files: {
      "debug.html": "test.jade"
    }
  }
}
```

--

*Task submitted by [Eric Woroshow](https://github.com/errcw).*