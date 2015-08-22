# Cara Kerja

Cara kerja dari aplikasi Person REST ini cukup mudah. Hanya saja untuk antar muka dengan pengguna tidak melalui antar muka web seperti halnya kita mengakses halaman Facebook misalnya karena secara umum aplikasi REST fungsinta lebih ke memberikan layanan data mentah sehingga developer bertanggung jawab penuh untuk apa data data tersebut digunakan apakah akan ditampilkan ke browser web ataukan akan digunakan untuk mengaktifkan device elektronik seperti Arduino, Port Raspberry Pi.  

Pada dasarnya aplikasi ini akan menyimpan data ke database MongoDB dan operasi CRUD (*Create, Read, Update, Delete*) dilakukan melalui *request* API.

Diagram kerja aplikasi Person REST digambarkan pada diagram dibawah ini


![](https://raw.githubusercontent.com/junwatu/pengenalan-nodejs-gitbook/develop/images/persons-rest-diagram.png)



Pengetesan operasi CRUD untuk aplikasi bisa dengan menggunakan bantuan alat *Command Line Interface* seperti cURL atau HTTPie ataupun tool yang lebih ramah seperti Postman dan bisa juga anda membangun antar muka web dengan memakai API yang disediakan oleh server Person ini. Contoh pengetesan untuk aplikasi Person REST ini bisa lihat pada sub-bab [**Pengetesan**](./testing.md).