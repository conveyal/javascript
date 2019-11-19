# JavaScript

Tools & best practices for writing JavaScript across Conveyal projects.

## [Node.js](http://nodejs.org)

Completely necessary for modern JavaScript development. Install with a [package manager.](https://nodejs.org/en/download/package-manager/) **YOU MUST** use a `6.x.x` version for Conveyal development.

```bash
$ brew install node@10
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
