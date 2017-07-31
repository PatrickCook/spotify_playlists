# Spotify Authorization With React + React-Router
Authors: Patrick Cook, Carson Holoien

## Server Code Structure

Under the `server` directory are two files `app.js` and `routes.js`. `app.js`
handles all the setup, and all the routes are in, well, `routes.js`.

## Application Flow

The basic flow is this: client hits `/login`, gets redirected to Spotify's auth
url, then gets redirected to `/callback`. If all is good and dandy, we send the
client to `/#/user/${access_token}/${refresh_token}` which triggers the User
page to load via React-Router. If all ain't good, we redirect the client to
`/#/error/${error message}` which triggers the Error page to load via
React-Router.

Once the client has the tokens, it requests information from spotify directly
through use of the [Spotify Web API Client][swj]. This happens in
`client/actions`, and the resulting data is interpreted through our reducer.
Once the client has the data, `User.js` defines how it renders.

## Set Up

Make sure you create your application, get your id and secret, and register
your callback url - `localhost:3000/callback` is what I used - by following
[Spotify's Getting Started Guide][sgs].

## Running

The first thing you'll need to do is set your applications client id, client
secret, and callback url. You can do this via the environment variables
`client_id`, `client_secret`, and `redirect_uri`. Or by typing them into the
code in `server/routes.js`. Fun tip: because we're using [Better NPM Run][bnr],
you can set these in your `package.json` - head over there to see an example.

There are three scripts - `start`, `dev`, and `build`.

To run the production bundle:

~~~bash
$ npm install
$ npm run build
$ npm start
~~~

To run in dev mode (with hot reloading, and un-minified source maps):

~~~bash
$ npm run dev
~~~
