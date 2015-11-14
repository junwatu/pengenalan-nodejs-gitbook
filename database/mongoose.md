#Mongoose

Seperti dikatakan sebelumnya untuk memudahkan pemodelan data di MongoDB anda bisa memakai pustaka 
[Mongoose](http://mongoosejs.com/). Meskipun sebenarnya Mongoose memakai objek JavaScript biasa dan mendukung
banyak metode `query` data tetapi yang paling membedakan adalah Mongoose mendukung schema type dan validasi di level schema.

    data:{type: schemaType}

##Schema Type

Ada beberapa schema type yang didukung oleh pustaka ini yaitu
- String 
- Number
- Date
- Boolean
- Buffer (untuk data binary misalnya gambar, mp3 dll.)
- Mixed (data dengan tipe apa saja)
- Array
- ObjectId

##Pemodelan Data

Lalu bagaimana Mongoose memodel data? ambil contoh misalnya dalam pengembangan aplikasi, data yang akan 
dipakai seperti berikut

```
var lokasiWisataKotaBatu = [{
  nama: 'Batu Night Square',
  alamat: 'Jl. Oro oro ombo 13, Tlekung'
  rating: 3,
  fasilitas: ['Wahana bermain','Roller coaster', 'Taman lampion']
}]
```
Dari data diatas dengan memakai Mongoose sangat mudah untuk diterjemahkan ke skema dan tipe data untuk tiap field

```
var lokasiWisataKotaBatuSchema = new mongoose.schema({
  nama: String,
  alamat: String,
  rating: Number,
  fasilitas: [String]
})
```

Bagaimana dengan validasi?. Jika anda lihat field data `rating` diatas dan umumnya mempunyai nilai antara 0 - 5 dan jika secara default diberi nilai 0 maka skema `rating` akan menjadi

    rating: {type: Number, 'default': 0}

Anda juga bisa memakai key `required` untuk menandakan bahwa field data tersebut bersifat wajib ada misalnya

    nama: {type: String, required: true} 

(TODO: Referensi validasi Mongoose)

Aplikasi node.js dengan database MongoDB yang memakai pustaka Mongoose dapat dikatakan mempunyai hubungan relasi satu-satu artinya 
dengan memakai model Mongoose berarti secara langsung aplikasi akan memakai data pada MongoDB. Kalau misalnya anda bekerja dengan database 
relasional MySQL maka anda akan memakai bahasa SQL seperti `INSERT INTO table VALUES (field1=data)` untuk memasukkan data sedangkan seperti
anda ketahui dengan database NoSQL anda bisa memakai model object dan menyimpannya dengan misalnya dengan `model.save()`.

Dalama Mongoose untuk memakai model yang telah mempunyai schema seperti diatas

    var LokasiModel = mongoose.model('Lokasi', lokasiWisataKotaBatuSchema, 'lokasiWisataBatu')

Kode diatas memberi arti bahwa aplikasi akan memakai model `Lokasi` dengan **schema type** yang telah di definisikan sebelumnya yaitu
`lokasiWisataKotaBatuSchema` dan model ini akan di simpan pada koleksi data di MongoDB dengan nama koleksi adalah `lokasiWisataBatu`.

Untuk memakai `LokasiModel` caranya adalah dengan menciptakan `instance` dari model ini

    var lokasiModel = new LokasiModel()
    lokasiModel.nama = 'Museum Angkut'
    lokasiModel.alamat = 'Jl. Kembar 11'
    lokasiModel.rating = 5
    lokasiModel.fasilitas = ['Restoran', 'Parkir luas']

Kemudian menyimpan data tersebut ke database MongoDB

    lokasiModel.save(function(err){
      if(!err) console.log('Data Disimpan!')
    })

Cukup mudah sebenarnya dan memang pustaka ini bertujuan untuk memudahkan developer dalam pemodelan data. Untuk lebih lengkapnya
silahkan anda mengunjungi situs resmi [mongoosejs.com](http://mongoosejs.com/). 


##Projek 

Bagi anda yang sudah mengerti gambaran umum dari pustaka Mongoose ini silahkan mengutak atik contoh projek [Person REST API](/person_rest_api/README.md).
