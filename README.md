# make-it-restart [![Build Status](https://travis-ci.org/anuoua/make-it-restart.svg?branch=master)](https://travis-ci.org/anuoua/make-it-restart)

Make command or app restart. e.g. make electron/webpack... restart.

## cli usage

```bash
make-it-restart webpack -w
```

For restarting, type to stdin `rs` and press enter...

## usage

install
```bash
npm install make-it-restart --save-dev
```

create a restartor

```javascript
const restart = require('make-it-restart')
let restartor = restart(command, env)
```

### parameter

- `command`: it supports running commands directly which in `./node_modules/.bin/`, like `npm run`.
- `env`: set environment variables with an object.

## example

script.js
```javascript
let count = 0
console.log(process.env.NODE_ENV)
setInterval(() => {
    console.log(++count)
}, 500)
```

index.js
```javascript
const restart = require('make-it-restart')

let restartor = restart('node ./script.js', { NODE_ENV: 'production' })

restartor()

setInterval(() => {
    restartor()
}, 2000)
```
result
```bash
production
1
2
3
restarting...
production
1
2
3
restarting...
```
