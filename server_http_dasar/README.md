# Server HTTP Dasar

Penggunaan Node.js yang revolusioner yaitu sebagai server. Yup...mungkin kita terbiasa memakai server seperti Apache - PHP, Nginx - PHP, Java - Tomcat - Apache atau IIS - ASP.NET sebagai pemroses data di sisi server, tetapi sekarang semua itu bisa tergantikan dengan memakai JavaScript - Node.js!. Lihat contoh dasar dari server Node.js berikut (kode sumber pada direktori code pada repositori ini)

[`server-http.js`](https://raw.github.com/idjs/belajar-nodejs/gh-pages/code/server-http.js)

```
var http = require('http'),
	PORT = 3400;

var server = http.createServer(function(req, res){
	var body = "<pre>Haruskah belajar Node.js?</pre><p><h3>...Yo Mesto!</h3></p>"
	res.writeHead(200, {
		'Content-Length':body.length,
		'Content-Type':'text/html',
		'Pesan-Header':'Pengenalan Node.js'
	});

	res.write(body);
	res.end();
});

server.listen(PORT);

console.log("Port "+PORT+" : Node.js Server...");

```

Paket [http](http://nodejs.org/api/http.html#http_http) merupakan paket bawaan dari platform Node.js yang mendukung penggunaan fitur-fitur protokol HTTP. Object `server` merupakan object yang di kembalikan dari fungsi `createServer()`.

```
var server = http.createServer([requestListener])

```

Tiap request yang terjadi akan ditangani oleh fungsi callback `requestListener`. Cara kerja callback ini hampir sama dengan ketika kita menekan tombol button html yang mempunyai atribut event `onclick`, jika ditekan maka fungsi yang teregistrasi oleh event `onclick` yaitu `clickHandler(event)` akan dijalankan.

[`onclick-button.html`](https://raw.github.com/idjs/belajar-nodejs/gh-pages/code/onclick-button.html)

```
<script>
	function clickHandler(event){
		console.log(event.target.innerHTML+" Terus!");
	}
</script>

<button onclick="clickHandler(event)">TEKAN</button>

```

Sama halnya dengan callback `requestListener` pada object `server` ini jika ada request maka `requestListener` akan dijalankan


```

function(req, res){
	var body = "<pre>Haruskah belajar Node.js?</pre><p><h3>...Yo Mesto!</h3></p>"
	res.writeHead(200, {
		'Content-Length':body.length,
		'Content-Type':'text/html',
		'Pesan-Header':'Pengenalan Node.js'
	});

	res.write(body);
	res.end();
}

```

Paket http Node.js memberikan keleluasan bagi developer untuk membangun server tingkat rendah. Bahkan mudah saja kalau harus men-setting nilai field header dari [HTTP](http://en.wikipedia.org/wiki/List_of_HTTP_header_fields).

Seperti pada contoh diatas agar respon dari request diperlakukan sebagai HTML oleh browser maka nilai field `Content-Type` harus berupa `text/html`. Setting ini bisa dilakukan melalui metode [`writeHead()`](http://nodejs.org/api/http.html#http_response_writehead_statuscode_reasonphrase_headers), `res.setHeader(field, value)` dan beberapa metode lainnya.

Untuk membaca header bisa dipakai fungsi seperti `res.getHeader(field, value)` dan untuk menghapus field header tertentu dengan memakai fungsi `res.removeHeader(field)`. Perlu diingat bahwa setting header dilakukan sebelum fungsi `res.write()` atau `res.end()` di jalankan karena jika `res.write()` dijalankan tetapi kemudian ada perubahan field header maka perubahan ini akan diabaikan.

Satu hal lagi yaitu tentang [kode status dari respon HTTP](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes). Kode status ini bisa disetting selain 200 (request http sukses), misalnya bila diperlukan halaman error dengan kode status 404.
