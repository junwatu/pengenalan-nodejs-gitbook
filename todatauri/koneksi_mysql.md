# Koneksi MySQL


```
/**
 * Sample use todatauri.js with Mysql
 */
var Util = require('./todatauri.js');
var mysql = require('mysql');

var connection = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: ''
});

connection.connect(function (err) {
    if (err) {
        console.log(err);
    } else {
        console.log('Koneksi MySQL dengan id ' + connection.threadId);
    }
});

var create_database = 'CREATE DATABASE IF NOT EXISTS data_uri ';
var create_table = "CREATE TABLE IF NOT EXISTS data_uri.images (id INT AUTO_INCREMENT PRIMARY KEY, data TEXT)";

connection.query(create_database, function (err, res) {
    if (err) {
        console.log(err);
    } else {
        console.log('Create database data_uri [ok]');

        connection.query(create_table, function (err, result) {
            if (err) {
                console.error(err);
            } else {
                console.log('Create table images [ok]');
                main(process);
            }
        })
    }
});

function insertData(data, connection) {
    connection.query('INSERT INTO data_uri.images SET ?', { data: data }, function (err, res) {
        (err) ? console.log(err) : console.log(res);
    })
};

function showData(connection) {
    connection.query('SELECT * FROM data_uri.images', function(err, result){
        if(err) {
            console.log(err);
        } else {
            console.log('\n\nMySQL Database\n============================\n');
            result.forEach(function(element, index){
                
                console.log('id \u2192', element.id);
                console.log('image \u2192', element.data);
            })
        } 
    })
}

function main(process) {
    if (process.argv[2]) {
        if (process.argv[2].toLowerCase().trim() == 'show') {
          showData(connection);
        } else {
            Util.toDataURI(process.argv[2], function (err, data) {
                if (!err) {
                    insertData(data, connection);
                }
            })
        }
    } else {
        Util.toDataURI(null, function (err, data) {
            if (!err) {
                console.log(data);
            }
        });
    }
}

```