# Node MySQL

Implementasi driver dari MySQL sudah sangat mature seperti modul node di https://github.com/felixge/node-mysql/


##Instalasi

Seperti biasa untuk menginstall modul npm dan otomatis menyimpan versi modul di file `package.json`


    $ npm install --save mysql


##Koneksi Sederhana

Untuk membuat koneksi ke database MySQL pake metode `connection.connect()`


    //app.js
    var mysql = require('mysql');

    var connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: ''
    });

    //Buka koneksi ke database MySQL
    connection.connect(function(err){
        if(err) {
            console.log(err);
        } else {
            console.log('Koneksi dengan id '+ connection.threadId);
        }
    });

    //Tutup koneksi
    connection.end(function(err){
       if(err) {
           console.log(err);
        } else {
           console.log('koneksi ditutup!');
       }
    });

    