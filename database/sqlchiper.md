# sqlcipher

Instalasi ekstensi ini sangat mudah yaitu jika anda berada dalam lingkungan Linux

    $ sudo apt-get install libsqlcipher-dev

Kemudian kompilasi ulang node-sqlite3 dengan perintah berikut ini

    $ npm install sqlite3 --build-from-source --sqlite_libname=sqlcipher \
    --sqlite=/usr/

Untuk menggunakan fitur enkripsi ini peru ditambahkan beberapa baris kode berikut pada aplikasi node-sqlite3.

    //encrypt database
    db.run('PRAGMA key="passwordmu!"');


Pada contoh CRUD node-sqlite3 pada bagian sebelumnya kode diatas bisa dituliskan sebelum operasi CRUD atau pada saat inisialisasi.

```
...
// Run SQL one at a time
db.serialize(function() {

    //encrypt database
    db.run('PRAGMA key="passwordmu!"');

	// Create table
    db.run(CREATE_TABLE, function(err) {
        if (err) {
            console.log(err);
        } else {
            console.log('CREATE TABLE');
        }
    });
...

```
Bandingkan jika SQLite  tidak memakai enkripsi, anda bisa menggunakan SQLite Browser atau tool `hexdump` pada Linux

![node-sqlite3-no-enkripsi](https://raw.githubusercontent.com/junwatu/pengenalan-nodejs-gitbook/master/images/node-sqlite3-no-enkripsi.png)

dan jika SQLite memakai enkripsi bisa dilihat dari screenshot dibawah ini bahwa isi dari database menjadi "meaningless".

![node-sqlite3-enkripsi](https://raw.githubusercontent.com/junwatu/pengenalan-nodejs-gitbook/master/images/node-sqlite3-enkripsi.png)



