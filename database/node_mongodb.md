#Node MongoDB

MongoDB menyediakan driver resmi untuk platform Node.js. Module npm ini tersedia di link berikut https://www.npmjs.com/package/mongodb dan dapat dengan mudah di install melalui `npm`


    $ npm install --save mongodb


Penulis mengasumsikan bahwa MongoDB sudah terinstal dan berjalan pada sistem. Untuk memulai koneksi dapat dengan mudah dilakukan seperti script berikut ini,

> app.js

```
var MongoClient = require('mongodb').MongoClient; 
var MONGODB_URL = 'mongodb://localhost:27017/sample';

MongoClient.connect(MONGODB_URL, function(err, db){
    err ? console.log(err): console.log('Koneksi ke MongoDB Ok!');
    db.close();
});

```


MongoDB akan membuat database baru jika database tersebut tidak ada, seperti halnya dengan database `sample` pada kode diatas karena sebelumnya database ini tidak ada maka secara otomatis MongoDB akan membuatnya. Bentuk umum URI untuk koneksi ke MongoDB adalah seperti berikut


```
mongodb://<username>:<password>@<localhost>:<port>/<database>

```


Jalankan apikasi di terminal dan jika tidak ada masalah maka akan muncul pesan pada konsol bahwa koneksi ke MongoDB telah sukses.


    $ node app.js
    Koneksi ke MongoDB Ok!


Berikutnya akan kita lakukan operasi dasar untuk MongoDB yaitu CRUD tapi sebelumnya kita buat *schema*  terlebih dahulu.

> person.js

```

function PersonSchema(data) {
    this.nama = data.nama;
    this.email = data.email;
    this.username = data.username;          
};

module.exports = PersonSchema;


```

*Schema* diatas merupakan model data sederhana yang dituliskan dalam object JavaScript dan tanpa *built-in type casting* ataupun fitur validasi. Jika anda membutuhkan pemodelan data yang lebih handal dan lebih baik, maka pakailah pustaka ODM (Object-Document Modeler) seperti [Mongoose](http://mongoosejs.com/).


Driver Node MongoDB menyediakan API yang lengkap untuk bekerja dengan database ini. Silahkan lihat link berikut untuk melihat lebih lengkap tentang API ini

http://mongodb.github.io/node-mongodb-native/2.0/api/Collection.html#insert


##Insert 

Untuk memasukkan dokumen bisa memakai metode [insertOne()](http://mongodb.github.io/node-mongodb-native/2.0/api/Collection.html#insertOne) untuk memasukkan satu dokumen


> app.js

```
/**
* Balajar Node - MongoDB
*
*
* MIT
* Equan Pr. 2015
*/

var PersonSchema = require('./person.js');
var MongoClient = require('mongodb').MongoClient;
var MONGODB_URL = 'mongodb://localhost:27017/sample';

var person = new PersonSchema({
    nama: 'Kebo Ijo',
    email: 'kebo@ijo.xyz',
    username: 'obek_rebo'
});

MongoClient.connect(MONGODB_URL, function(err, db){
    err ? console.log(err): console.log('Koneksi ke MongoDB Ok!');
    db.collection('persons').insertOne(person, function(err, result){
        if(err){
           console.log(err);
        } else {
           console.log(result);
        }
        db.close();  
    })
});


```
Secara otomatis operasi insert ini akan menghasilkan *primary key* `_id` yang unik yaitu berupa `ObjectId`. Yang membedakan `_id` ini dengan id pada database yang lain adalah dengan `ObjectId` bisa didapatkan kapan data ini dimasukkan melalui pemakaian metode `getTimestamp()`.

```
$ mongo
MongoDB shell version: 2.6.9
connecting to: test

>  _id = ObjectId()
ObjectId("55d81f48bb934a51424dbd37")

> ObjectId("55d81f48bb934a51424dbd37").getTimestamp();
ISODate("2015-08-22T07:05:44Z")

> 


```


Jika anda mempunyai banyak dokumen, untuk memasukkan dokumen-dokumen tersebut ke collection `persons` anda bisa memakai metode `insertMany()`.


##Update

Operasi update data juga cukup mudah apalagi jika anda sangat pahamn tentang MongoDB. Untuk meng-update data bisa dilakukan melalui metode `updateOne()` atau `updateMany()`.

> app.js

```
var PersonSchema = require('./person.js');
var MongoClient = require('mongodb').MongoClient;
var MONGODB_URL = 'mongodb://localhost:27017/sample';

var person = new PersonSchema({
    nama: 'Kebo Ijo',
    email: 'kebo@ijo.xyz',
    username: 'obek_rebo'
});

MongoClient.connect(MONGODB_URL, function(err, db){
    err ? console.log(err): console.log('Koneksi ke MongoDB Ok!');
    db.collection('persons').insertOne(person, function(err, result){
        if(err){
      	   console.log(err);
        } else {
      	   console.log('Simpan data person ok!');
          
           //update data
           var personUpdate = {
               nama: 'Sukat Tandika'
           }
           db.collection('persons').updateOne({nama: person.nama}, personUpdate, function(err, result){
               if(err) {
                 console.log(err);
               } else {
                 console.log('Data person berhasil dimodifikasi!');
               }
               db.close();
           })
        }
    })
});

```
Metode `updateOne()` mempunyai beberapa argumen seperti berikut

```
updateOne(filter, update, options, callback)

```

Untuk data update anda bisa memakai operator seperti `$set` contohnya seperti berikut ini 


```
db.collection('persons').updateOne({nama: person.nama}, {$set:{nama: 'Angel'}}, function(err, result){
    if(err) {
        console.log(err);
    } else {
        console.log('Data person berhasil dimodifikasi!');
    }
    
    db.close();
})
```

dari beberapa options yang terpenting adalah key `upsert` yaitu* update insert* dan jika option ini diberikan maka jika data yang akan di-update tidak ada maka MongoDB secara otomatis akan membuat data yang baru. Untuk lebih jelasnya anda bisa melihat [dokumentasi dari API `updateOne()`](http://mongodb.github.io/node-mongodb-native/2.0/api/Collection.html#updateOne).


##Query


Query data pada database MongoDB dapat dengan mudah dilakukan dengan memakai metode `find()`, sebagai contoh untuk menemukan data `person` pada collection `persons`

```
MongoClient.connect(MONGODB_URL, function(err, db){
    if(!err){
        findPerson({nama: 'Morbid Angel'}, db, function(err, doc){
            if(!err){
                console.log(doc);
            } else {
                console.log(err);
            }
            db.close();
        });
    } else {
        console.log(err);
    }
});


function findPerson(filter, db, callback){
  var cursor = db.collection('persons').find(filter);
  cursor.each(function(err, docResult){
    if(err){
      callback(err, null);
    } else {
      if(docResult != null) {
        console.log(docResult);
        callback(null, docResult);
      } else {
        callback(null, 'empty!');
      }
    }
  })
}

```

#Delete

