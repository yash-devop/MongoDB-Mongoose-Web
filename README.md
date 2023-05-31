# MongoDB-Mongoose-Web
I created this repo , just to save my Mongodb initial starter codes , so that it will be easy for me to access it whenever i feel that i forgot the syntax or want to refer to the code once.

# folder structure :  MVC structure
``` 
M=> Model
V=>Views
C=>Controller

```

```
1) Model=> contains the database model / Schema
2) Routes => Contains the Routes like GET,POST,PUT....
3) Controller => contains the logic of the project like create the moviePosts or how to get the posts.
```

# Starter Code :

Code : 
```
require('dotenv').config();
const express = require("express");
const app = express();

const mongoose = require('mongoose')
app.use(express.json());  //Middleware : to allow the json res.


// Database Connectivity:

mongoose.connect(process.env.MONGO_DB_URL,{
    useCreateIndex : true,
    useNewUrlParser : true,
    useUnifiedTopology: true,
}).then(()=>console.log("Database Connected Successfully "))
.catch((err)=>console.log(err))

app.listen(process.env.PORT || 5000 ,()=>{
    console.log("Server Connected Successfully.");
});
```

# Models folder :
I have created a file inside this folder called ```Mens.js``` where the Mens runners list are store.
![image](https://github.com/yash-devop/MongoDB-Mongoose-Web/assets/112558970/b02b5df8-3d1b-4e96-b68c-c1ca2077d14d)

code : 
```
const mongoose = require('mongoose')

const MenSchema = new mongoose.Schema({
    ranking : {
        type: Number,
        require: true, // this ranking field is REQUIRED ,else ERROR. 
        unique:true  // unique !
    },
    name : {
        type: String,
        require: true,
        trim:true  // means it will trim the SPACES
    },
    dob : {
        type: Date,
        require: true,
        trim:true 
    },
    country : {
        type: String,
        require: true,
        trim:true  
    },
    score : {
        type: Number,
        require: true,
        trim:true 
    },
    event : {
        type: String,
        default: "100m" // means byDefault set to 100 Meter if not provided the value.
    },
});

// we are creating a new Collection.
const MensRanking = new mongoose.model('MenRanking',MenSchema)
```

module.exports = MensRanking

![image](https://github.com/yash-devop/MongoDB-Mongoose-Web/assets/112558970/8d6346c8-c72c-49a6-a7bd-0f1771a2e3be)
![image](https://github.com/yash-devop/MongoDB-Mongoose-Web/assets/112558970/6ccfe1b0-d04a-4c12-bdcf-6fd08329d51a)


Now , Lets Configure the ```Router Folder```


Code : ```Mens.js```
```
const Router = require('express').Router();
const MensRankingModel = require('../Models/Mens');

Router.post('/', async(req,res)=>{
    try {
        const mensRecord = new MensRankingModel(req.body);
        const docResponse = await mensRecord.save();
        console.log(res.body);
        res.json(docResponse)
    } catch (error) {
        console.log(error)
        res.status(400).json(error)
    }
})

module.exports = Router;
```
