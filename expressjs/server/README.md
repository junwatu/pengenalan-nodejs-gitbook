# Server File

Sebelumnya bikin project kecil dengan mengetikkan perintah berikut pada direktori project

```text
$ npm init
```

dan berikan nama project sebagai `server-file-statik`. Direktori project dari server file bisa dilihat pada sususan tree dibawah ini.

> Susunan file dan direktori

```text


    server-file-statis
    ├── package.json
    ├── app.js
    ├── node_modules
    └── publik
        ├── index.html

```

Dengan adanya npm instalasi ExpressJS sangat mudah, ketik perintah berikut pada direktori project.

```text
$ npm install express --save
```

> Catatan :
>
> Perintah diatas akan menginstall ExpressJS dengan versi yang paling terbaru \(pada saat buku ini ditulis versi terbaru adalah 4.x\). Jika membutuhkan versi tertentu cukup dengan menambahkan '@' dan nomer versi yang akan di inginkan seperti contoh berikut
>
> ```text
>   $ npm install express@3  --save
> ```

Untuk kedepannya bahasan mengenai ExpressJS ini akan memakai versi 4.x.

## Kode

Jika anda ingat server file yang memakai modul http pada bab sebelumnya berikut merupakan versi yang memakai ExpressJS

> app.js

```text
'use strict';

var express = require('express');
var server = express();
var logger = require('morgan');

server.use(logger('dev'));

server.use(express.static(__dirname+'/publik'));

server.listen(4000, function(){
    console.log('Server file sudah berjalan bos!');
});
```

Seperti yang dijelaskan pada bab sebelumnya untuk memakai module Node.js di gunakan keyword `require`.

Modul `express` akan menangani tiap request dari user dan kemudian akan memberikan response berupa file yang diinginkan. Pada kode diatas file yang akan diberikan ke pengguna disimpan pada folder `publik`.

