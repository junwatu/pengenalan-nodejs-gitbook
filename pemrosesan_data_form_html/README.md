# Pemrosesan Data Form HTML

Aplikasi web memperoleh data dari pengguna umumnya melalui pengisian form HTML. Contohnya seperti ketika registrasi di media sosial atau aktifitas update status di Facebook misalnya pasti akan mengisi text field dan kemudian menekan tombol submit ataupun enter agar data bisa terkirim dan diproses oleh server.

Data yang dikirim oleh form biasanya salah satu dari dua tipe mime berikut

* application/x-www-form-urlencoded
* multipart/form-data

Node.js sendiri hanya menyediakan parsing data melalui `body` dari `request` sedangkan untuk validasi atau pemrosesan data akan diserahkan kepada komunitas.

