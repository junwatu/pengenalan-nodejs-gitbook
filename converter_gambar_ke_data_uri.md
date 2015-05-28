# Konverter Gambar Ke Data URI

CLI data uri merupakan aplikasi CLI yang mengubah gambar ke format data URI kemudian menyimpan data ini ke database MySQL.

```
/**
 * Download image and convert it to  Data URI
 *
 * WTFPL
 * (c) 2015, Equan Pr.
 */
var fs = require('fs');
var http = require('http');
var https = require('https');
var url = require('url');

process.argv[2] ? Util().toDataURI(process.argv[2]) : Util().toDataURI();

function Util() {

    var defaultImage = 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Node.js_logo.svg/320px-Node.js_logo.svg.png';
    var imageDest = 'download.png';
    var file;

    return {
        toDataURI: function(urlArg) {
            var imageURL;
            urlArg ? imageURL = urlArg : imageURL = defaultImage;
            url.parse(imageURL).protocol === 'https:' ? Util().httpsGetImage(imageURL) : Util().httpGetImage(imageURL);
        },

        httpGetImage: function(url) {
            file = fs.createWriteStream(imageDest);

            http.get(url, function(response) {
                response.pipe(file);

                console.log('Download node.js defaultImage from', defaultImage);
                console.log('\n');

                file.on('finish', function() {
                    file.close();
                    Util().imageToDataUri(imageDest, function(err, data) {
                        err ? console.log(err) : console.log(data);
                    });
                });
            })
        },

        httpsGetImage: function(url) {
            file = fs.createWriteStream(imageDest);

            https.get(url, function(response) {
                response.pipe(file);

                console.log('Download node.js defaultImage from', defaultImage);
                console.log('\n');

                file.on('finish', function() {
                    file.close();
                    Util().imageToDataUri(imageDest, function(err, data) {
                        err ? console.log(err) : console.log(data);
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
```