#ECMAScript 2015 atau ES6

Meskipun ECMAScript 2015 atau yang lebih dikenal ES6 sudah [diresmikan](http://www.ecma-international.org/ecma-262/6.0/) tetapi implementasi di browser dan platform Node.js masih terjadi secara *gradual*. Pada saat buku ini ditulis pada platform Node.js 4.x (LTS) dan 5.x sudah banyak fitur-fitur ES6 yang *built-in* dan untuk fitur yang belum didukung anda bisa memakai tool yang bernama Babel. 

Untuk mempelajari ES6 banyak sekali resource online yang menyediakan jadi silahkan anda bereksplorasi dan mencoba konsep-konsep baru yang ditawarkan oleh JavaScript. Anda bisa memulai dari buku online gratis tentang ES6

- [ExploringJS ES6](http://exploringjs.com/es6/)

Pada dasarnya Babel berfungsi untuk mengkompilasi ES6 (atau ES7, 8) menjadi ES5 sehingga bisa dijalankan pada browser atau platform Node.js yang belum mendukung ES6. Salah satu pertanyaan terbesar kalau anda memakai Babel adalah bagaimana mengkompilasi hanya beberapa fitur ES6 saja jikalau browser ataupun Node.js yang akan kita pakai secara native sudah mendukung sebagian atau beberapa fitur ES6? 

###Babel on The Fly

Sejak di release [Babel 6](https://babeljs.io/blog/2015/10/29/6.0.0/), tool ini mendukung kompilasi ES6 berdasarkan plugin artinya anda bisa memilih fitur mana yang akan dikompilasi ke ES5 jika misalnya pada platform Node.js sudah mendukung banyak fitur ES6. 

Kalau anda pernah memakai `babel-node` make sekarang diganti dengan paket `babel-cli`

    $ npm install -g babel-cli

Apa kegunaannya? `babel-cli` sangat berguna untuk mengkompilasi ES6 secara `on the fly` misalnya begini

**lib/module.js**
```
'use strict'
export function test() {
  console.log('test')
}
```

**main.js**

```
'use strict'
import {test} from './lib/module'
test()
```

Maka untuk mengeksekusi file `main.js` bisa melalui `babel-node`

    $ babel-node main.js
    
Jika anda memakai project dengan ES6 selain `babel-cli` maka paket berikut juga perlu di install
    
    $ npm install --save-dev babel babel-core babel-loader
   
dan juga setting file `.babelrc` (meskipun sebenarnya ada beberapa alternatif lain dimana harus menuliskan setting babel tapi cara ini lebih UNIX, tergantung selera masing masing)

**.babelrc**

```
{
  "plugins": ["transform-es2015-modules-commonjs"]
}

``` 

Bisa anda lihat bahwa plugins yang akan kita gunakan adalah `transform-es2015-modules-commonjs` jadi harus di install juga 

    $ npm install --save-dev babel-plugin-transform-es2015-modules-commonjs

Lalu bagaimana kalau kita menginginkan semua plugin kita pakai? jawabannya adalah dengan memakai `presets`

    $ npm install --save-dev babel-preset-es2015
  
 dan `.babelrc` perlu anda rubah menjadi seperti dibawah ini

```
{
  "presets": ["es2015"]
}
```

**Catatan** 
Penjelasan diatas berlaku untuk JavaScript yang digunakan pada sisi server untuk client atau JavaScript yang berjalan pada browser anda bisa memakai [webpack](https://webpack.github.io/) bersama dengan babel.