#Pengetesan REST

Kita ambil contoh server yang dibuat dengan ExpressJS. Server dibawah ini akan mengeluarkan data berupa JSON pada URL `/`.

```
var express = require('express')
var app = express()

app.get('/', function (req, res) {
  res.json({
    message: 'hello'
  })
})

module.exports = app

``` 

Lalu bagaimana cara mengetest URL `/` diatas? dengan memakai Mocha, module `assert` dan modul [Supertest](https://github.com/visionmedia/supertest) yaitu modul npm yang khusus untuk mengetest server HTTP. Mocha termasuk pustaka pengetesan yang bisa dipakai secara BDD ataupun TDD. Pustaka ini secara default memakai style BDD dan metode yang yang biasa dipakai adalah `describe` & `it`. 

```
var mocha = require('mocha')
var request = require('supertest')
var assert = require('assert')
var app = require('../app')

describe('Test REST API', function(){
  describe('GET /', function(){
	it('should return json with key "message" and value "hello"', function(done){
	  request(app).get('/')
	  .set('Accept', 'application/json')
	  .expect('Content-Type', /json/)
	  .expect(200)
	  .expect(function(res){
	  	assert.equal(res.body.message, 'hello')
	  })
      .end(function(err, res){
      	if(err) return done(err)
      	done()
      })
	})
  })
})

```

Perlu anda ingat bahwa supertest akan secara otomatis menjalankan server ExpressJS dan mengalokasikan port sehingga anda tidak perlu mejalankan server secara langsung.
     
    request(app)

Kalau diterjemahkan dalam bahasa manusia kode diatas akan mengetest beberapa kondisi yaitu

    expect('Content-Type', /json/)

kode diatas artinya diharapkan response dari GET untuk URL `/` adalah bertipe `json`

    expect(200)

kode diatas artinya **response code** dari request HTTP harus mempunyai kode 200.

    expect(function(res){
	  assert.equal(res.body.message, 'hello')
	})

dan kode diatas artinya diharapkan bahwa **response body** dengan field `message` mempunyai value `hello` dan tentu saja anda bisa menambahkan banyak kondisi untuk pengetesan yang lebih detil. 

Untuk melakukan pengetesan cukup dengan menginstal dan jalankan `mocha` maka secara otomatis mocha akan menjalankan berkas berkas pengetesan yang berada pada folder `test`.

    $ npm install -g mocha

![](/images/testing-mocha.png)

Sebenarnya banyak yang bisa dijelaskan tentang pengetesan dan sudah banyak resource online diluar sana yang membahas tentang ini tapi yang perlu anda ingat adalah pastikan pengetesan dimasukkan dalam alur kerja dalam pengembangan perangkat lunak yang sedang anda kerjakan. 
