# css-import-loader

auxiliary loader to support using CSS `@import` rules with [pug-plugin](https://www.npmjs.com/package/pug-plugin)

## rationale

Using `@import` at runtime generates unnecessary requests. Thus, the feature is unsupported by [pug-plugin](https://www.npmjs.com/package/pug-plugin) (see [discussion](https://github.com/webdiscus/pug-plugin/discussions/51)). On the other hand, `@import` is a simple, plain CSS way of modularizing your stylesheets. This loader scans CSS files for `@import` statements requesting local files and resolves them by concatenating the files together. This allows working with separate files development, while only emitting a single file during build. This obviously is a crude way of solving this issue, but should work for simple use cases.

## usage

Installation:

```
npm install css-import-loader --save-dev
```

Configuration:

```js
{
    test: /\.css$/,
    use: [
        // css-loader handling imports in not supported by pug-plugin
        { loader: 'css-loader', options: { import: false } },
        // instead, use this loader to concatenate the CSS files
        { loader: 'css-import-loader' },
    ]
},
```

## options

Set `verbose` to `true` to get logs on which CSS files are collected:

```
Checking [dir]\source\css\style.css for @import...
[dir]\source\css\style.css imports [dir]\source\css\divider.css
[dir]\source\css\style.css imports [dir]\source\css\font.css
```
