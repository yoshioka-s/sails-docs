# Default tasks

### Overview

The asset pipeline bundled in Sails is a set of Grunt tasks configured with conventional defaults designed to make your project more consistent and productive. The entire frontend asset workflow is completely customizable, while it provides some default tasks out of the box. Sails makes it easy to [configure new tasks](http://sailsjs.com/documentation/concepts/Assets/TaskAutomation.html?q=task-configuration) to fit your needs.
<!-- change link to: /documentation/concepts/assets/task-automation#?task-configuration once new site is live -->

Here are a few things that the default Grunt configuration in Sails does to help you out:
- Automatic LESS compilation
- Automatic JST compilation
- Automatic Coffeescript compilation
- Optional automatic asset injection, minification, and concatenation
- Creation of a web ready public directory
- File watching and syncing
- Optimization of assets in production

### Default Grunt tasks

Below is a list of the Grunt tasks that are included by default in new Sails projects:

##### clean

> This grunt task is configured to clean out the contents in the `.tmp/public/` of your sails project.

> [usage docs](https://github.com/gruntjs/grunt-contrib-clean)

##### coffee

> Compiles coffeeScript files from `assets/js/` into Javascript and places them into `.tmp/public/js/` directory.

> [usage docs](https://github.com/gruntjs/grunt-contrib-coffee)

##### concat

> Concatenates JavaScript and css files, and saves concatenated files in `.tmp/public/concat/` directory.

> [usage docs](https://github.com/gruntjs/grunt-contrib-concat)

##### copy

> **dev task config**
> Copies all directories and files, except coffeescript and less files, from the sails assets folder into the `.tmp/public/` directory.

> **build task config**
> Copies all directories and files from the .tmp/public directory into a www directory.

> [usage docs](https://github.com/gruntjs/grunt-contrib-copy)

##### cssmin

> Minifies css files and places them into `.tmp/public/min/` directory.

> [usage docs](https://github.com/gruntjs/grunt-contrib-cssmin)

##### jst

> Precompiles Underscore templates to a `.jst` file. (i.e. it takes HTML template files and turns them into tiny JavaScript functions). This can speed up template rendering on the client, and reduce bandwidth usage.

> [usage docs](https://github.com/gruntjs/grunt-contrib-jst)

##### less

> Compiles LESS files into CSS. Only the `assets/styles/importer.less` is compiled. This allows you to control the ordering yourself, i.e. import your dependencies, mixins, variables, resets, etc. before other stylesheets.

> [usage docs](https://github.com/gruntjs/grunt-contrib-less)

##### sails-linker

> Automatically inject `<script>` tags for JavaScript files and `<link>` tags for css files.  Also automatically links an output file containing precompiled templates using a `<script>` tag. A much more detailed description of this task can be found [here](https://github.com/balderdashy/sails-generate-frontend/blob/master/docs/overview.md#a-litte-bit-more-about-sails-linking), but the big takeaway is that script and stylesheet injection is *only* done in files containing `<!--SCRIPTS--><!--SCRIPTS END-->` and/or `<!--STYLES--><!--STYLES END-->` tags.  These are included in the default **views/layout.ejs** file in a new Sails project.  If you don't want to use the linker for your project, you can simply remove those tags.

> [usage docs](https://github.com/Zolmeister/grunt-sails-linker)

##### sync

> A grunt task to keep directories in sync. It is very similar to grunt-contrib-copy but tries to copy only those files that have actually changed. It specifically synchronizes files from the `assets/` folder to `.tmp/public/`, overwriting anything that's already there.

> [usage docs](https://github.com/tomusdrw/grunt-sync)

##### uglify

> Minifies client-side JavaScript assets.  Note that by default, this task will "mangle" all of your function and variable names (either by changing them to a much shorter name, or stripping them entirely).  This is usually desirable as it makes your code significantly smaller, but in some cases can lead to unexpected results (particularly when you expect an object's constructor to have a certain name).  To turn off or modify this behavior, [use the `mangle` option](https://github.com/gruntjs/grunt-contrib-uglify#no-mangling) when setting up this task.

> [usage docs](https://github.com/gruntjs/grunt-contrib-uglify)

##### watch

> Runs predefined tasks whenever watched file patterns are added, changed or deleted. Watches for changes on files in the `assets/` folder, and re-runs the appropriate tasks (e.g. less and jst compilation).  This allows you to see changes to your assets reflected in your app without having to restart the Sails server.

> [usage docs](https://github.com/gruntjs/grunt-contrib-watch)


<docmeta name="displayName" value="Default tasks">
