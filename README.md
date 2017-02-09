# JavaScript

Tools & best practices for writing JavaScript across Conveyal projects.

## [Node.js](http://nodejs.org)

Completely necessary for modern JavaScript development. Install with a [package manager.](https://nodejs.org/en/download/package-manager/) **YOU MUST** use a `6.x.x` version for Conveyal development.

```bash
$ brew install node@6
```

### [Yarn](https://yarnpkg.com/en/)

Use `yarn` as an `npm` replacement to manage dependencies.

```bash
$ brew install yarn
```

### [N](https://github.com/visionmedia/n)

Use `n` to manage Node.js versions.

```bash
$ yarn global add n
$ n latest
```

## [ES6](https://github.com/DrkSephy/es6-cheatsheet)

Certain conventions should be followed due to the new functionality that ES6 brings. Highlights:

* When working on a new codebase, use `let` for variables that will change their value over time, and `const` for variables which cannot be reassigned.
* Use Arrow Functions (`=>`) in place of function expressions when possible.
* Use `Promise`s instead of the `function asyncFunc (input, function callback (err, result) {}) {}` style.

## Other Tips

#### Use `Promises`, [`async`/`await`](http://tc39.github.io/ecmascript-asyncawait/) and [watch out for callback hell](http://callbackhell.com/)

Promiseified functions can be `awaited` allowing for this style of functions:

```js
async function chainAnimationsAsync(elem, animations) {
  let ret = null
  try {
    for(const anim of animations) {
      ret = await anim(elem)
    }
  } catch (e) {
    /* report and keep going */
  }
  return ret
}
```

#### Always use [`debug`](https://github.com/visionmedia/debug) instead of `console.log`

Debug is a tiny library that allows you to selectively turn on and off namespaced log statements in the browser and in node.

```js
import dbg from 'debug'
const debug = dbg('library:module')
debug('log this!')
```

The log will only be shown in the browser when you turn it on via simple regexp in the console:

```js
> localStorage.setItem('debug', 'library*')
```

#### Don't use `bind`

Do:

```jsx
onClick={(e) => this.handleEvent(e)}
```

Don't

```jsx
onClick={this.handleEvent.bind(this)}
```

In classes you can auto-bind to the instance by using class properties and arrow functions.

```js
class Foo {
  handleEvent = (e) => {
    // inside this function `this` will always be the instance of `Foo`
  }
}
```

#### Don't use `jQuery`

To start, see: [http://youmightnotneedjquery.com/](http://youmightnotneedjquery.com/). Use ES6 and smaller modern JavaScript libraries instead of using jQuery.

Use [`fetch`](https://github.com/github/fetch) instead of `$.ajax`/`$.get`/`$.post`:

```js
fetch(url)
  .then(res => res.json())
  .then(data => {
    console.log(data)
  })
```

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

### Taxonomy

If you're using a client-side MVC framework, each view, model, etc. should generally be in its own component (except for tiny things, for example trivial item views for collections or models that are used to marshal data within a component). They should be named `whatever-view`, `whatever-model`, `whatever-collection`, `whatever-collection-view`, `whatever-item-view` (for views that are intended for use in collections exclusively, for instance table rows or list items. The view should be the only thing in module.exports. (i.e. `model.exports = Backbone.Model.extend . . .`).
