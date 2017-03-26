# api documentation for  [live-server (v1.2.0)](https://github.com/tapio/live-server#readme)  [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-live-server.svg)](https://travis-ci.org/npmdoc/node-npmdoc-live-server)
#### simple development http server with live reload capability

[![NPM](https://nodei.co/npm/live-server.png?downloads=true)](https://www.npmjs.com/package/live-server)

[![apidoc](https://npmdoc.github.io/node-npmdoc-live-server/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-live-server_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-live-server/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-live-server/build/screen-capture.npmPackageListing.svg)



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
            "name": "tapio",
            "email": "tapiovierros@gmail.com"
        }
    ],
    "name": "live-server",
    "optionalDependencies": {},
    "preferGlobal": true,
    "readme": "ERROR: No README data found!",
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



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module live-server](#apidoc.module.live-server)
1.  [function <span class="apidocSignatureSpan">live-server.</span>shutdown ()](#apidoc.element.live-server.shutdown)
1.  [function <span class="apidocSignatureSpan">live-server.</span>start (options)](#apidoc.element.live-server.start)
1.  number <span class="apidocSignatureSpan">live-server.</span>logLevel
1.  object <span class="apidocSignatureSpan">live-server.</span>server
1.  object <span class="apidocSignatureSpan">live-server.</span>watcher



# <a name="apidoc.module.live-server"></a>[module live-server](#apidoc.module.live-server)

#### <a name="apidoc.element.live-server.shutdown"></a>[function <span class="apidocSignatureSpan">live-server.</span>shutdown ()](#apidoc.element.live-server.shutdown)
- description and source-code
```javascript
shutdown = function () {
	var watcher = LiveServer.watcher;
	if (watcher) {
		watcher.close();
	}
	var server = LiveServer.server;
	if (server)
		server.close();
}
```
- example usage
```shell
...
	- '--ignorePattern=RGXP' exclude files from watching by regexp (@psi-4ward)
	- '--watch=PATH' cli option to only watch given paths
* v0.9.0
	- '--mount=ROUTE:PATH' cli option to specify alternative routes to paths (@pmentz)
	- '--browser=BROWSER' cli option to specify browser to use (@sakiv)
	- Improved error reporting
	- Basic support for injecting the reload code to SVG files (@dotnetCarpenter, @tapio)
	- LiveServer.shutdown() function to close down the server and file watchers
	- If host parameter is given, use it for browser URL instead of resolved IP
	- Initial testing framework (@harrytruong, @evanplaice, @tapio)
* v0.8.2
	- Load initial settings from '~/.live-server.json' if exists (@mikker)
	- Allow '--port=0' to select random port (@viqueen)
	- Fix injecting when file extension is not lower case (@gusgard)
	- Fail gracefully if browser does not support WebSockets (@mattymaloney)
...
```

#### <a name="apidoc.element.live-server.start"></a>[function <span class="apidocSignatureSpan">live-server.</span>start (options)](#apidoc.element.live-server.start)
- description and source-code
```javascript
start = function (options) {
	options = options || {};
	var host = options.host || '0.0.0.0';
	var port = options.port !== undefined ? options.port : 8080; // 0 means random
	var root = options.root || process.cwd();
	var mount = options.mount || [];
	var watchPaths = options.watch || [root];
	LiveServer.logLevel = options.logLevel === undefined ? 2 : options.logLevel;
	var openPath = (options.open === undefined || options.open === true) ?
		"" : ((options.open === null || options.open === false) ? null : options.open);
	if (options.noBrowser) openPath = null; // Backwards compatibility with 0.7.0
	var file = options.file;
	var staticServerHandler = staticServer(root);
	var wait = options.wait === undefined ? 100 : options.wait;
	var browser = options.browser || null;
	var htpasswd = options.htpasswd || null;
	var cors = options.cors || false;
	var https = options.https || null;
	var proxy = options.proxy || [];
	var middleware = options.middleware || [];

	// Setup a web server
	var app = connect();

	// Add logger. Level 2 logs only errors
	if (LiveServer.logLevel === 2) {
		app.use(logger('dev', {
			skip: function (req, res) { return res.statusCode < 400; }
		}));
	// Level 2 or above logs all requests
	} else if (LiveServer.logLevel > 2) {
		app.use(logger('dev'));
	}
	if (options.spa) {
		middleware.push("spa");
	}
	// Add middleware
	middleware.map(function(mw) {
		if (typeof mw === "string") {
			var ext = path.extname(mw).toLocaleLowerCase();
			if (ext !== ".js") {
				mw = require(path.join(__dirname, "middleware", mw + ".js"));
			} else {
				mw = require(mw);
			}
		}
		app.use(mw);
	});

	// Use http-auth if configured
	if (htpasswd !== null) {
		var auth = require('http-auth');
		var basic = auth.basic({
			realm: "Please authorize",
			file: htpasswd
		});
		app.use(auth.connect(basic));
	}
	if (cors) {
		app.use(require("cors")({
			origin: true, // reflecting request origin
			credentials: true // allowing requests with credentials
		}));
	}
	mount.forEach(function(mountRule) {
		var mountPath = path.resolve(process.cwd(), mountRule[1]);
		if (!options.watch) // Auto add mount paths to wathing but only if exclusive path option is not given
			watchPaths.push(mountPath);
		app.use(mountRule[0], staticServer(mountPath));
		if (LiveServer.logLevel >= 1)
			console.log('Mapping %s to "%s"', mountRule[0], mountPath);
	});
	proxy.forEach(function(proxyRule) {
		var proxyOpts = url.parse(proxyRule[1]);
		proxyOpts.via = true;
		proxyOpts.preserveHost = true;
		app.use(proxyRule[0], require('proxy-middleware')(proxyOpts));
		if (LiveServer.logLevel >= 1)
			console.log('Mapping %s to "%s"', proxyRule[0], proxyRule[1]);
	});
	app.use(staticServerHandler) // Custom static server
		.use(entryPoint(staticServerHandler, file))
		.use(serveIndex(root, { icons: true }));

	var server, protocol;
	if (https !== null) {
		var httpsConfig = https;
		if (typeof https === "string") {
			httpsConfig = require(path.resolve(process.cwd(), https));
		}
		server = require("https").createServer(httpsConfig, app);
		protocol = "https";
	} else {
		server = http.createServer(app);
		protocol = "http";
	}

	// Handle server startup errors
	server.addListener('error', function(e) {
		if (e.code === 'EADDRINUSE') {
			var serveURL = protocol + '://' + host + ':' + port;
			console.log('%s is already in use. Trying another port.'.yellow, serveURL);
			setTimeout(function() {
				server.listen(0, host);
			}, 1000);
		} else {
			console.error(e.toString().red);
			LiveServer.shutdown();
		}
	});

	// Handle successful server
	server.addListener('listening', function(/*e*/) {
		LiveServer.server = server;

		var address = server.address();
		var serveHost = address.address === "0.0.0.0" ? "127.0.0.1" : address.address;
		var openHost = host === "0.0.0.0" ? "127.0.0.1" : host;

		var serveURL = protocol + '://' + serveHost + ':' + address.port;
		var openURL = protocol + '://' + openHost + ':' + address.port;

		var serveURLs = [ serveURL ];
		if (LiveServer.logLevel > 2 && address.address === "0.0.0.0") {
			var ifaces = os.networkInterfaces() ...
```
- example usage
```shell
...
	ignore: 'scss,my/templates', // comma-separated string for paths to ignore
	file: "index.html", // When set, serve this file for every 404 (useful for single-page applications)
	wait: 1000, // Waits for all changes, before reloading. Defaults to 0 sec.
	mount: [['/components', './node_modules']], // Mount a directory to a route.
	logLevel: 2, // 0 = errors only, 1 = some, 2 = lots
	middleware: [function(req, res, next) { next(); }] // Takes an array of Connect-compatible middleware that are injected into the
 server middleware stack
};
liveServer.start(params);
'''

HTTPS
---------------

In order to enable HTTPS support, you'll need to create a configuration module.
The module must export an object that will be used to configure a HTTPS server.
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
