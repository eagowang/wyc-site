---
title: 'webpack4打包vendor chunk'
date: 2019-03-25T11:28:00+08:00
draft: false
keywords: ['webpack', 'splitChunks', 'vendor']
description: 'create vendor chunk'
tags: ['splitChunks']
categories: ['前端']
author: 'eago'
comment: true
---

根据爆栈网回答整理：[webpack-4-create-vendor-chunk](https://stackoverflow.com/questions/48985780/webpack-4-create-vendor-chunk)

在 webpack3 配置中，我们像下面这样创建一个分离的 vendor.js chunk

```
entry: {
    client: ['./client.js'],
    vendor: ['babel-polyfill', 'react', 'react-dom', 'redux']
},
output: {
    filename: '[name].[chunkhash].bundle.js',
    path: '../dist',
    chunkFilename: '[name].[chunkhash].bundle.js',
    publicPath: '/'
},
plugins: [
    new webpack.HashedModuleIdPlugin(),
    new webpack.optimize.CommonsChunkPlugin({
        name: 'vendor'
    }),
    new webpack.optimize.CommonsChunkPlugin({
        name: 'runtime'
    })
]
```

但在 webpack4 中，commonChunksPlugin 被废弃了，使用如下配置也可以达到同样的效果

```
entry: {
 vendor: ['react', 'react-dom', 'react-router'],
 app: paths.appIndexJs
},
optimization: {
 splitChunks: {
  cacheGroups: {
    // match the entry point and spit out the file named here
    vendor: {
      chunks: 'initial',
      name: 'vendor',
      test: 'vendor',
      filename: 'vendor.js',
      enforce: true,
    },
  },
 },
},
```
