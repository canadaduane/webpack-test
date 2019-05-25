# Webpack Bug

## Recreate the problem

```
$ yarn install
$ yarn start
```

## Explanation

When generating code with `devtool: "inline"`, it's possible to get webpack to generate syntactically incorrect javascript in the following case:

```
import { SomeClass } from "somemodule";
const result = new SomeClass();
```

will generate the following syntax error:

```
const result = new !(function webpackMissingModule() { var e = new Error("Cannot find module 'somemodule'"); e.code = 'MODULE_NOT_FOUND'; throw e; }())();
```

(note the exclamation point after `new`).

## References

- https://github.com/webpack/webpack/issues/9187 (my report)
- https://github.com/webpack/webpack/issues/8762
- https://github.com/webpack/webpack/issues/6191

