# Cartero Screen Cast Outline
## Intro

> Cartero is a client side asset managment tool that enables users to have a modular front-end architecture. I am going to demo Cartero setup and workflow with a simple express server.

## Install dependencies and create Express server
First lets install all our dependencies with:

```
npm install express cartero cartero-express-hook jade grunt grunt-contrib-watch
```

And create a basic Express server at `app.js`:
```javascript
var express = require( 'express' );
var path = require( 'path' );
var app = express();
var carteroMiddleware = require( 'cartero-express-hook' );

app.configure( function() {
    app.set( 'views' , path.join( __dirname, 'views' ) );
    app.engine( 'jade', require( 'jade' ).__express );
    app.use( express.static( path.join( __dirname, 'static' ) ) );
    app.use( carteroMiddleware( __dirname ) );  // install the Cartero Hook
} );

app.get( '/', function( req, res ) {
  res.render( 'home/home.jade', function( err, html ) {
    res.send( html );
  } );
} );

app.listen( '8000' );
```
