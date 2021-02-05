How to recreate this:

$ npm init -y

Create 'server' folder
Create 'index.js' in 'server' folder

$ npm i express

$ npx create-react-app client

add "proxy": "http://localhost:3001" to client/package.json

Deploy to Heroku
Remove '.git'

$ cd client
$ rm -rf .git

IF powershell
Remove-Item .git -Force

Add code 
// server/index.js
const path = require('path');
const express = require('express');
...
// Have Node serve the files for our built React app
app.use(express.static(path.resolve(__dirname, '../client/build')));

// Handle GET requests to /api route
app.get("/api", (req, res) => {
  res.json({ message: "Hello from server!" });
});

// All other GET requests not handled before will return our React app
app.get('*', (req, res) => {
  res.sendFile(path.resolve(__dirname, '../client/build', 'index.html'));
});

Install Heroku CLI
$ npm i -g heroku

heroku login

$ heroku git:clone -a chonas-react-app
$ cd chonas-react-app

$ git add .
$ git commit -am "make it better"
$ git push heroku master

Add to GitHub
$ git remote add origin https://github.com/AikonaZA/my-react-app.git
$ git branch -M main
$ git push -u origin main