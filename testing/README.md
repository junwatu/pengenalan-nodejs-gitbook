# Testing

Perangkat lunak tidak ada yang sempurna dan pasti mempunyai *bugs*. Salah satu cara untuk menguranginya atau mencegahnya untuk muncul di kemudian hari adalah dengan jalan melakukan pengetesan. Pengetesan memberikan keyakinan pada developer bahwa perangkat lunak bekerja sebagai mana mestinya dan jika ada perubahan misalnya penambahan atau pengurangan fitur dipastikan bahwa pengetesan akan selalu berhasil.

Ada banyak tipe pengetesan tetapi dalam pengembangan aplikasi web ada dua tipe pengetesan yang penting untuk diketahui yaitu **Unit Testing** dan **Acceptance Testing**.

##Unit Testing

**Unit Testing** dilakukan langsung pada level kode aplikasi yaitu pada fungsi atau metode dan ada dua metodologi yang sering digunakan yaitu **TDD** dan **BDD**. Dalam JavaScript tersedia banyak pustaka yang dibuat untuk pengetesan seperti module `assert` bawaan dari Node.js, Nodeunit, Mocha, Jasmine dll.

###Test Driven Development (TDD)

Istilah TDD ini menjadi sangat keren beberapa tahun belakangan ini. Konsep TDD adalah melakukan pengetesan terlebih dahulu baru kemudian menulis kode dari aplikasi, jadi mindset dari pembuatan perangkat lunak dibalik kalo dalam pengembangan perangkat lunak yang konvensional alurnya yaitu menulis kode terlebih dahulu baru kemudian menulis kode untuk pengetesan sedangkan dalam **Test Driven Development** proses ini dibalik. 

Kelemahan pengetesan ini adalah pada proses awal biasanya dibutuhkan waktu yang relatif lebih lama untuk mengembangkan aplikasi karena harus menulis kode pengetesan terlebih dahulu tetapi keuntungan jangka panjangnya yaitu aplikasi yang dihasilkan biasanya mempunyai *bugs* yang lebih sedikit.


###Behavior Driven Development (BDD) 

Pengetesan secara BDD memakai bahasa atau metode pengetesan yang lebih ramah yaitu dengan melakukan pengetesan dengan cara atau alur seperti **user story** sehingga pengetesan ini relatif lebih populer karena secara bahasa menjembatani atau memungkinkan kolaborasi antara developer dan klien. Ciri-ciri pustaka yang mendukung BDD seperti Mocha atau Jasmine yaitu pasti mempunyai metode pengetesan seperti `describe()` dan `it()`.

```
describe('Upload file', function(){
  it('Harus bisa menerima file jpeg', function(){
    //testing disini
  })

  it('Harus bisa menerima file png', function(){
    //testing disini
  })

  it('Harus bisa menerima file xcf', function(){
    //testing disini
  })
})
```

Kalau diterjemahkan secara bahasa manusia maka kode testing BDD diatas akan mudah dibaca yaitu *Upload file harus bisa menerima file jpeg, png atau xcf*.

##Acceptance Testing

Untuk pengetesan dari antar muka aplikasi web beserta fungsinya contohnya seperti pengetesan penekanan button apakah berfungsi dengan baik atau tidak adalah termasuk dari **Acceptance Testing**. Testing ini bisa dilakukan dengan memakai bantuan browser dan dengan munculnya *headless browser* seperti PhantomJS memungkinkan pengetesan dilakukan secara terintegrasi dengan kode *back-end*.


> Catatan penting dari testing adalah pengetesan diusahakan berjalan secara automatis sehingga jika ada kesalahan yang terjadi maka developer bisa segera memperbaikinya, maka dari itu testing pasti mempunyai yang namanya info laporan entah itu berupa file, output terminal atau antarmuka berupa web. Pada proses pengembangan perangkat lunak modern, automasi testing merupakan bagian yang sangat penting.

Dalam buku ini pengetesan akan dibatasi pada pengetesan aplikasi web khususnya aplikasi Node.js dengan REST dengan memakai Mocha.