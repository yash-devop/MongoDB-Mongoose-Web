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

Models Folder : 

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

<!-- ![image](https://github.com/yash-devop/MongoDB-Mongoose-Web/assets/112558970/3b344347-f1e9-41b7-bd19-915d749c658c) -->
![image](https://github.com/yash-devop/MongoDB-Mongoose-Web/assets/112558970/8473885c-9ebb-475e-902c-232e9c88deb3)

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

So we have to make some changes to our ```Index.js``` file : so,

![image](https://github.com/yash-devop/MongoDB-Mongoose-Web/assets/112558970/d371be4d-6bac-49d6-a395-3f6a8e05ffe9)

Code :
```
require('dotenv').config();
const express = require("express");
const app = express();
const mensRoute = require('./Routers/Mens.js')
app.use(express.json());  //Middleware : to allow the json res.


const mongoose = require('mongoose');
// Database Connectivity:

mongoose.connect(process.env.MONGO_DB_URL,{
    useNewUrlParser : true,
    useUnifiedTopology: true,
}).then(()=>console.log("Database Connected Successfully "))
.catch((err)=>console.log(err))

// using the Router from Routers folder.
app.use('/mens',mensRoute);
 
app.listen(3000 ,()=>{
    console.log("Server Connected Successfully.");
});
```

Testing the REST API using Postman tool : 

![image](https://github.com/yash-devop/MongoDB-Mongoose-Web/assets/112558970/fe0cc9ab-c4a3-4eab-8008-0408fb4b42ac)

# IMPORTANT :  ![image](https://github.com/yash-devop/MongoDB-Mongoose-Web/assets/112558970/b436db7f-4387-4651-b128-a8125c810e97)

```(Note: the data should match the fields we have created in our schema. Fields can be also be 1 or 2 but should not more than the Defined Model schema.)```
![image](https://github.com/yash-devop/MongoDB-Mongoose-Web/assets/112558970/8c6ec57c-af1e-45ab-8ee9-1c2212b5a3f7)

RESPONSE :

![image](https://github.com/yash-devop/MongoDB-Mongoose-Web/assets/112558970/31c43651-57f2-488f-a7a2-6458085ea699)
