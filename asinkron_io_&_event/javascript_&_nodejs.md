# Javascript & Node.js

Kembali ke Javascript!. Untuk mengetahui apa yang dimaksud dengan pemrograman asinkron bisa lebih mudah dengan memakai pendekatan contoh kode. Perhatikan kode Javascript pada Node.js berikut


```
var fs = require('fs');

fs.readFile('./resource.json',function(err, data){
	if(err) throw err;
	console.log(JSON.parse(data));
});

console.log('Selanjutnya...');

```

fungsi `readFile()` akan membaca membaca isi dari file `resource.json` secara asinkron yang artinya  proses eksekusi program tidak akan menunggu pembacaan file `resource.json` sampai selesai tetapi program akan tetap menjalankan kode Javascript selanjutnya yaitu `console.log('Selanjutnya...')`. Sekarng lihat apa yang terjadi jika kode javascript diatas dijalankan


![belajar-asinkron-nodejs](https://raw.github.com/idjs/belajar-nodejs/gh-pages/images/belajar-asinkron-nodejs.png)


Jika proses pembacaan file `resource.json` selesai maka fungsi callback pada `readFile()` akan di jalankan dan hasilnya akan ditampilkan pada console. Yah, fungsi callback merupakan konsep yang penting dalam proses I/O yang asinkron karena melalui fungsi callback ini data data yang dikembalikan oleh proses I/O akan di proses.

Lalu bagaimana platform Node.js mengetahui kalau suatu proses itu telah selesai atau tidak ?...jawabannya adalah [Event Loop](http://en.wikipedia.org/wiki/Event_loop). Event - event yang terjadi karena proses asinkron seperti pada fungsi `fs.readFile()` akan ditangani oleh yang namanya Event Loop ini.

Campuran teknologi antara event driven dan proses asinkron ini memungkinkan pembuatan aplikasi dengan penggunaan data secara masif dan real-time. Sifat komunikasi Node.js I/O yang ringan dan bisa menangani user secara bersamaan dalam jumlah relatif besar tetapi tetap menjaga state dari koneksi supaya tetap terbuka dan dengan penggunaan memori yang cukup kecil memungkinkan pengembangan aplikasi dengan penggunaan data yang besar dan kolaboratif...Yeah, Node.js FTW! :metal:


