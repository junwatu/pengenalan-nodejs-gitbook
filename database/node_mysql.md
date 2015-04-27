# Node MySQL

Implementasi driver dari MySQL sudah sangat mature seperti modul node di https://github.com/felixge/node-mysql/


##Instalasi

Seperti biasa untuk menginstall modul npm dan otomatis menyimpan versi modul di file `package.json`


    $ npm install --save mysql


##Koneksi Sederhana

Untuk membuat koneksi ke database MySQL aalah satu caranya adalah dengan menggunakan metode `connection.connect()`


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
    
    // Query

    //Tutup koneksi
    connection.end(function(err){
       if(err) {
           console.log(err);
        } else {
           console.log('koneksi ditutup!');
       }
    });

    
##Query

Mungkin istilah `query` menurut mindset kita adalah mengambil data dari database tetapi dalam modul node-mysql untuk membuat database atau schema juga melalui query di metode `connection.query()`. 

Untuk membuat schema database pakailah SQL statement seperti biasa dipakai di MySQL CLI. 
   
    var create_db = 'CREATE DATABASE IF NOT EXISTS node_mysql_test'
    
    connection.query(create_db, function(err, result){
        if(err){
          console.log(err);
        } else {
          console.log(result);
        }
    )
    
    
Intinya adalah dengan metode ini kita bisa memakai statemen SQL yang biasa dipakai untuk query data di MySQL jadi penggunaan modul npm ini cukuplah mudah.
    