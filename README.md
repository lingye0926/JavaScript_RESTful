# npm command
npm init -y: to initiallize the project
npm i express ejs mongoose : to add package to the project

## routine to setup a server

const express = require("express");
const bodyParser = require("body-parser");
const ejs = require("ejs");
const mongoose = require("mongoose");

const app = express();

app.set("view engine","ejs");

app.use(bodyParser.urlencoded({
    extended:true
}));

app.use(express.static("public"));

mongoose.connect("mongodb://localhost:27017/wikiDB")

const articleSchema = {
    title: String,
    content: String
};

const Article = mongoose.model("Article",articleSchema);
//TODO

app.listen(3000,function(){
    console.log("Server started on port 3000");
});
### check port status on terminal
lsof -i tcp:3000
### make sure you open mongo service before start the connection use nodemon 
brew services start mongodb-community

## RESTful
### read data from mongoDB


### use express route parameters to captrue values as part of request route query string
app.route("/articles/:articleTitle")//this articleTitle will be call by eq.params.articleTitle
.get(function(req,res){  
    Article.findOne({title:req.params.articleTitle},function(err,foundArticle){
        if(foundArticle){
            res.send(foundArticle);
        }else{
            res.send("No article match the title.");
        }
    })
})