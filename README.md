# web-template
Web client server starter template.
Client and server parts are separate npm projects under one source control root.

Client folder contains build tooling, source code and assets as well as a dist folder where finalized package lands.
Server folder contains build tooling, source code  as well as a dist folder where finalized backend bundle lands.

The server is serving `client/dist` folder and on top of that provides additional endpoints.

In order to run npm commands one needs to `cd` into server or client folder.

##Setup new repository based on web-template

* Create new repository on Github: https://github.com/organizations/Crowdmix/repositories/new

* `git clone <new repository path>` (example: `git clone git@github.com:Crowdmix/web-artist.git`)

* `cd <new repository name>` (example `cd web-artist`)

* `git remote add upstream git@github.com:Crowdmix/web-template.git`
	* (this will add a new remote and allow you to pull in changes to web-template in the future)

* `git pull upstream master`
	* (pull from web-template)

* `git push origin master`

* done


##Working on the client

The minimal setup has:
* ES2015 syntax through babel, sourcemaps support,
* Bundling through webpack,
* ESLint for development,
* HotReload, that is prelinting.
* Testing from console supporting watch mode,

###Available commands:

 * `npm run stampConfig`
 	* "stampConfig": `node config/stampEnv.js`
	 * Determines current node env and copies proper configuration file to dist folder from where it is served to browsers.
 * `npm run build`
 	* "build": `webpack --config webpack.build.config.babel.js`
 	* Builds the distribution bundle and places it in dist folder. Uses production webpack settings.
 *  "predev":
 	* 'npm run stampConfig'
	 * always runs before dev script. Not meant to be used directly.
 *  `npm run dev`
 	* "dev": `webpack-dev-server`
	 * starts a hotreloading development server with sourcemaps and linter.
 *  `npm test`
 	* "test": `mocha --compilers js:babel-core/register --require ./test/test_helper.js 'test/**/*.@(js|jsx)'`,
	 * Runs all tests found in 'test' folder once.
 *  `npm run test:watch`
 	* "test:watch": `npm run test -- --watch --watch-extensions jsx`
	 * Runs all tests found in 'test' folder and watches for changes.

##Working on the server

The minimal setup contains:
* ES2015 syntax through babel transpiler, sourcemaps support
* Bundling with webpack
* ESLint for development
* LiveReload with nodemon. Restarts server on code changes
* Testing from console supporting watch mode
* e2e testing with supertest
* Babel 6 with presets that will do minimum needed for node server

###Available commands:

 *  `npm run build`
 	* "build": `webpack`
	 * builds backend bundle and places it in dist folder.
 *   "prestart":
 	* `cd ../client/; npm run stampConfig`
 	* Executes clients config selection task. Always runs before start script.
 *   `npm start`
 	* "start": `node dist`
	 * Starts server application
 *   "predev":
 	* `npm run build -- --watch &`
	 * Executes before dev task. Kicks off a webpack build in watch mode. Any change to source triggers rebuild.
 *   `npm run dev`
 	* "dev": `nodemon --debug dist --watch dist`
	 * runs backend bundle in dev mode wrapped in nodemon for liveReload. Only compiled bundle is watched so only actual server code changes will trigger reload.
 *   `npm test`
 	* "test": `mocha --compilers js:babel-core/register --require ./test/test_helper.js --recursive`
	 * Runs all tests found in 'test' folder once.
 *   `npm run test:watch`
  	* "test:watch": `npm run test -- --watch`
	  * Runs all tests found in 'test' folder and watches for changes.

##TODO
* CSS pipeline for client.

##MAYBE
* Investigate why linter is not picking up small changes like dangling commas. See : https://github.com/webpack/watchpack/issues/16
* Wallaby integration for unit tests.
* Coverage test for units.
