# Konverter Gambar Ke Data URI


Aplikasi ini adalah aplikasi Node.js CLI yang mengubah gambar ke format data URI dan kemudian menyimpan data tersebut ke database MySQL. 

Kode sumber selengkapnya bisa di lihat di [Github](https://github.com/junwatu/todatauri) pada branch `todatauri-mysql` atau ketik perintah berikut pada command line. 

    $ git clone -b todatauri-mysql https://github.com/junwatu/todatauri todatauri-mysql
    
    $ cd todatauri-mysql
    
    $ npm install
    
Ada tiga penggunaan file `tdi.js` yaitu

##Download PNG & Simpan Ke MySQL 

    $ node ./tdi.js <url_image_png_dari_internet>
    
 
##Demo 

    $ node ./tdi.js
        
##Tampilkan Data MySQL

    $ node ./tdi.js show
    
    

Mari kita lihat isi dari file `todatauri.js`. Pada dasarnya file ini merupakan pustaka sederhana yang akan mendownload image berformat `.png` di internet dan kemudian mengubahnya menjadi format **Data URI**.


```
/**
 * todatauri.js
 * Download image and convert it to  Data URI
 *
 * WTFPL
 * (c) 2015, Equan Pr.
 */
var fs = require('fs');
var http = require('http');
var https = require('https');
var url = require('url');

function Util() {

    var defaultImage = 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Node.js_logo.svg/320px-Node.js_logo.svg.png';
    var imageDest = 'download.png';
    var file;

    return {
        toDataURI: function(urlArg, cb) {
            var imageURL;
            urlArg ? imageURL = urlArg : imageURL = defaultImage;
            if(url.parse(imageURL).protocol === 'https:') {
                Util().httpsGetImage(imageURL, function(err, data){
                    err ? cb(err,null): cb(null, data);
                }) ;
            } else {
                Util().httpGetImage(imageURL, function(err, data){
                    err ? cb(err, null): cb(null, data);
                });
            } 
        },

        httpGetImage: function(url, cb) {
            file = fs.createWriteStream(imageDest);

            http.get(url, function(response) {
                response.pipe(file);

                console.log('Download node.js defaultImage from', defaultImage);
                console.log('\n');

                file.on('finish', function() {
                    file.close();
                    Util().imageToDataUri(imageDest, function(err, data) {
                        err ? cb(err, null) : cb(null,data);
                    });
                });
            })
        },

        httpsGetImage: function(url, cb) {
            file = fs.createWriteStream(imageDest);

            https.get(url, function(response) {
                response.pipe(file);

                console.log('Download node.js defaultImage from', defaultImage);
                console.log('\n');

                file.on('finish', function() {
                    file.close();
                    Util().imageToDataUri(imageDest, function(err, data) {
                        err ? cb(err, null) : cb(null,data);
                    });
                });
            })
        },

        imageToDataUri: function(imageName, cb) {
            //TODO: lookup mime type here
            var mime = 'image/png';
            var encoding = 'base64';

            var uri = 'data:' + mime + ';' + encoding + ',';

            fs.readFile(imageName, function(err, buf) {
                if (err) return cb(err, null);
                cb(null, uri + buf.toString(encoding));
            })
        }
    }
}

module.exports = Util();
```

Fungsi utama yang dipakai jika file `todatauri.js` di import yaitu fungsi `toDataURI()`
