# docker-nodejs-webserver-template
Simplest possible template with Docker, NodeJS and a webserver

```Dockerfile
FROM node:12-alpine
ADD ./server.js
CMD server.js
```

```js
const net = require('net');
const port = 8080;

const server = net.createServer();

server.listen(port, function() {
    console.log('listening on', port);
});

server.on('connection', function(socket) {
    
    console.log('connection');
    
    socket.write('Oh hi there!');
    
    socket.on('data', function(chunk) {
        console.log('data:', chunk.toString());
    });
    socket.on('end', function() {
        console.log('end');
    });
    socket.on('error', function(err) {
        console.log('error:', err);
    });

});
```