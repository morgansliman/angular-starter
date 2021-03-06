# Angular-starter

## Overview

[Angular-starter](https://github.com/morgansliman/angular-starter/) is a mildly opinionated boilerplate for MEAN stack web development, with tools for building a great experience across many devices. Designed to build productive programmers.

### Features

| Feature                                | Summary                                                                                                                                                                                                                                                     |
|----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Auto-Injection | Seamlessly integrated with [gulp-inject](https://www.npmjs.com/package/gulp-inject), newly compiled CSS files, all necessary AngularJS files, and [Bower](https://bower.io/) components are automatically injected directly into `index.html` so your code just works. No more fumbling through `<script>` tags.                          |
| Built-in Express Server                   | Simple [Express](http://expressjs.com/) server complete with [body-parser](https://www.npmjs.com/package/body-parser), [morgan](https://www.npmjs.com/package/morgan), and [mongoose](https://www.npmjs.com/package/mongoose) pre-configured. (Run `npm start` to start with [gulp-nodemon](https://www.npmjs.com/package/gulp-nodemon))                                                                                                                                                                          |
| Cross-device Synchronization           | Synchronize clicks, scrolls, forms and live-reload across multiple devices as you edit your project. Powered by [BrowserSync](http://browsersync.io). (Run `npm start` and open up the IP provided on other devices on your network)                       |
| Sass support                           | Compile [Sass](http://sass-lang.com/) into CSS with ease, bringing support for variables, mixins and more. (Run `gulp styles` to compile, or just `gulp` to compile and auto-inject CSS files into `index.html`)                                                                                                   |


## Prerequisites

Node.js and npm are essential to Angular development.

<a href="https://docs.npmjs.com/getting-started/installing-node" target="_blank" title="Installing Node.js and updating npm">
Get it now</a> if it's not already installed on your machine.

**Verify that you are running at least node `v4.x.x` and npm `3.x.x`**
by running `node -v` and `npm -v` in a terminal/console window.
Older versions produce errors.


## Create a new project based on the QuickStart

Clone this repo into new project folder (e.g., `my-proj`).
```shell
git clone https://github.com/morgansliman/angular-starter my-proj
cd my-proj
```

## Install dependencies

> See npm version notes above

Install the npm packages described in the `package.json`:

```shell
npm install
```

The `npm install` command will first install all dependencies listed in `package.json`, then it will call `bower install` to install the front-end dependencies listed in `bower.json` ([AngularJS](https://angularjs.org/) & [UI-Router](https://ui-router.github.io/) by default).

When Bower finishes installing its packages, it will call `gulp inject-bower` which will inject the newly installed dependencies into `src/client/index.html` automatically.

> When installing additional packages with bower, always check your `index.html` file to be sure they were injected correctly. This code is not perfect yet; please [open an issue](https://github.com/morgansliman/angular-starter/issues) if you find an error in your dependency injections.


### Delete _non-essential_ files

You can quickly delete the _non-essential_ files (`.git`)
by entering the following command while in the project folder:

> Note: this will also delete the README.md file. If you're reading this in your IDE, [open it in a browser first](https://github.com/morgansliman/angular-starter#delete-non-essential-files)!

```shell
gulp renew
```

> Note: For now, you will still need to manually edit the information inside of `package.json` and `bower.json`. (i.e., name, description, keywords, etc.)

### Create a new git repo
You _could_ start writing code now and throw it all away when you're done.
If you'd rather preserve your work under source control, consider taking the following steps.

Initialize this project as a *local git repo* and make the first commit:
```shell
git init
git add .
git commit -m "Initial commit"
```


Create a *remote repository* for this project on the service of your choice.

Grab its address (e.g. *`https://github.com/<my-profile>/my-proj.git`*) and push the *local repo* to the *remote*.
```shell
git remote add origin <repo-address>
git push -u origin master
```

## Start the app and verify that it works

#### Start the app:

```shell
npm start
```

The `npm start` command first compiles any `.sass` or `.scss` files within `src/client/sass` then auto-injects these along with all your custom AngularJS into the appropriate places in `index.html` then simultaneously re-compiles and runs the Express server in `src/server/index.js` using `gulp-nodemon`.

> Changes made to any `.js`, `.sass`, or `.scss` files are tracked by `gulp-nodemon` and will restart the server, triggering a Sass re-compile and full auto-injection. Changes made to any `.html` file is tracked by `BrowserSync`, and will automatically live-reload the page. If this isn't working as expected, please [open an issue](https://github.com/morgansliman/angular-starter/issues).

#### Verify that it works:

Try changing the `<h1>` tag inside of `src/client/index.html` and watch your browser live-reload your changes when the file is saved!

During startup, BrowserSync logs several IP adresses to the console. Open the appropriate address in another device (connected to the same network) and watch your changes live-reload to all browser instances at the same time! This makes testing your app in multiple environments much easier. (read more about [BrowserSync](http://browsersync.io))

#### Shutdown

Shut it down manually with `Ctrl-C`.

Congrats! You're ready to write your application.

## Usage

#### Command list (in no specific order):


  - `gulp` - Compile Sass and auto-inject CSS/JS files into `index.html`
  - `gulp styles` - Compile Sass (does not auto-inject)
  - `gulp inject` - Auto-injects CSS/JS files from `src/client/app` into `index.html`
  - `gulp inject-bower` - You shouldn't ever need to call this directly; automatically run by Bower after installing a new package
  - `bower install` - Use this command to install new front-end dependencies to `src/client/lib` (auto runs `gulp inject-bower` postinstall)
  - `npm install` - Used as normal (will also run bower install if there are uninstalled dependencies listed in `bower.json`)
  - `npm start` - Used to start app with BrowserSync, Nodemon, Sass auto-compiling, and auto-injection enabled.

Unfortunately, I've discovered some problems and, while this works overall, there are some ways you can break it or send gulp spiraling into an infinite loop. 

Until I fix these bugs, (or someone else does :D) there's a very specific set of rules to follow when using the included commands to keep everything running smoothly:


  - Don't use `bower install` while the server is running. This is most likely going to send gulp into an infinite loop.
  
  
  - Check your index.html after installing any packages through bower to make sure the dependencies were injected correctly. The filtering is not very specific so there's often unwanted/unneeded css/js files that get added. 
  
  
  - If bower injection is really more of a hassle than a help for you, default to sourcing from a CDN as usual, just don't put the CDN tags inside of the auto-injection comments or they will be overwritten.
