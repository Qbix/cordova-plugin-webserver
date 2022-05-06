# cordova-plugin-webserver
Cordova plugin for localhost web server written in Kotlin and Ktor

## Install plugin
    cordova plugin add https://github.com/Qbix/cordova-plugin-webserver.git
## Supported platforms
- __Android@9.0.0__

## Let's start
- __First step:__ In your index.js file add this line to start the web server
```js
cordova.plugins.webServer.startServer(function(result) { console.log(result); }, function(error) { console.log(error); })
```
- __Second step:__ Build and run your app. Voila, enjoy the web server!
#### Start Server
```js
cordova.plugins.webServer.startServer(function(result) { console.log(result); }, function(error) { console.log(error); })
```
#### Stop Server
```js
cordova.plugins.webServer.stopServer(function(result) { console.log(result); }, function(error) { console.log(error); })
```
# Requests

## Serving static content
GET request:
```
http://localhost:3005/static-content/{your path from assets directory}
```
__Example__ with serving index.html:
```
http://localhost:3005/static-content/www/index.html
```
## Executing Cordova methods
POST request:
```
curl -X POST -F service=CordovaServiceName -F action=CordovaMethod -F args=["Args"] http://localhost:3005/cordova-request
```
__Example__ with common cordova request:
```js
Q.Users.Cordova.Labels.get(["e"], function(data) { console.log(data); }, function(err) { console.log(err); })
```
equivalent to
```
curl -X POST -F service=QUsersCordova -F action=get -F args=[["e"]] http://localhost:3005/cordova-request
```
## Common errors
- __Not found__ - if static content is not found.
- __Service not found__ - if the web server could not find the service or the structure of the post request was incorrect.
- __Invalid action execution__ - if the web server could not find the action or the structure of the post request was incorrect.
- __Gateway timeout__ - if the web server could not execute cordova request within the timeout.
- __Different callbackId__ - when we run our Cordova request we generate a callbackId, if we get a callbackId different than our callbackId we return an error.
- __Plugin manager is null__ - something wrong happened after initialization.
- __Plugin response is null__ - if plugin response is null.
