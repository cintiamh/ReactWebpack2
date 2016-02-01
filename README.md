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
