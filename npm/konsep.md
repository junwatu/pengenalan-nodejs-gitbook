# Paket npm

Secara default data paket npm disimpan di registry npmjs.org. Sehingga untuk menginstall paket npm tertentu anda bisa mencari paket ini melalui command `npm` atau langsung melalui website.

Sejak versi Node.js 0.6.3 command `npm` sudah ter-bundle dengan installer Node.js. Untuk menginstall modul npm yang anda butuhkan ketik misalnya

```
npm install express

```

perintah diatas akan mendownload paket `express` dari `http://npmjs.org` dan secara otomatis akan membuat directory `node_modules`.

Untuk memakai modul `express` ini cukup dengan membuat file JavaScript baru di luar direktori `node_modules` dan load modul dengan keyword `require`.


```
var app = require('express');

// kode lainnya

```

##Membuat Paket npm

Sebelum membuat paket npm pastikan fungsionalitas yang anda cari tidak ada dalam registry npm. Caranya yaitu anda bisa menggunakan perintah

    npm search

atau dengan memakai website berikut [npmjs.org](http://npmjs.org), [node-modules.com](http://node-modules.com) atau [npmsearch.com](http://npmsearch.com)

Untuk membuat paket npm caranya cukup mudah. Berikut alur umum untuk membuat paket npm untuk di publish ke registry `npmjs.org`.



![alur pembuatan npm](/images/npm-flow.png)

Secara garis besar proses pembuatan paket npm menurut alur diatas akan dijelaskan sebagai berikut

###Registrasi

Sebelum publish ke registry npmjs.org kita harus registrasi dulu melalui perintah berikut

    npm adduser


###Buat Project

Untuk membuat project baru dari nol langkah pertama adalah membuat direktori

    mkdir npmproject

Kemudian inisialisasi project tersebut

    npm init

perintah diatas akan membuat file `package.json` yang isinya adalah info dan dependensi project. Ikuti saja tiap pertanyaan dan isi informasi sesuai dengan paket yang ingin anda buat.

Contohnya pada paket `svh` berikut ini

`package.json`

```
{
  "name": "svh",
  "version": "0.0.7-beta",
  "author": "Equan Pr.",
  "description": "Simple file server for html-javascript web client app development",
  "keywords": [
    "process",
    "reload",
    "watch",
    "development",
    "restart",
    "server",
    "monitor",
    "auto",
    "static",
    "nodemon"
  ],
  "homepage": "https://github.com/junwatu/svh",
  "bugs": "https://github.com/junwatu/svh/issues",
  "main": "./lib/core.js",
  "scripts": {
    "test": "./node_modules/mocha/bin/mocha"
  },
  "dependencies": {
    "async": "~0.2.9",
    "chalk": "0.2.x",
    "cheerio": "0.12.x",
    "commander": "2.0.x",
    "compression": "^1.0.2",
    "concat-stream": "1.0.x",
    "express": "4.x",
    "morgan": "^1.1.1",
    "send": "^0.3.0",
    "watch": "0.8.x",
    "wordgenerator": "0.0.1"
  },
  "devDependencies": {
    "gulp": "^3.5.6",
    "gulp-uglifyjs": "^0.3.0",
    "gulp-util": "2.2.14",
    "mocha": "1.13.x",
    "supertest": "0.8.x"
  },
  "repository": {
    "type": "git",
    "url": "http://github.com/junwatu/svh.git"
  },
  "bin": {
    "svh": "./bin/svh"
  },
  "license": "MIT"
}
```

###Publish Lokal

Sebelum di publish pastikan paket anda bisa berjalan atau digunakan pada komputer lokal. Perintah berikut akan menginstall paket anda secara global di komputer.

    npm publish . -g


atau jika diinginkan link simbolik bisa memakai perintah npm berikut

    npm link



###Publish Publik

    npm publish


Untuk lebih jelasnya silahkan kunjungi dokumentasi untuk [developer npm](https://www.npmjs.org/doc/misc/npm-developers.html).









