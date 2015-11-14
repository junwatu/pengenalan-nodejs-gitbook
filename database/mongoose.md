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

Bagaimana dengan validasi data?. Jika anda lihat field data `rating` diatas dan umumnya mempunyai nilai antara 0 - 5 dan jika secara default diberi nilai 0 maka skema `rating` akan menjadi

    rating: {type: Number, 'default': 0}

Anda juga bisa memakai key `required` untuk menandakan bahwa field data tersebut bersifat wajib ada misalnya

    nama: {type: String, required: true} 

Untuk lebih jelasnya silahakan lihat dokumentasi dari [Validators Mongoose](http://mongoosejs.com/docs/validation.html).

Aplikasi node.js dengan database MongoDB yang memakai pustaka Mongoose dapat dikatakan mempunyai hubungan relasi satu-satu artinya 
dengan memakai model Mongoose berarti secara langsung aplikasi akan memakai data pada MongoDB. 

Kalau misalnya anda bekerja dengan database relasional MySQL maka anda akan memakai bahasa SQL seperti `INSERT INTO table VALUES (field1=data)` untuk memasukkan data sedangkan seperti anda ketahui jika dengan database NoSQL untuk menyimpan model object cukup dengan memakai metode misalnya `model.save()`. Dalam Mongoose untuk memakai model yang telah mempunyai schema seperti diatas

    var LokasiModel = mongoose.model('Lokasi', lokasiWisataKotaBatuSchema, 'lokasiWisataBatu')

Kode diatas memberi arti bahwa aplikasi akan memakai model `Lokasi` dengan **schema type** yang telah di definisikan sebelumnya yaitu
`lokasiWisataKotaBatuSchema` dan model ini akan di simpan pada koleksi data di MongoDB dengan nama koleksi adalah `lokasiWisataBatu`.

Untuk memakai model `Lokasi` caranya adalah dengan menciptakan `instance` dari model tersebut

    var lokasiModel = new LokasiModel()
    lokasiModel.nama = 'Museum Angkut'
    lokasiModel.alamat = 'Jl. Kembar 11'
    lokasiModel.rating = 5
    lokasiModel.fasilitas = ['Restoran', 'Parkir luas']

Kemudian untuk menyimpan data tersebut ke dalam database MongoDB

    lokasiModel.save(function(err){
      if(!err) console.log('Data Disimpan!')
    })

Cukup mudah bukan dan memang pustaka ini bertujuan untuk memudahkan developer dalam pemodelan data terutama jika data yang akan dimodel mempunyai struktur yang rumit misalnya nested document. Untuk lebih lengkapnya silahkan anda mengunjungi situs resmi [mongoosejs.com](http://mongoosejs.com/). 

##Projek 

Bagi anda yang sudah mengerti gambaran umum dari pustaka Mongoose ini silahkan mengutak atik contoh projek sederhana yang memakai framework ExpressJS dan Mongoose, [Person REST API](/person_rest_api/README.md).
