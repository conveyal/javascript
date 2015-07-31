# JavaScript

Tools & best practices for writing JavaScript across Conveyal projects.

## [Using Standard Style](http://standardjs.com)

Standard can lint and format your code. No need for custom configuration files.

```bash
$ npm install -g standard
```

All checked in code should pass the latest `standard` linting.

```bash
$ standard
$ standard --format
```

See the styling rules [here](http://standardjs.com/rules.html#javascript-standard-style).

## [Atom.io](https://atom.io)

If you don't already have a preferred text editor, [install Atom](https://github.com/atom/atom/blob/master/README.md#installing). It's free, in active development, has thousands of plug-ins, and is easily hackable.

Install the [standard style linter](https://atom.io/packages/linter-js-standard) to see errors and lint on saves.

## [Node.js](http://nodejs.org)

Completely necessary for modern JavaScript development. May need to install `npm` separately depending on your OS. On Ubuntu, install the `nodejs-legacy` and `npm` packages. Installation instructions for other platforms are [here](https://github.com/joyent/node/wiki/installing-node.js-via-package-manager).

### [N](https://github.com/visionmedia/n)

Use `n` to manage Node.js versions. Use the latest `0.12.x` version.

```bash
$ npm install -g n
$ n stable
```

## [Component](https://github.com/componentjs/guide)

Dependency managment & build system. For all projects use `1.x`. Read the [guide](https://github.com/componentjs/guide) to get familiar with the toolset.

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

`paths` define folders, `client` in this case, in which to look for components. `local` defines components to be accessible from the root level. To use in an application `entry-component` will need to be required in your `index.html`. If you use the included build script, it will be required automatically.

```html
  <srcipt src="build/build.js"></script>
  <script>require('entry-component');</script>
</body>
```

Components within your application can access each other by defining their own `local` fields in their `component.json`.

### Taxonomy

If you're using a client-side MVC framework, each view, model, etc. should generally be in its own component (except for tiny things, for example trivial item views for collections or models that are used to marshal data within a component). They should be named `whatever-view`, `whatever-model`, `whatever-collection`, `whatever-collection-view`, `whatever-item-view` (for views that are intended for use in collections exclusively, for instance table rows or list items. The view should be the only thing in module.exports. (i.e. `model.exports = Backbone.Model.extend . . .`).
