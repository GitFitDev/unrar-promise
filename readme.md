# unrar-promise

* [honeo/unrar-promise](https://github.com/honeo/unrar-promise)  
* [unrar-promise](https://www.npmjs.com/package/unrar-promise)

## What's This

Easy .rar expansion module.

## How to use

```sh
$npm i unrar-promise
```

```js
const {unrar, list} = require('unrar-promise');

await unrar('archive.rar', './output');
```

## API

* About output destination
* Skip the file if it already exists.
* If the directory does not exist, create it.
* [node-sanitize-filename](https://github.com/parshap/node-sanitize-filename)Normalize with

### Options

| key       | type     | default | description                                                           |
|:--------- |:-------- | ------- | --------------------------------------------------------------------- |
| filter    | function |         | Executed with object as an argument for each output content、Skip if false。 |
| overwrite | boolean  | false   | Do you want to allow overwriting?                                                  |
| password  | string   |     ""    | Archive password.                                                    |

### unrar(inputFile, outputDir [, options])

Expand the .rar archive with 1 argument path to the directory with 2 arguments.  
Returns a promise that resolves to the path of the extraction directory as an argument.

```js
// hoge.rar => output/...
const dirPath = await unrar('hoge.rar', 'output');

// options
const dirPath = await unrar('hoge.rar', 'output', {
    filter({path, type}){
        return type==='File' && /\.txt$/.test(path); //  *.txt file only
    },
    overwrite: true,
    password: '123456'
});
```

### list(inputFile [, options])

Get the content list of .rar archive with 1 argument path as an array.
Returns a promise that resolves the obtained array as an argument.

```js
const arr = await list('hoge.rar'); // [..."path"]

// options
const arr = await list('foobar.rar', {
    password: 'qwerty'
});
```

## Breaking Changes

### v1 => v2

* .extract(), extractAll()
  * Abolished and integrated into .unrar ().
* .list()
  * Change argument 2 from string to object.
