# augmented-error

Re-throw an error and preserve the original stack trace.

## Install

```
$ npm install aggregate-error
```


## Usage

```js
const AugmentedError = require('augmented-error');
const fs = require('fs');

try {
  config = fs.readFileSync('/home/mark/app/config.yaml', 'utf8');
} catch (e) {
  throw new AugmentedError("Could not read config file - ensure this file exists!", e);
}
/*
AugmentedError:
    Error: Could not read config file - ensure this file exists!
        at Array.map (<anonymous>)
        at Object.<anonymous> (/Users/markl/mess/dsfs/test3.js:9:9)
        at Module._compile (node:internal/modules/cjs/loader:1108:14)
        at Object.Module._extensions..js (node:internal/modules/cjs/loader:1137:10)
        at Module.load (node:internal/modules/cjs/loader:973:32)
        at Function.Module._load (node:internal/modules/cjs/loader:813:14)
        at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:76:12)
        at node:internal/main/run_main_module:17:47
    Error: ENOENT: no such file or directory, open '/home/mark/app/config.yaml'
        at Object.openSync (node:fs:495:3)
        at readFileSync (node:fs:396:35)
        at Object.<anonymous> (/Users/markl/mess/dsfs/test3.js:7:12)
        at Module._compile (node:internal/modules/cjs/loader:1108:14)
        at Object.Module._extensions..js (node:internal/modules/cjs/loader:1137:10)
        at Module.load (node:internal/modules/cjs/loader:973:32)
        at Function.Module._load (node:internal/modules/cjs/loader:813:14)
        at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:76:12)
        at node:internal/main/run_main_module:17:47
    at Object.<anonymous> (/Users/markl/mess/dsfs/test3.js:9:9)
    at Module._compile (node:internal/modules/cjs/loader:1108:14)
    at Object.Module._extensions..js (node:internal/modules/cjs/loader:1137:10)
    at Module.load (node:internal/modules/cjs/loader:973:32)
    at Function.Module._load (node:internal/modules/cjs/loader:813:14)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:76:12)
    at node:internal/main/run_main_module:17:47
*/
```


## API

### AggregateError(errors)

Returns an `Error` that is also an [`Iterable`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators#Iterables) for the individual errors.

#### errors

Type: `Array<Error|Object|string>`

If a string, a new `Error` is created with the string as the error message.<br>
If a non-Error object, a new `Error` is created with all properties from the object copied over.
