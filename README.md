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
Then init the package with the syntax below (For the first arg its verbose to enable verbose mode put true, to disable it put false or nothing any other value will throw an error, the second arg is the prefix if left empty it will be "[Easynodes]" else it will be your prefix. Note that if you disable verbose no message from easynodes will be displayed so it'll be useless to put a special prefix.)
```js
easynodes.init(verbose:true,false,undefined prefix:"string",undefined);
```
Exemples of use:
```js
easynodes.init()
easynodes.init(true)
easynodes.init(false)
easynodes.init(true, "[Custom prefix]")

//Useless
easynodes.init(false, "[Custom prefix]")
```

### HTTP get Sync
To create an HTTP synchronous GET request with easynodes, you'll need to use an asyncronous function, because easynodes need await to wait for the request to be done before returning the result. In this exemple we use easynodes to syncronously make a GET request to Coolcraft servers (My servers) for a text file containg "Hello world!" and printing the result of the request in the console if there is an error it will be printed as "An error has occured %error%"
```js
var app = async function(){
    try{
        var get = await easynodes.http.get.sync("http://89.159.202.47/Text/Hello_world.txt");
        console.log(get);
    }
    catch (error){
        console.error("An error has occured: " + error);
    }
}

app();
```
The output should be either the error or 
```
Hello world!
```
### HTTP get Async
To create an HTTP asyncronous request with easynodes first you'll need the code as below:
```js
try{
    var data = "";
    easynodes.http.get.async("http://89.159.202.47/Text/Hello_world.txt", function(request){
        request.on("data", function(chunk){
            data += chunk
        })
        request.on("end", function(chunk){
            console.log(data);
        })
    })
}
catch (error){
    console.error("An error has occured: " + error);
}
```
Callback values are:
```js
request.removeEvents();
request.on(event, eventcallback);
```
On events callback values are:
```js
request.on("data", function(chunk)){
    //Interact with chunk
})
request.on("end", function(){
    //Request has ended do something
})
```
### HTTP server
To create an HTTP server with easynodes you'll need to use the code below:
```js
easynodes.http.newServer(function(request){
    //Got request

    //Print ip to console
    console.log(request.ip);

    //Print url to console
    console.log(request.url);

    //Print method to console
    console.log(request.method);

    //Print headers to console
    console.log(request.headers);

    //Write data to client and set htttpCode and writeHead (you can only set httpCode and writeHead once)
    request.write("Hello", 200 {"Content-Type": "text/plain", "Content-Length": 12, "Access-Control-Allow-Origin", "*"});

    //End request with some more data (you could also set httpCode and writeHead here but we already did it)
    request.end(" world!");
});
```
Callback values are:
```js
request.