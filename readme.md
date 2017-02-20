# reshape-cli
> Simple CLI for [reshape][reshape-url]

[![node](https://img.shields.io/node/v/reshape-cli.svg?maxAge=2592000&style=flat-square)]()[![NPM version][npm-image]][npm-url][![Travis Build Status](https://img.shields.io/travis/GitScrum/reshape-cli.svg?style=flat-square&label=unix)](https://travis-ci.org/GitScrum/reshape-cli)[![AppVeyor Build Status][appveyor-img]][appveyor][![Coveralls Status][coveralls-image]][coveralls-url][![Dependency Status][depstat-image]][depstat-url][![Standard Code Style][style]][style-url]

## Install

```
npm install --global reshape-cli
```

## Usage

```bash
$ reshape --help

  Usage
  reshape [-o output-file/directory|-r] [-i input-file/directory] [--config|-c path/to/file/config] [--use|-u plugin]

  Options
  --config,  -c Path to JS file                    [string]
  --output,  -o Output html file/folder result     [required]
  --input,   -i Input html file/folder             [required]
  --use,     -u reshape plugin name                [string]
  --replace, -r Replace input file(s)              [boolean]
  --help,    -h Show help                          [boolean]
  --version, -v Show version number                [boolean]
```

## Config
*Automatically loads plug-ins with configuration from package.json using [post-load-plugins](https://github.com/post-org/post-load-plugins)*

package.json
```json
{
  "name": "my project",
  "dependencies": {
    "reshape-include": "^1.0.2"
  },
  "reshape": {
    "include": {
      "root": "./"
    }
  }
}
```

## Sample example
1. Create config in `package.json`

  ```json
  {
    "name": "my project",
    "dependencies": {
      "reshape-include": "^1.0.2"
    },
    "reshape": {
      "include": {
        "root": "./"
      }
    }
  }
  ```

2. Create `index.html`

  ```html
  <p>Here's my partial:</p>
  <include src='_partial.html'></include>
  <p>after the partial</p>
  ```

3. Create `_partial.html`
  ```html
  <strong>hello from the partial!</strong>
  ```

4. Run the command in the terminal
  ```bash
  $ reshape -i path/to/input/index.html -o pat/to/output/result.html
  ```
  *Will be automatically found plugin `reshape-include` assembled configuration for it `{ "root": "./"}` and it will be initialized.*

5. Enjoy `result.html`
  ```html
  <p>Here's my partial:</p>
  <strong>hello from the partial!</strong>
  <p>after the partial</p>
  ```

## Options 
### `config`
config.js  
```js
module.exports = {
  parser: require('sugarml'),
  plugins: {
    include: {
      root: './'
    }
  }
};
```
```bash
$ reshape -o output.html -i input.html -c config.js
```

--

### `use`
```bash
$ reshape 
  -o output.html 
  -i input.html 
  -c config.js
  -u reshape-custom-elements
```

--


### `dir`
```bash
$ reshape -o outputFolder/ -i inputFolder/*.html
```

```bash
$ reshape -o outputFolder/ -i inputFolder/**/*.html
```

--


### `replace`
```bash
$ reshape -i input.html -r
```

```bash
$ reshape -i inputFolder/*.html -r
```

### License [MIT](license)

[reshape-url]: http://github.com/reshape/reshape

[npm-url]: https://npmjs.org/package/reshape-cli
[npm-image]: http://img.shields.io/npm/v/reshape-cli.svg?style=flat-square

[travis-url]: https://travis-ci.org/GitScrum/reshape-cli
[travis-image]: http://img.shields.io/travis/GitScrum/reshape-cli/master.svg?style=flat-square&label=unix

[appveyor]:     https://ci.appveyor.com/project/GitScrum/reshape-cli
[appveyor-img]: https://img.shields.io/appveyor/ci/GitScrum/reshape-cli/master.svg?style=flat-square&label=windows

[coveralls-url]: https://coveralls.io/r/GitScrum/reshape-cli
[coveralls-image]: http://img.shields.io/coveralls/GitScrum/reshape-cli.svg?style=flat-square

[depstat-url]: https://david-dm.org/GitScrum/reshape-cli
[depstat-image]: https://david-dm.org/GitScrum/reshape-cli.svg?style=flat-square

[depstat-dev-url]: https://david-dm.org/GitScrum/reshape-cli
[depstat-dev-image]: https://david-dm.org/GitScrum/reshape-cli/dev-status.svg?style=flat-square

[style-url]: https://github.com/sindresorhus/xo
[style]: https://img.shields.io/badge/code_style-XO-5ed9c7.svg?style=flat-square
