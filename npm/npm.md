# Konsep

npm memakai sistem modul [CommonJS](http://www.commonjs.org/specs/) yang cukup mudah dalam penggunaanya. Sistem modul ini akan meng-export objek JavaScript ke variabel `exports` yang bersifat global di modul tersebut.

Sebagai contoh

`band.js`

```
'use strict';

function Band(){}

Band.prototype.info = function(){
    return 'Nama Band: '+this.name;
}

Band.prototype.add = function(name){
    this.name = name;
}

module.exports = new Band();
```

Untuk pemakaiannya seperti di bawah ini

`app.js`

```
var band = require('./band.js');
band.add('Dewa 19');

console.log(band.info);

```


`require()` diatas adalah fungsi sinkron yang meload paket atau modul lain dari sistem file.







