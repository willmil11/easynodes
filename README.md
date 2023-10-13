# Easynodes

## Installation
Warning: This package is not yet published to npm. This is a placeholder for when it is published.
```bash
npm install easynodes
```

## Usage
First require the package
```js
var easynodes = require('easynodes');
```
Then init the package if you don't everything else that you do will throw an error. The syntax is as below
```js
easynodes.init(verbose, custom-prefix)
//Verbose must be boolean
//Custom-prefix must be a string or not defined
```
Then here's how to use the package.
### Logging
Here's how to change the custom prefix:
```js
easynodes.logging.changeprefix("new-prefix")
```
Here's how to disable verbose
```js
easynodes.logging.disableverbose()
```
Here's how to enable verbose
```js
easynodes.logging.enableverbose()
```
### HTTP
Here's how to make an http request syncronously.
<br>
<br>
For this you'll be required to use an async function in order to use await to wait for the request to finish.
```js
var run = async function() {
    //Get response
    var response = await easynodes.http.get.sync("url");
    console.log(response);
}
//Launch that
run();
```
Here's how to make an http request asyncronously.
```js
easynodes.http.get.async("url", function(request) {
    //Defining a variable to receive the data
    var data = "";
    //Set an event for when data is received
    request.on("data", function(chunk) {
        //Add the chunk to the data variable
        data += chunk;
    });
    //Set an event for when the request is finished
    request.on("end", function() {
        console.log(data);
    });
    
    //You could also abort the request like this
    request.abort();
    //
    //Or you can get the http code as this
    console.log(request.statusCode);
    //
    //And you can remove all set events for the request like this
    request.removeEvents();
});
```
You can also create an http server like this
```js
easynodes.http.newServer(function(requestHandler){
    //You are not required to specify the authorised ip but you're required to specify the port
    //
    //You can get the ip of the client as this:
    console.log(requestHandler.ip);
    //You can get the url of the request as this:
    console.log(requestHandler.url);
    //You can get the method of the request as this:
    console.log(requestHandler.method);
    //You can get the headers of the request as this:
    console.log(requestHandler.headers);
    //You can write text to request as this (Note that the httpCode and writeHead are optional and can only be set once per request)
    requestHandler.write("Hello ", 200, {"Content-Type": "text/plain", "Access-Control-Allow-Origin": "*"});
    //You can end the request as this (You can also set httpcode and writeHead here but we already did that above also you can just end the request without any data)
    requestHandler.end("World!");

}, port, ip)
```
### Websocket
Here's how to create a websocket client
```js
easynodes.websocket.newClient("adress", function(client){
    //When this code is ran it means that the client is opened
    //You can send data to the server like this
    client.send("Hello");
    //You can set an event for when the client receives data like this
    client.onmessage(function(data){
        //You can get the data like this
        console.log(data);
    });
    //You can set an event for when the client is closed like this
    client.onclose(function(){
        console.log("Client closed");
    });
    //You can close the client like this
    client.close();
    //You can remove all events for the client like this
    client.removeEvents();
})
```
Here's how to create a websocket server
```js
easynodes.websocket.newServer(port, function(client){
    //When this code is ran it means that a new client connected
    //You can send data to the client like this
    client.send("Hello");
    //You can set an event for when the client receives data like this
    client.onmessage(function(data){
        //You can get the data like this
        console.log(data);
    });
    //You can set an event for when the client is closed like this
    client.onclose(function(){
        console.log("Client closed");
    });
    //You can close the client like this
    client.close();
    //You can remove all events for the client like this
    client.removeEvents();
})
```
### Filesystem
Here's how to read a file syncronously
```js
var data = easynodes.files.read.sync("path");
console.log(data);
```
Here's how to read a file asyncronously
```js
easynodes.files.read.async("path", function(data){
    console.log(data);
});
```
Here's how to write to a file syncronously
```js
easynodes.files.write.write.sync("path", "data");
```
Here's how to write to a file asyncronously
```js
easynodes.files.write.write.async("path", "data", function(){
    console.log("Done");
});
```
Here's how to append to a file syncronously
```js
easynodes.files.write.add.sync("path", "data");
```
Here's how to append to a file asyncronously
```js
easynodes.files.write.add.async("path", "data", function(){
    console.log("Done");
});
```
Here's how to get the path of the current directory
```js
var path = easynodes.files.getDirname();
console.log(path);
```
Here's how to delete a file/folder syncronously
```js
easynodes.files.delete.sync("path");
```
Here's how to delete a file/folder asyncronously
```js
easynodes.files.delete.async("path", function(){
    console.log("Done");
});
```
Here's how to copy a file/folder syncronously
```js
easynodes.files.copy.sync("path", "new-path");
```
Here's how to copy a file/folder asyncronously
```js
easynodes.files.copy.async("path", "new-path", function(){
    console.log("Done");
});
```
Here's how to move a file/folder syncronously
```js
easynodes.files.move.sync("path", "new-path");
```
Here's how to move a file/folder asyncronously
```js
easynodes.files.move.async("path", "new-path", function(){
    console.log("Done");
});
```
Here's how to create a folder syncronously
```js
easynodes.files.create.folder.sync("path");
```
Here's how to create a folder asyncronously
```js
easynodes.files.create.folder.async("path", function(){
    console.log("Done");
});
```
Here's how to create a file syncronously
```js
easynodes.files.create.file.sync("path", "optional-data");
```
Here's how to create a file asyncronously
```js
easynodes.files.create.file.async("path", "optional-data", function(){
    console.log("Done");
});
```
Here's how to rename a file/folder syncronously
```js
easynodes.files.rename.sync("path", "new-path");
```
Here's how to rename a file/folder asyncronously
```js
easynodes.files.rename.async("path", "new-path", function(){
    console.log("Done");
});
```
Here's how to check if a file/folder exists syncronously
```js
var exists = easynodes.files.exists.sync("path");
console.log(exists);
```
Here's how to check if a file/folder exists asyncronously
```js
easynodes.files.exists.async("path", function(exists){
    console.log(exists);
});
```
Here's how to get the type of the path (file or folder) syncronously
```js
var type = easynodes.files.getTypeOf.sync("path");
console.log(type);
```
Here's how to get the type of the path (file or folder) asyncronously
```js
easynodes.files.getTypeOf.async("path", function(type){
    console.log(type);
});
```
Here's how to get the size of a file/folder in the most humman readable format possible syncronously
```js
var size = easynodes.files.getSize.sync("path");
console.log(size);
```
Here's how to get the size of a file/folder in the most humman readable format possible asyncronously
```js
easynodes.files.getSize.async("path", function(size){
    console.log(size);
});
```
Here's how to get the permissions of a file/folder as a number syncronously
```js
var permissions = easynodes.files.getPermissions.asNumber.sync("path");
console.log(permissions);
```
Here's how to get the permissions of a file/folder as a number asyncronously
```js
easynodes.files.getPermissions.asNumber.async("path", function(permissions){
    console.log(permissions);
});
```
Here's how to get the permissions of a file/folder as a string syncronously
```js
var permissions = easynodes.files.getPermissions.asString.sync("path");
console.log(permissions);
```
Here's how to get the permissions of a file/folder as a string asyncronously
```js
easynodes.files.getPermissions.asString.async("path", function(permissions){
    console.log(permissions);
});
```
Here's how to set the permissions of a file/folder syncronously
```js
//The permissions must be a number
easynodes.files.setPermissions.sync("path", permissions);
```
Here's how to set the permissions of a file/folder asyncronously
```js
//The permissions must be a number
easynodes.files.setPermissions.async("path", permissions, function(){
    console.log("Done");
});
```
