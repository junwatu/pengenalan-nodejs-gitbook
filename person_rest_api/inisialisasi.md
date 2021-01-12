# Cara Kerja

Cara kerja dari aplikasi Person REST ini cukup mudah. Hanya saja untuk antar muka dengan pengguna tidak melalui antar muka web seperti halnya kita mengakses halaman Facebook misalnya, karena secara umum aplikasi REST fungsinya lebih ke memberikan layanan data mentah sehingga developer bertanggung jawab penuh untuk apa data-data tersebut digunakan, apakah akan ditampilkan ke browser web atau digunakan pada aplikasi mobile android atau akan digunakan untuk mengaktifkan device elektronik seperti Arduino, Raspberry Pi dll.

Untuk aplikasi Person REST ini, data disimpan di database MongoDB melalui operasi CRUD \(_Create, Read, Update, Delete_\) yang dapat diakses melalui _request_ API yang telah di sebutkan sebelumnya.

Diagram kerja aplikasi Person REST digambarkan pada diagram dibawah ini

![](../.gitbook/assets/persons-rest-diagram.png)

Pengetesan operasi CRUD untuk aplikasi bisa dengan menggunakan bantuan alat _Command Line Interface_ seperti cURL atau HTTPie ataupun tool yang lebih ramah seperti Postman dan bisa juga anda membangun antar muka web dengan memakai API yang disediakan oleh server Person ini. Contoh pengetesan untuk aplikasi Person REST ini bisa lihat pada sub-bab [**Pengetesan**](testing.md).

