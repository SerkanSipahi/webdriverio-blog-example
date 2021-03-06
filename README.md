
# WebdriverIO Examples 

[![CircleCI](https://circleci.com/gh/EastCoastProduct/webdriverio-blog-example.svg?style=svg)](https://circleci.com/gh/EastCoastProduct/webdriverio-blog-example)

This repo serves as a companion to a [blog post where I explain why I love WebdriverIO](https://blog.eastcoastproduct.com/webdriverio-why-and-how-to-use-it-for-testing) and contains several examples that I discussed in the blog post. These examples show how to set up and utilize [WebdriverIO](http://webdriver.io/) using [Mocha](https://mochajs.org/), [Gulp](http://gulpjs.com/) and [Chai](http://chaijs.com/) for automated checking of the [craigslist](https://boston.craigslist.org/) classifieds page. I will be continuously updating this and keep adding more examples as I explore more of WebdriverIO’s functionalities I haven't had a chance to use before.

##Environment setup

First, you need to install [Node.js](https://nodejs.org/en/).

Then, the easiest way to start is to clone this repository and install its dependencies:

```
clone https://github.com/EastCoastProduct/webdriverio-blog-example.git && cd webdriverio-blog-example
npm install
``` 

This will install all the packages needed to run the checking scripts locally.

The postinstall script will automatically install the [Selenium Standalone server](http://www.seleniumhq.org/download/) and browser drivers (drivers available for Chrome, Internet Explorer, Firefox and PhantomJS). Only the Chrome and Firefox drivers get installed by default.

Now, install gulp globally 
```
npm install -g gulp
```
and the environment is set up!

##Setting up the configuration file

If you've cloned the repo, then you have my *wdio.conf.js* and you don't need to set it up. If you want to customize the configurnation file, type
```
wdio config
```
into the command line and answer the questions about your project.

##Running the scripts

Type ```gulp test``` in the project folder command line to start the automated checking scripts.

In the *package.json* file, under "scripts", I added a few handy scripts that do a log cleanup from previous checks (delete the report, results and error folders) and build and open a report after the checks finish running. I had to separate the commands that generate the report (```allure generate allure-results```) and open it (```allure report open```), because it fails the CI (the environment doesn't support the opening of a browser). But, if you're going to run the checks locally, without a CI tool, you can combine the two tasks into one like this:

```
javascript
   "scripts": {
     "cleanup": "rm -rf ./allure-results && rm -rf ./allure-report && rm -rf ./errorShots",
     "pretest": "npm run cleanup",
     "test": "./node_modules/.bin/gulp test",
     "report": "allure generate allure-results && allure report open",
     "posttest": "npm run report",
     "postinstall": "./node_modules/.bin/selenium-standalone install"
  },
```

