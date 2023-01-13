






















//Purpose of the server.js file (acts as text section here on GitHub): To help define the 4 endpoint functions and information needed to perform the 4 API tasks of listUsers, addUser, showDetail (or ":id"), and deleteUser (Tutorialspoint.com, n.d.). This .js file acts as the entry point and references the users.json file, which helps people be able to execute the 4 endpoint functions within the API application of Postman.

//defines the express, app, and fs variables while also making sure express, fs, and express() parts are executed and fully fleshed out.
var express = require('express');
var app = express();
var fs = require("fs");

//listUsers: This code below allows users to be able to list the users from the users.json file or in this case, would be three users.
app.get('/listUsers', function (req, res) {
   fs.readFile( __dirname + "/" + "users.json", 'utf8', function (err, data) {
      console.log( data );
      res.end( data );
   });
})

//addUser: Code below is on addUser, which includes details on defining a 4th user while identifying the other users before adding this new person.
var user = {
   "user4" : {
      "name" : "mohit",
      "password" : "password4",
      "profession" : "teacher",
      "id": 4
   }
}

app.post('/addUser', function (req, res) {
   // First read existing users.
   fs.readFile( __dirname + "/" + "users.json", 'utf8', function (err, data) {
      data = JSON.parse( data );
      data["user4"] = user["user4"];
      console.log( data );
      res.end( JSON.stringify(data));
   });
})

//showDetail: The code below focuses on show detail, which fleshes out information on each user.
app.get('/:id', function (req, res) {
   // First read existing users.
   fs.readFile( __dirname + "/" + "users.json", 'utf8', function (err, data) {
      var users = JSON.parse( data );
      var user = users["user" + req.params.id] 
      console.log( user );
      res.end( JSON.stringify(user));
   });
})

//deleteUser: Purpose here is to remove a user based on equalling a certain Id. In the case of the code below, this corresponds to user 2 and results in having information on users 1 and 3 remain.

var id = 2;

app.delete('/deleteUser', function (req, res) {
   // First read existing users.
   fs.readFile( __dirname + "/" + "users.json", 'utf8', function (err, data) {
      data = JSON.parse( data );
      delete data["user" + 2];
       
      console.log( data );
      res.end( JSON.stringify(data));
   });
})


//Lines 64 to 67 focus on the server listening at HTTP port 8081, which allows people to test the server with applications like Postman whether it is with listUsers, addUser, showDetail, and/or deleteUser.
var server = app.listen(8081, function () {
   var host = server.address().address
   var port = server.address().port
   console.log("Example app listening at http://%s:%s", host, port)
})
