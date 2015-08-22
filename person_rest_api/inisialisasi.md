# Cara Kerja

Cara kerja dari aplikasi Person REST ini cukup mudah seperti halnya aplikasi web lainnya. Hanya saja untuk antar muka dengan pengguna tidak melalui antar muka web. 

Pada dasarnya aplikasi ini akan menyimpan data ke database MongoDB dan operasi CRUD (*Create, Read, Update, Delete*) dilakukan melalui *request* API.

Diagram kerja aplikasi Person REST digambarkan pada diagram dibawah ini


![](https://raw.githubusercontent.com/junwatu/pengenalan-nodejs-gitbook/develop/images/persons-rest-diagram.png)



Pengetesan operasi CRUD untuk aplikasi bisa dengan menggunakan bantuan alat *Command Line Interface* seperti cURL atau HTTPie ataupun tool yang lebih ramah seperti Postman dan bisa juga anda membangun antarmuka web dengan memakai API yang disediakan oleh server Person ini.

Contoh pengetesan untuk aplikasi Person REST ini bisa lihat pada sub-bab [**Pengetesan**](./testing.md).