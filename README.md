# react-template

## Basic Javascript Set Up

initialize the npm project on the command line which will create a `package.json` file. Libraries (node modules) you install will appear here:

```
npm init -y
```

By giving it the `-y` shorthand flag, you are telling npm that it should take all the defaults. 

Now create a directory for projects source code with some test JS:

>  /src/index.js
```
console.log('Hello Project.');
```

Into the scripts attribute of the package.json add the the following key value pair:
```
"start": "node src/index.js"
```

Now running `npm start` form the command line will run `node src/index.js` which runs the code in the source file.

[Wieruch Guide](https://www.robinwieruch.de/javascript-project-setup-tutorial/)


## Javascript with Webpack

Webpack is a JavaScript bundler for your web application. A `dist` folder will be used to serve your application from.

Add in the basic HTML template to your index.html:

>  /dist/index.html
```
<!DOCTYPE html>
<html>
  <head>
    <title>Hello Webpack</title>
  </head>
  <body>
    <div>
      <h1>Hello Webpack</h1>
    </div>
  </body>
</html>
```

`index.js` needs to be linked to `index.html`. This would normally be done via a link in the html file but with many JS files this could become messy, very quickly. 

So Webpack is used to generate one JavaScript bundle from all our source code in the src/ folder, which will be automatically put into your dist/ folder afterward. Then, it can be used in our entry point HTML file the following way:

```
<script src="./bundle.js"></script>
```

Webpack now needs to be installed:

```
npm install --save-dev webpack webpack-dev-server webpack-cli
```
*Note: Development dependencies (short: dev dependencies, indicated with --save-dev) are not bundled in your production code later on.*

In `package.json` change the start value to 
```
"start": "webpack-dev-server --mode development"
```

Running this command will now start the server and serve our `index.html` but there is no `bundle.js` to link it to as we haven't told webpack to do this yet. 

Change `package.json` to the following:

```
"start": "webpack-dev-server --config ./webpack.config.js --mode development"
```

The `webpack.config.js` now needs to be created in root folder with the following config:

>/webpack.config.js

```
module.exports = {

  entry: './src/index.js',

  output: {
    path: __dirname + '/dist',
    publicPath: '/',
    filename: 'bundle.js'
  },

  devServer: {
    contentBase: './dist'
  }
};
```
`entry` tells webpack where to compile from.<br>
`output` tell webpack where to compile to. At this point the bundle.js is served in memory.<br>
`devServer` tells webpack where we will be serving our app from.


## Webpack with Babel

Babel transpiles code into vanilla JS that any browser can read. Install it as follows:

```
npm install --save-dev @babel/core @babel/preset-env
```

To use Babel with Webpack the Webpack Loader needs to be installed:

```
npm install --save-dev babel-loader
```

Add the following file to your route `.babelrc`, and add the bbel config:

>/.babelrc
```
{
    "presets": ["@babel/preset-env"]
}
```

The add instruction in the `webpack.config.js` that tells webpack which files to use babel for:

```
  module: {
    rules: [
      {
        test: /\.(js)$/,
        exclude: /node_modules/,
        use: ['babel-loader']
      }
    ]
  },
  resolve: {
    extensions: ['*', '.js']
  }
  ```


## React wit Webpack and Babel

First up install Babel preset for React:

```
npm install --save-dev @babel/preset-react
```

Add second rpeset to `.babelrc`

>/.babelrc
```
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}
```

Update the `webpack.config.js` to tell it to look for `.jsx`;

>/webpack.config.js
```
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: ['babel-loader']
      }
    ]
  },
  resolve: {
    extensions: ['*', '.js', '.jsx']
  }
  ```

Now install `react` and `react-dom`:

```
npm install --save react react-dom
```

In `index.js` add:

>/src/index.js
```
import React from 'react';
import ReactDOM from 'react-dom';

const title = 'React with Webpack and Babel';

ReactDOM.render(
    <div>{title}</div>,
    document.getElementById('app')
);
```

Now install Hot Module Replacement which will monitor the source code for any changes and automatically render in the DOM:

```
npm install --save-dev react-hot-loader
```

Yoou have to obviously tell Webpack how to use it in `webpack.config.js`:

>/webpack.config.js
```
const webpack = require('webpack');

module.exports = {
.
.
.
  plugins: [
    new webpack.HotModuleReplacementPlugin()
  ],
  devServer : {
      .
      .
      .
      hot: true
  }
}
```

In your `index.js` let it know Hot Mod Rep is enabled:

>/src/index.js
```
.
.
.
module.hot.accept();
```






