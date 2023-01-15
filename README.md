//Alexander Cayer 1-13-2023 CSC 560 Assignment 1.1 GitHub
//Purpose of the assignment: Making a repository for server from unit 1, which is based on the Tutorialspoint.com article on Node.js, after making the server.js and users.json files, installing node and npm, typing in the npm commands in command prompt, and executing the 4 endpoint functions of listUsers, addUser, showDetail, and deleteUser.
//Note: View in "raw" to see correct spacing regardding each file.

//Purpose of the users.json file below (text section here): To define three starting users and information about them in order to work together with the server.js file and when working within API applications.
//Postman, as noted by them on their web page, is one example of a API application and "platform" (Postman, n.d.). 
{
   "user1" : {
      "name" : "mahesh",
      "password" : "password1",
      "profession" : "teacher",
      "id": 1
   },
   
   "user2" : {
      "name" : "suresh",
      "password" : "password2",
      "profession" : "librarian",
      "id": 2
   },
   
   "user3" : {
      "name" : "ramesh",
      "password" : "password3",
      "profession" : "clerk",
      "id": 3
   }
}

//End of user.json here.

//Beginning of server.js file down below:

//Purpose of the server.js file below (acts as text section here on GitHub): To help define the 4 endpoint functions and information needed to perform the 4 API tasks of listUsers, addUser, showDetail (or ":id"), and deleteUser (Tutorialspoint.com, n.d.). 
//These requests are made in Postman by creating a new HTTP request for each task as noted in Dr. Litman's Week 1 presentation slides (Litman, 2023). 
//This .js file acts as the entry point and references the users.json file, which helps people be able to execute the 4 endpoint functions within the API application of Postman.

//defines the express, app, and fs variables while also making sure express, fs, and express() parts are executed and fully fleshed out.
var express = require('express');
var app = express();
var fs = require("fs");

//listUsers: This code below allows users to be able to list the users from the users.json file or in this case, would be three users.
//So, utilizing the "GET" technique and typing in "localhost:8081/listUsers" and pushing the "Send" button in Postman as noted in Tutorialspoint.com's article would would get this result (Tutorialspoint.com, n.d.).

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

//addUser is executed in Postman through using the "POST" technique, typing in "localhost:8081/addUser," and pushing the "Send" button (Tutorialspoint.com, n.d.).
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
//showDetail is executed in Postman through using the "GET" technique, typing in "localhost:8081/2," and pushing the "Send" button (Tutorialspoint.com, n.d.).
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
//deleteUser is executed in Postman through using the "DELETE" technique, typing in "localhost:8081/deleteUser," and pushing the "Send" button (Tutorialspoint.com, n.d.).

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


//The last few lines of server.js focus on the server listening at HTTP port 8081, which allows people to test the server with applications like Postman whether it is with listUsers, addUser, showDetail, and/or deleteUser.
var server = app.listen(8081, function () {
   var host = server.address().address
   var port = server.address().port
   console.log("Example app listening at http://%s:%s", host, port)
})

//End of server.js file here.

//References:
//Debugger. (2022). Code: 'MODULE_NOT_FOUND' | Bug Report | NODE JS | Beginners [Video]. YouTube. https://www.youtube.com/watch?v=TsHqAZgQtOc
//GitHub. (n.d.). Hello World exercise. GitHub Docs. Retrieved January 14, 2023, from https://docs.github.com/en/get-started/quickstart/hello-world
Referred to this page to help complete the GitHub tutorial and utilized this knowledge to help set up my GitHub repository link for my response for the server task in assignment 1.1.
//Litman, M. (2023). CSC-560: Intro and Unit 1. Referred to the slideshow to make sure I understood the concepts and steps needed to help me complete the server.js and users.json setup.
//Postman. (n.d.). Postman home page. Retrieved January 13, 2023, from https://www.postman.com/. This is where I found that this can act as an application for running APIs.
//Telusko. (2021). Node JS Installation [Video]. YouTube. https://www.youtube.com/watch?v=JINE4D0Syqw
//Tutorialspoint.com. (n.d.). Node.js-RESTful API. Retrieved January 13, 2023, from https://www.tutorialspoint.com/nodejs/nodejs_restful_api.htm. Referred to this page when creating the server.js and users.json files but did explain the purpose behind each part regarding these files as comments.
