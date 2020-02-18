https://scotch.io/tutorials/setup-a-react-environment-using-webpack-and-babel

https://stackoverflow.com/questions/52067944/cannot-find-module-babel-core/52067984


* yarn init
* yarn add webpack webpack-dev-server path
* touch webpack.config.js


/webpack.config.js

    const path = require('path');
    module.exports = {
    entry: './client/index.js',
    output: {
        path: path.resolve('dist'),
        filename: 'index_bundle.js'
    },
    module: {
        rules: [
        { test: /\.css$/,
            use: [
            { loader: "style-loader" },
            { loader: "css-loader" }
            ]
        },
        {
            test: /\.js$/,
            exclude: /node_modules/,
            use: "babel-loader"
        }, {
            test: /\.jsx?$/,
            exclude: /node_modules/,
            use: "babel-loader"
        }
        ]
    }
    }

* yarn add --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader

/.babelrc


    {
    "presets": [
        "@babel/preset-env",
        "@babel/preset-react"
    ]
    }

* yarn add html-webpack-plugin

* yarn start