# Node Sqlite3

Komunitas node menyediakan banyak solusi untuk memakai SQLite di platform Node.js. Salah satu yang paling populer adalah modul [`node-sqlite3`](https://github.com/mapbox/node-sqlite3).

## Instal

node `sqlite3` merupakan binding modul JavaScript yang asinkron untuk database sqlite3.

Untuk penginstalan modul ini ketik perintah berikut

```text
$ npm install sqlite3 --save
```

## CRUD

Operasi database seperti **Create**, **Read**, **Update** dan **Delete** untuk database SQLite sangat mudah seperti pada contoh berikut

`app.js`

```text
/**
 * Akses SQLite 3
 */
var sqlite = require('sqlite3').verbose();
var file = 'film.db';
var db = new sqlite.Database(file);
var fs = require('fs');

// Sample Data
var film = {
    judul: "Keramat",
    release: "2009",
    imdb: "http://www.imdb.com/title/tt1495818/",
    deskripsi: "Film horror paling horror!"
}

var filmUpdate = {
    id: 1,
    deskripsi: "Best Indonesian Horror Movie."
}

// SQL Statement
var CREATE_TABLE = "CREATE TABLE IF NOT EXISTS fdb ( id INTEGER PRIMARY KEY AUTOINCREMENT, judul TEXT NOT NULL, release TEXT NOT NULL, imdb TEXT, deskripsi TEXT )";
var INSERT_DATA = "INSERT INTO fdb (judul, release, imdb, deskripsi) VALUES (?, ?, ?, ?)";
var SELECT_DATA = "SELECT * FROM fdb";
var UPDATE_DATA = "UPDATE fdb SET deskripsi=$deskripsi WHERE id=$id";

// Run SQL one at a time
db.serialize(function() {
    // Create table
    db.run(CREATE_TABLE, function(err) {
        if (err) {
            console.log(err);
        } else {
            console.log('CREATE TABLE');
        }
    });

    // Insert data with sample data
    db.run(INSERT_DATA, [film.judul, film.release, film.imdb, film.deskripsi], function(err) {
        if (err) {
            console.log(err);
        } else {
            console.log('INSERT DATA');
        }
    });

    // Query all data
    selectAllData();

    // Update data
    db.run(UPDATE_DATA, {$deskripsi: filmUpdate.deskripsi, $id: filmUpdate.id}, function(err){
        if(err) {
            console.log(err);
        } else {
            console.log('UDATE DATA');
        }
    });

    selectAllData();

    db.run('DELETE FROM fdb WHERE id=$id', {$id:1}, function(err){
        if(err) {
            console.log(err)
        } else {
            console.log("DELETE DATA");
        };

    })

});

function selectAllData() {
    db.each(SELECT_DATA, function(err, rows) {
        if (!err) {
            console.log(rows);
        }
    })
}
```

Aplikasi diatas akan membuat tabel `fdb`, memasukkan data baru kemudian data tersebut akan di update dan terakhir akan dihapus.

Contoh diatas memakai API berikut ini

`db.serialize()`

`db.run(operasi_sqlite, callback)`

Dengan memakai fungsi `db.serialize()` maka eksekusi sql akan di eksekusi secara serial atau berurutan dan operasi SQL apa saja bisa di eksekusi oleh node-sqlite3 dengan memakai metode `db.run()` tersebut.

Penjelasan API lebih lanjut untuk Node SQLite bisa dilihat pada link berikut

[https://github.com/mapbox/node-sqlite3/wiki/API](https://github.com/mapbox/node-sqlite3/wiki/API).

