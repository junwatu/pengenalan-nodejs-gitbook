# Cara Kerja

Cara kerja dari aplikasi Person REST ini cukup mudah seperti halnya aplikasi web lainnya. Hanya saja untuk antar muka dengan pengguna tidak melalui antar muka web. Jadi interaksi dengan aplikasi ini adalah melalui *request* URL  

Pada dasarnya aplikasi ini akan menyimpan data ke database MongoDB dan operasi CRUD (*Create, Read, Update, Delete*) dilakukan melalui *request* API.

Diagram kerja aplikasi Person REST digambarkan pada diagram dibawah ini


![](https://raw.githubusercontent.com/junwatu/pengenalan-nodejs-gitbook/develop/images/persons-rest-diagram.png)



Untuk pengetesan operasi CRUD, pengguna aplikasi ini bisa secara langsung menggunakan bantuan alat *Command Line Interface* seperti Curl atau HTTPie ataupun yang lebih ramah seperti Postman dan bisa juga anda membangun antarmuka web dengan memakai API yang disediakan oleh server Person ini.

Contoh pengetesan untuk aplikasi Person REST ini bisa lihat pada sub-bab [**Pengetesan**](./testing.md).