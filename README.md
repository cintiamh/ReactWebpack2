# React Webpack

http://spencerdixon.com/blog/test-driven-react-tutorial.html

## Setting up Webpack

* [Webpack Cookbook](https://christianalfoni.github.io/react-webpack-cookbook/Getting-started.html)
* [Webpack Beginner Blog Post](http://blog.madewithlove.be/post/webpack-your-bags/)
* [Pete Hunts Infamous Webpack how-to](https://github.com/petehunt/webpack-howto)

```
$ npm init
$ npm i babel-loader babel-core webpack --save-dev
```

If npm installed webpack v2.0.0 or up, run this too:

```
$ npm install webpack@^1.12.11 --save-dev
```

Next set up the project's directory and create a `webpack.config.js` file:

```
$ mkdir src
$ touch src/main.js
$ mkdir test
$ mkdir dist
$ touch webpack.config.js
```

Installing presets:

```
$ npm i babel-preset-react babel-preset-es2015 --save-dev
$ touch .babelrc
```

`.babelrc` content:

```
{
  "presets": ["react", "es2015"]
}
```

Install React and create a new component:

```
$ npm i react react-dom -S
```

Create ./dist/index.htm file

Include webpack script on package.json.

```
"scripts": {
  "build": "webpack"
}
```

```
$ npm i webpack-dev-server --save-dev
```

Add webpack dev server entry points to our `webpack.config.js`:

```
entry: [
  'webpack/hot/dev-server',
  'webpack-dev-server/client?http://localhost:3000',
  './src/main.js'
],
```

In package.json include the script for running dev.

```
scripts: {
  "dev": "webpack-dev-server --port 3000 --devtool eval --progress --colors --hot --content-base dist",
  "build": "webpack"
}
```

In `webpack.config.js` include:

```
  resolve: {
    root: [
      // allows us to import modules as if /src was the root.
      // so I can do: import Comment from 'components/Comment'
      // instead of:  import Comment from '../components/Comment' or whatever relative path would be
      path.resolve(__dirname, './src')
    ],
    // allows you to require without the .js at end of filenames
    // import Component from 'component' vs. import Component from 'component.js'
    extensions: ['', '.js', '.json', '.jsx']
  },
  module: {
    loaders: [
      {
        test: /\.js?$/,
        // dont run node_modules or bower_components through babel loader
        exclude: /(node_modules|bower_components)/,
        // babel is alias for babel-loader
        // npm i babel-core babel-loader --save-dev
        loader: 'babel'
      }
    ],
  }
```

Running development mode: preview is available at http://localhost:3000

```
$ npm run dev
```

## Setting up Mocha, Chai, Sinon, and Enzyme

```
$ npm i mocha chai sinon --save-dev
$ npm i babel-register --save-dev
```

Include testing scripts to `package.json`:

```
"test": "mocha --compilers js:babel-register --recursive",
"test:watch": "npm test -- --watch",
```

Create tests:

`/test/test_helper.js`

```js
import { expect } from 'chai';
import sinon from 'sinon';

global.expect = expect;
global.sinon = sinon;
```

In package.json use the helper so you don't need to import chai and sinon in all files anymore.

```
"test": "mocha --compilers js:babel-register --require ./test/test_helper.js --recursive",
```

### Enzyme

Enzyme helps to test React components.

Install Enzyme in v.1.2.0 in order to work with this tutorial.

```
$ npm i enzyme@^1.2.0 react-addons-test-utils --save-dev
```

Create `/test/container/Root.spec.js`

Testing more than Shallow DOM elements.

Create `/src/components/CommentList.js`.

## Setting up Karma

```
$ npm i karma karma-chai karma-mocha karma-webpack --save-dev
$ npm i phantomjs-prebuilt@^1.9 --save-dev
$ npm i karma-sourcemap-loader karma-phantomjs-launcher --save-dev
$ npm i karma-spec-reporter --save-dev
$ npm i phantomjs --save-dev

# The polyfills arn't required but will help with browser support issues
# and are easy enough to include in our karma config that I figured why not
$ npm i babel-polyfill phantomjs-polyfill --save-dev
# yargs let you use command line arguments.
$ npm i yargs -S
```

In `package.json` replace the test scripts to use karma:

```
"test": "node_modules/.bin/karma start karma.config.js",
"test:dev": "npm run test -- --watch",
"old_test": "mocha --compilers js:babel-register --require ./test/test_helper.js --recursive",
"old_test:watch": "npm test -- --watch",
```

With the addition of webpack preprocessing in our test suite we can now remove those annoying relative path declarations inside our tests:

```js
// test/containers/Root.spec.js
import React from 'react';
import { shallow } from 'enzyme';
import Root from 'containers/Root';               // new import statement
// import Root from '../../src/containers/Root';  // old import statement

// test/components/CommentList.spec.js
import React from 'react';
import CommentList from 'components/CommentList';               // new import statement
// import CommentList from '../../src/components/CommentList';  // old import statement

import {
  describeWithDOM,
  mount,
  shallow,
  spyLifecycle
} from 'enzyme';
```
