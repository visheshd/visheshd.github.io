---
layout: post
title: CRA fails on CircleCI because of Terser
type: post
published: true
excerpt: "Overriding webback config using customize-cra"
comments: true
tags: ["customize-cra", "terser", "cra", "minify"]
---

So I tried upgrading CRA for an existing app. I wanted to use the latest [React Fast Refresh](https://github.com/facebook/react/issues/16604) to hot reload react while making changes. Everything worked fine locally on the dev machine but the build failed on CircleCI while minifying.

It turned out to be a resourcing issue and Terser config had to be overridden without ejecting CRA of course.

Publishing the config I used borrowed from [here](https://github.com/webpack-contrib/terser-webpack-plugin/issues/202#issuecomment-580443244).


```javascript

const { override } = require('customize-cra');
const { addReactRefresh } = require('customize-cra-react-refresh');
const TerserPlugin = require('terser-webpack-plugin');

const overrideTerser = options => config => {

  config.optimization = {
    minimize: true,
    minimizer: [
      new TerserPlugin({
        terserOptions: {
          parse: {
            ecma: 8,
          },
          compress: {
            ecma: 5,
            warnings: false,
            comparisons: false,
            inline: 2,
            drop_console: true,
          },
          mangle: {
            safari10: true,
          },
          output: {
            ecma: 5,
            comments: false,
            ascii_only: true,
          },
        },
        parallel: 2,
        cache: true,
        sourceMap: true,
        extractComments: true,
      }),
    ],
  };
  return config;
};

/* config-overrides.js */
module.exports = override(addReactRefresh({ disableRefreshCheck: true }), overrideTerser());

```