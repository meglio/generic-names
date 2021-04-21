generic-names
=============

Helper for building generic names, similar to webpack. Designed to be used with [postcss&#x2011;modules&#x2011;scope](https://github.com/css-modules/postcss-modules-scope).

Uses [interpolateName](https://github.com/webpack/loader-utils#interpolatename) from the webpack/loader-utils.

## API

```javascript
var genericNames = require('generic-names');
var generate = genericNames('[name]__[local]___[hash:base64:5]', {
  context: process.cwd()
});

generate('foo', '/case/source.css'); // 'source__foo___3mRq8'
```

## Compatibility

### With Webpack's `css-loader` and `babel-plugin-react-css-modules`

Starting from version `3.0`, this plugin is not compatible with `babel-plugin-react-css-modules` running under `css-modules<3.6.0` due to [this update](https://github.com/webpack-contrib/css-loader/commit/d2f6bd2755a513e98faca84c3f52544be72d53f3).

Explanation: starting from `3.6.0`, css-modules uses `\x00` instead of `+` when generating `content.options` consumed by Webpack when generating `[hash]` and `[contenthash]`, as can be seen in [this update](https://github.com/webpack-contrib/css-loader/commit/d2f6bd2755a513e98faca84c3f52544be72d53f3#diff-3274f1a37032fb0ae4e2823def0007c634e869ae0dfc304ff6a12c36513c3a52R49). As a result, the hash value generated by the react css modules plugin is not the same as the one generated by Webpack's css-loader.
