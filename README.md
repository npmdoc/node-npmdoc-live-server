# npmdoc-live-server

#### api documentation for  [live-server (v1.2.0)](https://github.com/tapio/live-server#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-live-server.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-live-server) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-live-server.svg)](https://travis-ci.org/npmdoc/node-npmdoc-live-server)

#### simple development http server with live reload capability

[![NPM](https://nodei.co/npm/live-server.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/live-server)

- [https://npmdoc.github.io/node-npmdoc-live-server/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-live-server/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-live-server/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-live-server/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-live-server/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-live-server/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Tapio Vierros"
    },
    "bin": {
        "live-server": "./live-server.js"
    },
    "bugs": {
        "url": "https://github.com/tapio/live-server/issues"
    },
    "dependencies": {
        "chokidar": "^1.6.0",
        "colors": "latest",
        "connect": "3.5.x",
        "cors": "latest",
        "event-stream": "latest",
        "faye-websocket": "0.11.x",
        "http-auth": "3.1.x",
        "morgan": "^1.6.1",
        "object-assign": "latest",
        "opn": "latest",
        "proxy-middleware": "latest",
        "send": "latest",
        "serve-index": "^1.7.2"
    },
    "description": "simple development http server with live reload capability",
    "devDependencies": {
        "eslint": "^3.13.0",
        "jshint": "^2.9.2",
        "mocha": "^3.2.0",
        "supertest": "^2.0.1"
    },
    "directories": {},
    "dist": {
        "shasum": "4498644bbf81a66f18dd8dffdef61c4c1c374ca3",
        "tarball": "https://registry.npmjs.org/live-server/-/live-server-1.2.0.tgz"
    },
    "engines": {
        "node": ">=0.10.0"
    },
    "eslintConfig": {
        "env": {
            "node": true
        },
        "rules": {
            "quotes": 0,
            "curly": 0,
            "strict": 0,
            "no-process-exit": 0,
            "eqeqeq": 1,
            "no-unused-vars": 1,
            "no-shadow": 1
        }
    },
    "gitHead": "6a77f048559fdeaf98ed135c04a9082ff2dfa281",
    "homepage": "https://github.com/tapio/live-server#readme",
    "keywords": [
        "front-end",
        "development",
        "tool",
        "server",
        "http",
        "cli"
    ],
    "license": "MIT",
    "maintainers": [
        {
            "name": "tapio"
        }
    ],
    "name": "live-server",
    "optionalDependencies": {},
    "preferGlobal": true,
    "repository": {
        "type": "git",
        "url": "git+https://github.com/tapio/live-server.git"
    },
    "scripts": {
        "hint": "jshint live-server.js index.js",
        "lint": "eslint live-server.js index.js",
        "test": "mocha test && npm run lint"
    },
    "version": "1.2.0"
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
