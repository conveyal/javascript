# JavaScript

Tools & best practices for writing JavaScript across Conveyal projects.

## [Node.js](http://nodejs.org)

Completely necessary for modern JavaScript development. May need to install `npm` separately depending on your OS. On Ubuntu, install the `nodejs-legacy` and `npm` packages. Installation instructions for other platforms are [here](https://github.com/joyent/node/wiki/installing-node.js-via-package-manager).

### [N](https://github.com/visionmedia/n)

Use `n` to manage Node.js versions. For now use the latest `0.10.x` version. When `0.12.x` is released we will be switching to it.

```bash
$ npm install -g n
$ n stable
```

## [Component](https://github.com/componentjs/guide)

Dependency managment & build system. For all new projects use `1.x`, Modeify currently uses `0.19.x` but will be upgrading soon. Read the [guide](https://github.com/componentjs/guide) to get familiar with the toolset.

```bash
$ npm install -g component
```

### Open file limit error

On Mac's, a build may open thousands of files at once and hit the machine's max limit. See this [gist](https://gist.github.com/trevorgerhardt/40e944e63dee3ee1779f) to get around that error.

### Tips

* Don't recreate the wheel! Use other components as much as possible.
* Split out a component into it's own repo if it can be used across projects.
* Build with the `--dev` flag to get source maps to help with debugging.

### Project Setup

For smaller projects, use just one `component.json` file. For larger ones use an entry `component.json` file and individual components. (See [Modeify](https://github.com/conveyal/modeify) for an example)

The `component.json` would look like:

```json
{
  "paths": [
    "client"
  ],
  "local": [
    "entry-component"
  ]
}
```

`paths` define folders, `client` in this case, in which to look for components. `local` defines components to be accessible from the root level. To use in an application `entry-component` will need to be required in your `index.html`.

```html
  <srcipt src="build/build.js"></script>
  <script>require('entry-component');</script>
</body>
```

Components within your application can access each other by defining their own `local` fields in their `component.json`.

## [JSHint](https://jshint.com)

JSHint prevents a lot of headaches that appear in JavaScript development. Always **always** setup JSHint as part of your build process.

```bash
$ npm install -g jshint
```

Run it against your JavaScript on every file change.

```bash
$ jshint index.js
```

Symlink the `jshint.json` file in this repo to `~/.jshintrc` or to the base folder of your Conveyal projects so that we will not need to recreate one for each project.

Our current rules are:

```json
{
  "globals": {
    "before": false,
    "describe": false,
    "it": false,
    "$": false,
    "L": false
  },
  "boss": true,
  "browser": true,
  "indent": 2,
  "laxbreak": true,
  "maxcomplexity": 12,
  "node": true,
  "trailing": true,
  "undef": true
}
```

## [JSBeautify](https://github.com/beautify-web/js-beautify)

Consolidate styling rules.

```bash
$ npm install -g js-beautify
```

Run it on your `.js` files before checking in changes.

```bash
$ js-beautify index.js --replace
```

Symlink the `jsbeautify.json` file in this repo to `~/.jsbeautifyrc` or to the base folder of your Conveyal projects so that we will not need to recreate one for each project.

Our current rules are:

```json
{
  "end_with_newline": true,
  "indent_size": 2,
  "indent_char": " ",
  "indent_level": 0,
  "indent_with_tabs": false,
  "preserve_newlines": true,
  "max_preserve_newlines": 2,
  "jslint_happy": false,
  "brace_style": "collapse",
  "keep_array_indentation": false,
  "keep_function_indentation": false,
  "space_before_conditional": true,
  "break_chained_methods": false,
  "eval_code": false,
  "unescape_strings": false,
  "wrap_line_length": 120
}
```
