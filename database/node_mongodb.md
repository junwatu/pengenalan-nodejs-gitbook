#Driver Node MongoDB

MongoDB menyediakan driver resmi untuk platform Node.js. Module npm ini tersedia di link berikut https://www.npmjs.com/package/mongodb dan dapat dengan mudah di install melalui `npm`


    $ npm install --save mongodb


Penulis mengasumsikan bahwa MongoDB sudah terinstal pada sistem. Untuk memulai koneksi adalah sangat mudah seperti script dibawah ini

> app.js

```
var MongoClient = require('mongodb').MongoClient; 
var MONGODB_URL = 'mongodb://localhost:27017/sample';

MongoClient.connect(MONGODB_URL, function(err, db){
    err ? console.log(err): console.log('Koneksi ke MongoDB Ok!');
    db.close();
});

```