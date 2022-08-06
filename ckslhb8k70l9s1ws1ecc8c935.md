## Setup Mongo Database and insert noSQL data with JavaScript

In below steps we are going to install mongo database locally and insert some data via command line and also javascript script.

- Install Mongo via this link
    - https://docs.mongodb.com/manual/administration/install-community/
    - Install the extra mongoDB compass

- Create a new directory
```
mkdir mongo
```

- Start up mongo database into directory your using for mongo eg.
```
"C:\Program Files\MongoDB\Server\5.0\bin\mongod.exe" --dbpath="<YOUR_DIRECTORY>\mongo"
```

Mongo is running now. Now we are going to add some data via command line

- Install mongosh
   - https://docs.mongodb.com/mongodb-shell/install/#std-label-mdb-shell-install

- Open command line
```
mongosh
```

- See all your current dbs by running
```
show dbs
```

- Create a new db
```
use newTestDB
```

- Create a new collection
```
Insert a new document in the notes including (name, description)
db.notes.insert({name: "Az", description: 205})
```

Now we are going to create collection and insert data via some JavaScript 

- Install node js if you havent already https://nodejs.org/en/

- Create a new directory for your JavaScript files
```
mkdir mongo
```

- In your project directory install 
```
npm install mongoose --save
```

- Add a JS file and add below
- This creates new collection called anotherTest and adds some data to it

```
// Insert into anotherTest db
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/anotherTest', {useNewUrlParser: true, useUnifiedTopology: true});

const db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  // we're connected!
  console.log("connected")
});

const personSchema = new mongoose.Schema({
  name: String
});

const Kitten = mongoose.model('Person', personSchema);

const Person = new Kitten({ name: 'Az' });

Person.save(function (err, Person) {
  if (err) return console.error(err);
});

```

- Run your script by running
```
node <YOUR_JS_FILE>
```

- Confirm by looking up your data in MongoDB Compass as below

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628794882446/NB5e1JjFX.png)


References:
- https://docs.mongodb.com/mongodb-shell/install/
- https://docs.mongodb.com/manual/crud/
- https://mongoosejs.com/docs/index.html
- https://www.mongodb.com/

Hope this solution worked for you!
If this didn't please comment and I will try to help you.
Remember to like, comment and share
Happy Coding,
Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]

%%[amazonads]