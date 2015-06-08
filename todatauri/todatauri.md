# ToDataURI


Aplikasi ini adalah aplikasi Node.js CLI yang mengubah gambar png ke format data URI dan kemudian menyimpan data tersebut ke database MySQL. 


![todatauri flow diagram](https://raw.githubusercontent.com/junwatu/pengenalan-nodejs-gitbook/develop/images/todatauri.png)


##Data URI

Bagi yang belum tahu [Data URI](http://en.wikipedia.org/wiki/Data_URI_scheme) adalah salah satu cara untuk meng-embed data secara inline alih-alih harus mengambil data tersebut dari resource luar. Data yang akan diubah ke Data URI disini bisa berupa image, file csv dll. Untuk aplikasi ini hanya dibatasi untuk gambar berformat png.


```
data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAUAAAABXCAYAA
AB1NJw9AAAABmJLR0QA/wD/AP+gvaeTAAAbmklEQVR4nO2deXgVdZrvv2/V
SQIIqChi007rIAM5CSDkJDmJIqmToC0OTDvdHa+9qLd7+uLYKiCioFkocsI
mLgHtxZ6enmm1fXrAp71XbRU0nAooZDuHRUJYxIXxugC2smat3zt/JIFsZK
uqs5Df53nyPORU1e/9osX3/Lb3/REkkgiS...

```