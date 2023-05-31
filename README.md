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
![image](https://github.com/yash-devop/MongoDB-Mongoose-Web/assets/112558970/cf88a07f-0f55-4e65-afe0-afa736d80f01)

code : 
```
const mongoose = require('mongoose')

const MenSchema = new mongoose.connect({
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
