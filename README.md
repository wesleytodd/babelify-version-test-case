# Babel Version Test Case

This repo explores the issues around importing modules that use different versions of Babel.  Namely there is a bug that results in a message like his:

```
ReferenceError: [BABEL] /path/to/file.js: Unknown option: /path/to/package.json.presets while parsing file: /path/to/node_modules/module1/index.js
```

The apps in this repo both use `babelify@7.2.0` which uses `babel-core@6.0.14`.  The modules both use `babelify@6.1.2` which uses `babel-core@5.0.0`.  App1 imports module1, and app2 imports module2.  App1 does not exibit the error because module1 specifies babelify as a dev dependency and thus doesnt load a new version, while app2 will not build because it loads both versions of babelify.

Running the apps:

```
$ cd app1
$ npm install
$ npm start
```

# NPM Linking

Also to note, this uses file based installs, so you can also get app1 to throw the error by linking the module into it.  I used [linklocal](https://github.com/timoxley/linklocal) for this because it is a nice way to manage local dependencies.  So if you want to try it just install linklocal and run it it app1, then run `npm start`.  You can also do a global link if you want to test, which also exibits the error.

