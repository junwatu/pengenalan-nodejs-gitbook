# Middleware

Fungsionalitas yang diberikan oleh ExpressJS di bantu oleh yang namanya `middleware` yaitu fungsi asinkron yang bisa mengubah request dan respon di server.

Pada kode diatas contoh middleware yaitu modul `morgan`. Cara pemakaian `middleware` yaitu melalui `app.use()`.

Module `morgan` merupakan modul untuk logger yang berfungsi untuk pencatatan tiap request ke server. Pencatatan ini atau istilahnya `logging` akan ditunjukkan di console terminal.

Untuk menginstall modul ini ketik perintah berikut

    $ npm install morgan --save

Middleware middleware ini bisa anda lihat di link berikut

https://github.com/senchalabs/connect#middleware
