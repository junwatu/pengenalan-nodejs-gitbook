#Automasi

Dalam prakteknya biasanya testing ini dilakukan secara otomatis misalnya jika anda memakai Github dalam pengembangan perangkat lunak open source maka anda bisa memakai server **Travis** yang dengan setting konfigurasi tertentu akan menjalankan pengetesan jika anda menge-*push* kode ke repository Github atau anda bisa memakai *build server* yang ada diluaran seperti **Jenkins**, **Bamboo**, **TeamCity** dll.

##Travis

Jika anda memakai Github dan menggunanakan Travis maka secara default server travis ini akan menjalankan command

    $ npm test

sehingga dalam package.json yang anda push ke Github anda perlu menulis script untuk pengetesan misalnya jika memakai Mocha 

```
"scripts": {
	"test": "mocha"
}

```

###.travis.yml
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

Kemudian anda perlu mengatur konfigurasi repo di Github ([Testing Learn](https://github.com/junwatu/testing-learn)). Supaya Github bisa memakai service dari Travis maka anda perlu meengubah konfigurasi repo (Masuk ke menu **Settings**)

![](/images/github-service.png)

###Enable Build

Supaya build selalu dijalankan oleh Travis maka anda harus meng-**ON**-kan tombol enable di [travis-ci.org](https://travis-ci.org) pada repo yang anda inginkan. 

![](/images/enable.png)

###Test Build

Build akan dijalankan oleh Travis setiap ada kode baru di Github atau anda bisa menggunakan tombol **Test Service** pada **Settings** -> **Webhooks & services** untuk **force build**. 

![](/images/testing-ci.png)

###Notifikasi

Notifikasi Travis bisa di integrasikan dengan Slack, Email, dll atau biasanya dengan gambar status di README repo. Untuk konfigurasi gambar status klik tombol **Build/Passing** di sebelah nama repo di Travis dan *copy paste* ke README repo di Github. 

![](/images/image-build.png)

Sehingga jika anda membuka repo di Github maka akan muncul gambar status yang apakah build sukses atau dalam status error.

![](/images/notif.png)

