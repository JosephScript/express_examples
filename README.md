# express_examples

``` javascript
var express = require('express');
var app = express();
var path = require('path');

// always use __dirname plus the directory for best results
app.use('/static', express.static(__dirname + '/static'));

// use path.join to use relative paths
var relativePath = path.join(__dirname + '../../another/folder');
app.use('/public', express.static(relativePath));

// send a single file
app.get('/', function(req,res,next){
   res.sendFile(path.join(__dirname, './index.html'));
});

// how to get
app.get('/', function(req, res, next) {
  next();
});

// how to post
app.post('/', function(req, res, next) {
  next();
});

// how to update
app.put('/', function(req, res, next) {
  next();
});

// how to delete
app.delete('/', function(req, res, next) {
  next();
});

// or use 'router' to chain them
app.router('/').get(function(req, res, next) {
  next();
}).post(function(req, res, next) {
  next();
}).put(function(req, res, next) {
  next();
}).delete(function(req, res, next) {
  next();
});

// how to send information
app.get('/hello', function(req, res, next) {
  res.send('Hello! cruel world!');
});

// match acd and abcd
app.get('/ab?cd', function(req, res, next) {
  res.send('Goodbye cruel world!');
});

// match abcd, abbbbbbcd any number of 'b'
app.get('/ab+cd', function(req, res, next) {
  res.send('Goodbye cruel world!');
});

// match abcd, abqwertycd
app.get('/ab*cd', function(req, res, next) {
  res.send('Goodbye cruel world!');
});

// will match butterfly, dragonfly, but not flyman
app.get(/.*fly$/, function(req, res, next) {
  res.send('woo');
});

// we can create new middleware and put it in the middle of our functions!
function logger(req, res, next) {
  // do something, then pass it to the next function
  console.log('Request made at ' + req.url);
  next();
}
app.get('/log', logger, function(req, res, next) {
  res.send('woo it logged');
});

// how to respond to everything else
app.get('/*', function(request, response, next) {
  next();
});

// this actually starts our server!
var server = app.listen(3000, function() {
  var host = server.address().address;
  var port = server.address().port;
  console.log('Example app listening at http://%s:%s', host, port);
});
```
