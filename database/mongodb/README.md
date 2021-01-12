# MongoDB

Kalau anda sudah terbiasa memakai database relasional seperti MySQL mungkin diperlukan sedikit perubahan _mindset_ untuk mengenal tipe database yang namanya **NoSQL**. Seperti arti dari namanya, database ini merupakan database yang tidak memakai bahasa SQL query data tapi bisa secara langsung menggunakan bahasa pemrograman client sebagai contoh adalah [MongoDB](https://www.mongodb.org/).

Database **NoSQL** seperti MongoDB menyimpan data sebagai dokumen yang _schema-less_ yang artinya yaitu data yang disimpan mempunyai _key - value_ yang tidak terikat atau bebas. Anda bisa membayangkannya sebagai data JSON yang tersimpan di database.

Klien bisa berinteraksi langsung dengan database MongoDB dengan menggunakan shell JavaScript `mongo` untuk administrasi dan query data. Sebagai contoh jika kita ingin membuat sample data sebanyak 100 di **collection** `sample` maka perintah dalam shell adalah seperti berikut,

```text
$ mongo
MongoDB shell version: 2.6.9
connecting to: test
> use sample;
switched to db sample

> for(var i=0; i<100; i++){ db.sample.insert({band:"Dewa "+i})};
WriteResult({ "nInserted" : 1 })

> db.sample.count()
100

> db.sample.find();
{ "_id" : ObjectId("55cf520e2dd317a13673d11b"), "band" : "Dewa 0" }
{ "_id" : ObjectId("55cf520e2dd317a13673d11c"), "band" : "Dewa 1" }
{ "_id" : ObjectId("55cf520e2dd317a13673d11d"), "band" : "Dewa 2" }
{ "_id" : ObjectId("55cf520e2dd317a13673d11e"), "band" : "Dewa 3" }
{ "_id" : ObjectId("55cf520e2dd317a13673d11f"), "band" : "Dewa 4" }
{ "_id" : ObjectId("55cf520e2dd317a13673d120"), "band" : "Dewa 5" }
{ "_id" : ObjectId("55cf520e2dd317a13673d121"), "band" : "Dewa 6" }
{ "_id" : ObjectId("55cf520e2dd317a13673d122"), "band" : "Dewa 7" }
{ "_id" : ObjectId("55cf520e2dd317a13673d123"), "band" : "Dewa 8" }
{ "_id" : ObjectId("55cf520e2dd317a13673d124"), "band" : "Dewa 9" }
{ "_id" : ObjectId("55cf520e2dd317a13673d125"), "band" : "Dewa 10" }
{ "_id" : ObjectId("55cf520e2dd317a13673d126"), "band" : "Dewa 11" }
{ "_id" : ObjectId("55cf520e2dd317a13673d127"), "band" : "Dewa 12" }
{ "_id" : ObjectId("55cf520e2dd317a13673d128"), "band" : "Dewa 13" }
{ "_id" : ObjectId("55cf520e2dd317a13673d129"), "band" : "Dewa 14" }
{ "_id" : ObjectId("55cf520e2dd317a13673d12a"), "band" : "Dewa 15" }
{ "_id" : ObjectId("55cf520e2dd317a13673d12b"), "band" : "Dewa 16" }
{ "_id" : ObjectId("55cf520e2dd317a13673d12c"), "band" : "Dewa 17" }
{ "_id" : ObjectId("55cf520e2dd317a13673d12d"), "band" : "Dewa 18" }
Type "it" for more
>
```

Untuk lebih jelasnya jika anda tertarik untuk bermain main dengan terminal MongoDB silahkan kunjungi [dokumentasinya](https://docs.mongodb.org/getting-started/shell/).

Sebelum kita lanjutkan ke koneksi Node.js dan MongoDB, perlu di ingat beberapa konsep penting dari MongoDB

## Collection

**Collection** adalah kumpulan dari **document**, analoginya walaupun kurang tepat sebenarnya bisa dibilang seperti tabel kalo dalam database relasional.

## Document

**Document** itu sendiri adalah data yang tersimpan di database NoSQL dan didefinisikan oleh yang namanya **Schema**.

## Schema

Sebelumnya di katakan bahwa NoSQL menyimpan data yang _schema-less_, memang benar tapi tetap untuk menyimpan suatu dokumen di database biasanya aplikasi bekerja dengan model data tertentu misalnya untuk data `Person` bisa mempunyai _key - value_ seperti berikut

```text
{
    nama: "Kebo Ijo",
    email: "mbolang@kebo.xyz",
    username: "obek_seloso"
}
```

