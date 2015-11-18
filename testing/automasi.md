#Automasi

Dalam prakteknya biasanya testing ini dilakukan secara otomatis misalnya jika anda memakai Github dalam pengembangan perangkat lunak open source maka anda bisa memakai server **Travis** yang dengan setting konfigurasi tertentu akan menjalankan pengetesan jika anda menge-*push* kode ke repository Github atau anda bisa memakai *build server* yang ada diluaran seperti **Jenkins**, **Bamboo**, **TeamCity** dll.

##Travis

Jika anda memakai Github dan menggunanakan Travis maka secara default server travis ini akan menjalankan command

    $ npm test

sehingga dalam package.json yang anda push ke Github anda perlu menulis script untuk pengetesan misalnya kalau memakai Mocha 

```
"scripts": {
	"test": "mocha"
}

```

Untuk setting Travis anda cukup membuat file **.travis.yml** pada folder projek misalnya seperti dibawah ini (contoh source code projek test ada di [sini](https://github.com/junwatu/testing-learn))

```
.
├── app.js
├── .travis.yml
├── node_modules
├── package.json
└── test
    └── app.test.js

```

Dengan isi file tersebut adalah versi dari Node.js dimana test akan dijalankan. Misalnya untuk menjalankan pengetesan Node.js versi 4.1 dan 4.0

```
language: node_js
node_js:
  - "4.1"
  - "4.0"
```

