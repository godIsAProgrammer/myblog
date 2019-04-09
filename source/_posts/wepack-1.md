---
layout: post
title: webpack2配置sass
author: CAO qisen
date: 2017-03-19 21:53:40
subtitle:
header-img:
cdn:
tags:
    - webpack2
    - sass
    - CSS
---
#### 首先安装所需要的sass-loader和node-sass
```shell
    npm install sass-loader node-sass webpack --save-dev
```
<!-- excerpt -->
#### 然后在webpack.config.js如此配置
```javascript
    module.exports = {
        module: {
            rules: [{
                test: /\.scss$/,
                use: [{
                    loader: "style-loader"
                }, {
                    loader: "css-loader"
                }, {
                    loader: "sass-loader",
                    options: {
                        includePaths: ["absolute/path/a", "absolute/path/b"]
                    }
                }]
            }]
        }
    };
```
#### 如果要配合extract-text-webpack-plugin可以这样配置
```shell
    npm install extract-text-webpack-plugin --save-dev
```
```javascript
const ExtractTextPlugin = require("extract-text-webpack-plugin");
 
const extractSass = new ExtractTextPlugin({
    filename: "[name].[contenthash].css",
    disable: process.env.NODE_ENV === "development"
});
 
module.exports = {
    module: {
        rules: [{
            test: /\.scss$/,
            loader: extractSass.extract({
                use: [{
                    loader: "css-loader"
                }, {
                    loader: "sass-loader"
                }],
                // use style-loader in development 
                fallback: "style-loader"
            })
        }]
    },
    plugins: [
        extractSass
    ]
};
```
