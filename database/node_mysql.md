# Node MySQL

Implementasi driver dari MySQL untuk platform Node.jssudah sangat mature seperti modul **node-mysql** di https://github.com/felixge/node-mysql/


##Instalasi

Seperti biasa untuk menginstall modul ini dan secara otomatis menyimpan nama & versi modul di file `package.json` yaitu dengan memakai perintah berikut


    $ npm install --save mysql


##Koneksi Sederhana

Untuk membuat koneksi ke database MySQL salah satu caranya adalah dengan menggunakan metode `connection.connect()`


    //app.js
    var mysql = require('mysql');
    
    /**
    * Setting opsi dari connection, 
    * lihat https://github.com/felixge/node-mysql/
    */
    var connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: ''
    });
    
    //Membuka koneksi ke database MySQL
    connection.connect(function(err){
        if(err) {
            console.log(err);
        } else {
            console.log('Koneksi dengan id '+ connection.threadId);
        }
    });
    
    // Query bisa dilakukan di sini

    //Menutup koneksi
    connection.end(function(err){
       if(err) {
           console.log(err);
        } else {
           console.log('koneksi ditutup!');
       }
    });

    
##Query

Istilah `query` mungkin menurut mindset umum artinya adalah mengambil data dari database tetapi dalam modul node-mysql ini untuk membuat database atau schema juga didefiniskan sebagai `query`. Ada beberapa bentuk fungsi untuk wrapper `query` ini yang pertama adalah

**`connection.query(sqlString, callback)`** 

Dengan memakai statemen SQL kita bisa membuat schema database **ebook** seperti berikut
   
    var create_db = 'CREATE DATABASE IF NOT EXISTS ebook'
    
    connection.query(create_db, function(err, result){
        if(err){
          console.log(err);
        } else {
          console.log(result);
        }
    )
    
    
Dan bentuk kedua yaitu

**`connection.query(sqlString, value, callback)`** 


Misalnya untuk menyimpan data semua judul buku pada database **ebook**

    var ebook = {
        id: 1,
        title: 'Wiro Sableng Pendekar Kapak Maut Naga Geni 212 : Batu Tujuh Warna',
        pengarang: 'Bastian Tito'
    }
    
    var insert_sql = 'INSERT INTO ebook SET ?';
    
    connection.query(insert_sql, ebook, function(err, result){
        err ? console.log(err): console.log(result);
    })
    
Kalau dibutuhkan `escaping` value sebelum dimasukkan ke database MySQL bisa memakai metode `.escape()` atau pake placeholder `?`.

    var ebook = {
        id: 1,
        title: 'Wiro Sableng Pendekar Kapak Maut Naga Geni 212 : Batu Tujuh Warna',
        pengarang: 'Bastian Tito'
    }
    
    var insert_sql = 'UPDATE ebook SET title = ? WHERE id = ?';
    
    connection.query(insert_sql, [ebook.title, ebook.id], function(err, result){
        err ? console.log(err): console.log(result);
    })
    

**`connection.query(options, callback)`** 

// todo

Dengan metode `query` ini kita bisa memakai statemen SQL yang biasa dipakai untuk query data di MySQL, jadi penggunaan dari modul npm ini sebenarnya cukuplah mudah.

Untuk contoh aplikasi yang memanfaatkan database ini bisa dilihat pada bab **Converter Gambar Ke Data URI**.

