# Multipart Data

*Parsing* data form dan file yang di *upload* ke server Node.js adalah pekerjaan yang cukup susah kalo dikerjakan secara manual atau dari *scratch* karena disamping harus *parsing* data binary yang berupa file juga harus *parsing* data form.

Protokol untuk `multipart/form-data` di definisikan secara lengkap di [RFC 2388](https://www.ietf.org/rfc/rfc2388.txt). 
