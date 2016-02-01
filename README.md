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
