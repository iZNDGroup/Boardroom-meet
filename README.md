[![Build Status](https://travis-ci.org/aullman/opentok-meet.svg?branch=master)](https://travis-ci.org/aullman/opentok-meet)
[![Code Climate](https://codeclimate.com/github/aullman/opentok-meet/badges/gpa.svg)](https://codeclimate.com/github/aullman/opentok-meet)
[![Test Coverage](https://codeclimate.com/github/aullman/opentok-meet/badges/coverage.svg)](https://codeclimate.com/github/aullman/opentok-meet)

boardroom-meet
===============

Opentok app with screen sharing using the WebRTC screen sharing and Archiving features. You can check it out running at [meet.boardroom.work(https://meet.boardroom.work).

## Mobile Applications

There are a few different mobile applications that have been built to interoperate with this application. 

* [meet-swift](https://github.com/robjperez/meet-swift) An iOS app built in Swift.
* [opentok-meet-android](https://github.com/opentok/opentok-meet-android) and Android application.

## Running locally

1. If you haven't already, [sign up for OpenTok](https://tokbox.com/signup).
1. Clone this repo
2. `cp config.json.sample config.json`
3. Add your OpenTok apikey and secret to config.json
4. Create your screensharing extensions by following the instructions at https://github.com/opentok/screensharing-extensions and put your Chrome Extension ID in config.json.
4. Run redis. You can find instructions for doing this [here](https://redis.io/topics/quickstart).
5. `npm install` (you will need at least 1GB memory for this step)
6. If you want to use SSL you will need to generate a key and make sure the server.key and server.crt files are in the main directory. You can find instructions for generating a self-signed certificate [here](https://devcenter.heroku.com/articles/ssl-certificate-self). SSL is recommended so that screen-sharing works and so that you don't have to keep clicking the allow button to allow access to your camera. If you still don't want to use SSL then just update [app.js](app.js) to use `http.createServer` instead of `https.createServer`.
7. `npm start`
8. Go to https://localhost:3000

## Running on Heroku

1. If you haven't already, [sign up for OpenTok](https://tokbox.com/signup).
1. Create a [Heroku](heroku.com) instance
2. Clone this repo
3. In the repo run `heroku git:remote -a <instance name>` to add the remote to github.
4. Add redistogo `heroku addons:add redistogo`
5. Add your OpenTok API Key and Secret and your Chrome Screensharing Extension ID to the environment `heroku config:set HEROKU=true OT_API_KEY=<YOUR_API_KEY> OT_API_SECRET=<YOUR_SECRET> CHROME_EXTENSION_ID=<YOUR_EXTENSION_ID>`
6. `git push heroku master`
7. Visit your heroku URL

## Running Tests

You can run the unit tests using `npm test`. This command is setup to work correctly in the Travis CI system as well as when running locally. But if you want it to run locally you need to setup a few things. You will need to sign up for [Sauce Labs](https://saucelabs.com/). This service offers [free options for Open Source](https://saucelabs.com/open-source). You will need the following environment variables set.

```
export SAUCE_USERNAME=<YOUR_SAUCE_USERNAME>
export SAUCE_ACCESS_KEY=<YOUR_SAUCE_KEY>
export TRAVIS_JOB_NUMBER=<ANYTHING>
```

By default `npm test` will run the tests in Chrome Stable. If you want to run in different environments you can set the `BROWSER` and `BVER` environment variables. eg. `export BROWSER=ie BVER=11;npm test`. Supported combinations are:

* ie (10,11)
* chrome (stable, beta, unstable)
* firefox (stable, beta, unstable)

These tests are also run in the cloud with every commit and every pull request using [Travis-CI](travis-ci.org) and [Sauce Labs](https://saucelabs.com/).
