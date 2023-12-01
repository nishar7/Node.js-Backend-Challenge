# Node.js-Backend-Challenge
This project is a Node.js backend application that demonstrates user authentication and profile management using MongoDB as the database. It provides a set of RESTful API endpoints for user registration, login, profile retrieval, profile update, and profile deletion. 

#Git was crashing while uploading the Files. Please Download ZIP file and review
Sorry for inconvenience
Name:Nishar Bafna
Email: nisharbafna7@gmail.com




Challenge Details:
Objective: Develop a robust and scalable Node.js backend using MongoDB as your database.

Required Features:
User Authentication: Implement a secure login/logout system.
MongoDB Integration: Use MongoDB for data storage. Demonstrate how to perform CRUD (Create, Read, Update, Delete) operations.
API Development: Create RESTful APIs for the following functionalities:
User Profile Management: Allow users to create, view, and edit their profiles.
Post Creation and Retrieval: Enable users to create posts and retrieve them.
Commenting System: Users should be able to comment on posts.
Error Handling: Implement comprehensive error handling and logging.
Documentation: Provide clear documentation on the setup and usage of your backend.



Step by Step Making of the Project

1)Initializing Node.js Project
Run the following command to initialize a new Node.js project:  npm init

npm will generate a package.json file. This file contains metadata about your project and its dependencies.

Folder of Package.json
{
  "name": "node_task",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "bcrypt": "^5.1.1",
    "body-parser": "^1.20.2",
    "ejs": "^3.1.9",
    "express": "^4.18.2",
    "mongodb": "^6.3.0",
    "mongoose": "^8.0.2",
    "multer": "^1.4.5-lts.1",
    "yarn": "^1.22.21"
  }
}

//color is because code is copied from VS CODE

Dependencies required for this task are as follows:

npm install express 
npm install mongoose
npm install bcrypt
Npm install multer

2)User Authentication

Implement User Model
Created a User schema using Mongoose to define the structure of user data in MongoDB. In your models/User.js file:

const mongoose = require("mongoose");
mongoose.connect("mongodb://127.0.0.1:27017/User_Management_System");

const express = require("express");
const app = express();


//for user routes
const userRoute = require('./routes/userRoute');
app.use('/userRoute')

app.listen(3000, function(){
    console.log("Server is running..");
});

User Registration
Developed an API endpoint to handle user registration. Used Express to define a route that receives user data, hashes the password using Bcrypt, and stores it in MongoDB.
//color is because of the code is copied from vs code
const User = require('../models/usermodel');
const bcrypt = require('bcrypt');
const securePassword = async(password)=>{
    try{
        const passwordHash = await bcrypt.hash(password, 10);
        return passwordHash;
    }
    catch (error){
        console.log(error.message);
    }
}
const loadRegister = async(req, res) =>{
    try{
       res.render('registration');
    }
    catch(error){
        console.log(error.message);
    }
}

const insertUser = async(req, res) =>
{
    try{
        const spasswod = securePassword(req.body.password);
        const user = new User({
           name:req.body.name,
           email:req.body.email,
           mobile:req.body.mno,
           image:req.file.filname,
           name:req.body.password,
          is_admin:0
           

        });

        const userData = await user.save();

        if(userData){
             res.render('registration', {message:"Successfully registered, Please verify email"});
        }
        else{
            res.render('registration', {message:"Registration Failed"});
        }
    }catch(error){
        console.log(error.message);
    }
}
Module.exports = { loadRegister}




3. MongoDB Integration
Connected to MongoDB,we used Mongoose, a MongoDB object modeling tool. First, installed Mongoose as a dependencies
Performed CRUD Operations(Create, Read, Update, Delete)



4. API Development

Set up an Express.js application to handle API routes. In your main application file (e.g., index.js), initialize Express and set up middleware
Created API for all the required functions such as:
  Insert user
  Register User
  Edit Profile and many more…
    onst express = require("express");
const user_route = express();

user_route.set('view engine', 'ejs');
user_route.set('views', './views/users');

const bodyParser = require('body-parser');
user_route.use(bodyParser.json());
user_route.use(bodyParser.urlencoded({extended:true}))

const multer = require("multer");
const path = require("path");

user_route.use(expres.static('public'));

const storage = multer.diskStorage({
    destination:function(req,file,cb){
        cb(null, path.join(___dirname, '/public/userImages'));
    },
    filename:function(){
        const name = Date.now() + '-'+file.originalname;
        cb(null,name);
    }
});
const upload = multer ({storage : storage});
const usercontoller = require("../controllers/userController");

user_route.get('/register', usercontoller.loadRegister);

user_route.post('/register', upload.single('image'),usercontoller.insertUser);

user_route.get('/', usercontoller.loginLoad);
user_route.get('/login', usercontoller.loginLoad);

user_route.get('/logout', auth.isLogin, userController.userLogout);
user_route.get('/home', auth.isLogin, usercontoller.loadHome);

user_route.get('/edit', auth.isLogin, usercontoller.editLoad);

user_route.post('/edit', upload.single('image'), userContoller.updateProfile);

module.exports = user_route;


4) Additional Feature
I added an additional feature of User Verification via Email which updates on the MongoDB i.e Database in real-time.














         
















                Fig 15: Updated (NEW) Data of User















