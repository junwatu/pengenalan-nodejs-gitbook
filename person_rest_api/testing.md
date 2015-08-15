#Pengetesan

Untuk menggunakan atau pengetesan API ini cara termudah adalah dengan memakai [Postman](https://www.getpostman.com/). 

##POST /persons 

Untuk membuat data Person baru melalui api `/persons`

![](https://raw.githubusercontent.com/junwatu/pengenalan-nodejs-gitbook/develop/images/person-rest-post.png)


##GET /persons

Mengambil data dengan mengakses API `/persons` yang akan mengembalikan semua data yang telah tersimpan sebelumnya. 

![](https://raw.githubusercontent.com/junwatu/pengenalan-nodejs-gitbook/develop/images/person-rest-get.png)


##PUT /persons/:username

Update data bisa dilakukan dengan mudah dengan memakai PUT.

![](https://raw.githubusercontent.com/junwatu/pengenalan-nodejs-gitbook/develop/images/person-rest-update.png)


##DELETE /persons/:username

Operasi penghapusan data hanya bisa dilakukan satu persatu melalui key `:username`.

![](https://raw.githubusercontent.com/junwatu/pengenalan-nodejs-gitbook/develop/images/person-rest-delete.png)