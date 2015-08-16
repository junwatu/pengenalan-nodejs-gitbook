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


MongoDB akan membuat database jika database tersebut tidak ada, seperti halnya dengan database `sample` pada kode diatas. Bentuk URI untuk koneksi ke MongoDB adalah seperti ini


```
mongodb://<username>:<password>@<localhost>:<port>/<database>

```


Jalankan apikasi dan jika tidak ada masalah maka pesan bahwa koneksi sukses ke MongoDB akan muncul pada terminal.

    $ node app.js
    Koneksi ke MongoDB Ok!


Berikutnya akan kita lakukan operasi dasar untuk MongoDB yaitu CRUD tapi sebelumnya kita buat *schema*  dahulu.

> person.js

```

function PersonSchema(data) {
    this.nama = data.nama;
    this.email = data.email;
    this.username = data.username;          
};

module.exports = PersonSchema;


```

*Schema* diatas merupakan model data sederhana berupa object JavaScript. 