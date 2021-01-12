# Penggunaan

Untuk kode sumber selengkapnya bisa di lihat di [Github](https://github.com/junwatu/todatauri) pada branch `todatauri-mysql` atau ketik perintah berikut pada command line.

```text
$ git clone -b todatauri-mysql https://github.com/junwatu/todatauri todatauri-mysql

$ cd todatauri-mysql

$ npm install
```

Ada tiga penggunaan aplikasi ini yaitu

## Download PNG & Simpan Ke MySQL

```text
$ node ./tdi.js <url_image_png_dari_internet>
```

Aplikasi ini akan mendownload file image png dari internet dan mendukung protokol `http` ataupun `https`.

## Demo

```text
$ node ./tdi.js
```

Jika dijalankan tanpa argumen maka hasilnya adalah keluaran demo yang tidak lain adalah contoh format Data URI.

## Tampilkan Data MySQL

```text
$ node ./tdi.js show
```

Jika ada argumen `show` maka data dalam MySQL akan ditampilkan semua. Hati hati jika anda banyak mengkonversi banyak data gambar png.

