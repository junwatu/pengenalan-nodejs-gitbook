# Konverter PNG Ke Data URI

Mari kita lihat isi dari file `todatauri.js`. Pada dasarnya file ini merupakan pustaka sederhana yang akan mendownload image berformat `.png` di internet dan kemudian mengubahnya menjadi format **Data URI**.

Jadi anda bisa menggunakan seperti halnya modul npm dengan bantuan `require`.


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

Fungsi utama pada file `todatauri.js` yaitu fungsi `imageToDataUri()` dan jika dilihat isinya maka sebenarnya sangat sederhana untuk mengubah gambar png ke encoding `base64` yang akan digunakan di Data URI.

    buf.toString(encoding))

[`fs.readFile(filename[, options], callback)`](https://nodejs.org/api/fs.html#fs_fs_readfile_filename_options_callback) merupakan fungsi untuk membaca file secara asinkron dan jika encoding tidak di berikan maka hasil pembacaan file akan mengembalikan data berupa `buffer`. Sehingga untuk mengubah data `buffer` ini ke `base64` cukup dengan memakai metode `.toString(encoding)`.
