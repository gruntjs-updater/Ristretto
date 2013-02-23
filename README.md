# grunt-ristretto

> Autoreload with LESS and Latte.

## Getting Started
This plugin requires [Grunt](http://gruntjs.com/) `~0.4.0` and [Composer](http://getcomposer.org/) with PHP `>= 5.3.0`.

```shell
npm install grunt-ristretto --save-dev
```

One the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-ristretto');
```

## The "ristretto" task

### Overview
In your project's Gruntfile, add a section named `ristretto` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  ristretto: {
    options: {
      port: 2013,
      www_dir: 'www',
      latte_dir: 'www',
      model_dir: 'www/model'
    },
    publish: { // not available yet
      destination: 'dist'
    },
  },
})
```

### Your `Gruntfile.js` might look like this.

Dont forget to mention `grunt-contrib-less` and `grunt-contrib-watch` in your `npm package.json`.

```js
module.exports = function (grunt) {
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    less: {
      production: {
        options: {
          yuicompress: true
        },
        files: {
          "www/css/screen.css": "www/less/screen.less",
          "www/css/print.css": "www/less/print.less"
        }
      }
    },
    watch: {
      styles: {
        files: ['www/**/*.less'],
        tasks: ['less', 'ristretto:stylesheets']
      },
      scripts: {
        files: ['www/**/*', '!www/**/*.css', '!www/**/*.less'],
        tasks: ['ristretto:pages']
      }
    },
    ristretto: {
      options: {
        model_dir: 'www/model',
        latte_dir: 'www',
        www_dir: 'www',
        port: 2013
      },
      server: {
      },
      publish: {
      },
      stylesheets: {
      },
      pages: {
      }
    }
  });

  grunt.loadNpmTasks('grunt-contrib-less');
  grunt.loadNpmTasks('grunt-contrib-watch');
  grunt.loadNpmTasks('grunt-ristretto');

  grunt.registerTask('default', ['ristretto:server', 'less', 'ristretto:pages', 'watch']);
};
```