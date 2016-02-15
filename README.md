# JavaScript

Tools & best practices for writing JavaScript across Conveyal projects.

## [ES6](https://github.com/DrkSephy/es6-cheatsheet)

Certain conventions should be followed due to the new functionality that ES6 brings. Highlights:

* When working on a new codebase, use `let` for variables that will change their value over time, and `const` for variables which cannot be reassigned.
* Use Arrow Functions (`=>`) in place of function expressions when possible.
* Use `Promise`s instead of the `function asyncFunc (input, function callback (err, result) {}) {}` style.

## [Using Standard Style](http://standardjs.com)

Standard can lint and format your code. No need for custom configuration files.

```bash
$ npm install -g standard
```

Add the `babel-eslint` parser to your project's `devDependencies` and add the following to your `package.json`

```json
  "standard": {
    "parser": "babel-eslint"
  }
```


All checked in code should pass the latest `standard` linting.

```bash
$ standard
```

To format, run:

```bash
$ standard --format
```

See the styling rules [here](http://standardjs.com/rules.html#javascript-standard-style).

## [Atom.io](https://atom.io)

If you don't already have a preferred text editor, [install Atom](https://github.com/atom/atom/blob/master/README.md#installing). It's free, in active development, has thousands of plug-ins, and is easily hackable.

Install the [standard style linter](https://atom.io/packages/linter-js-standard) to see errors and lint on saves.

## [Node.js](http://nodejs.org)

Completely necessary for modern JavaScript development. May need to install `npm` separately depending on your OS. On Ubuntu, install the `nodejs-legacy` and `npm` packages. Installation instructions for other platforms are [here](https://github.com/joyent/node/wiki/installing-node.js-via-package-manager).

### [N](https://github.com/visionmedia/n)

Use `n` to manage Node.js versions. Use the latest `5.x.x` version.

```bash
$ npm install -g n
$ n latest
```

### Taxonomy

If you're using a client-side MVC framework, each view, model, etc. should generally be in its own component (except for tiny things, for example trivial item views for collections or models that are used to marshal data within a component). They should be named `whatever-view`, `whatever-model`, `whatever-collection`, `whatever-collection-view`, `whatever-item-view` (for views that are intended for use in collections exclusively, for instance table rows or list items. The view should be the only thing in module.exports. (i.e. `model.exports = Backbone.Model.extend . . .`).
