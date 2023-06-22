---
title: Membuat Screen Mirroring Menggunakan Python
description: "meta description"
date: 2022-06-22T05:00:00Z
image: "/images/posts/Python.jpg"
categories: ["development"]
authors: ["Raka Rmp"]
tags: ["Python", "Flask", "Pillow"]
draft: false
---

Yo Broo dalam artikel ini, kita akan membahas cara membuat aplikasi screen mirroring sederhana menggunakan Python. Aplikasi ini akan memungkinkan Anda untuk mengambil tangkapan layar dari komputer Anda dan menampilkannya secara real-time melalui jaringan menggunakan protokol HTTP. Proyek ini akan menggunakan Flask, sebuah framework web Python yang ringan, dan Pillow, sebuah library Python untuk pemrosesan gambar.

## Persiapan

Untuk memulai, Anda perlu menginstal Python 3.8 atau versi yang lebih baru. Anda juga perlu menginstal Flask dan Pillow. Untuk menginstal Flask, Anda dapat menggunakan perintah berikut:

```bash
pip install flask
```

Untuk menginstal Pillow, Anda dapat menggunakan perintah berikut:

```bash
pip install pillow
```

## Membuat Aplikasi

Setelah Anda menginstal Python, Flask, dan Pillow, Anda dapat membuat aplikasi screen mirroring. Pertama, buat file server.py dan tambahkan kode berikut:

```python
from io import BytesIO
from flask import Flask, send_file, request
from PIL import ImageGrab

app = Flask(__name__)

@app.route("/")
def home_page():
    res = send_file("index.html", mimetype="text/html")
    return res

@app.route("/screenshot")
def img_screenshot():
    img_byte_arr = BytesIO()
    img_quality = request.args.get("quality", default=70, type=int)
    img_size = request.args.get("size", default=100, type=int)

    scale_factor = img_size / 100

    img = ImageGrab.grab()
    img_w = int(img.size[0] * scale_factor)
    img_h = int(img.size[1] * scale_factor)
    img.resize((img_w, img_h)).save(img_byte_arr, format="JPEG", quality=img_quality)
    img_byte_arr.seek(0)

    res = send_file(img_byte_arr, mimetype="image/jpeg")

    return res

if __name__ == '__main__':
    svhost = "0.0.0.0"
    svport = 8099
    app.run(svhost, svport)
```

Kode di atas akan membuat server Flask yang akan melayani permintaan tangkapan layar. Pertama, kita mengimpor BytesIO dari modul io untuk membantu kita mengonversi gambar menjadi byte array. Kemudian, kita mengimpor Flask dan send_file dari modul flask untuk membantu kita membuat server Flask dan mengirimkan file. Terakhir, kita mengimpor ImageGrab dari modul PIL untuk membantu kita mengambil tangkapan layar.

Setelah itu, kita membuat instance Flask dan menentukan rute untuk halaman utama dan tangkapan layar. Untuk rute halaman utama, kita mengirimkan file index.html sebagai respons. Untuk rute tangkapan layar, kita mengambil tangkapan layar menggunakan ImageGrab.grab() dan mengonversinya menjadi byte array menggunakan BytesIO. Kemudian, kita mengirimkan byte array tersebut sebagai respons.

Kita buat file index.html dan tambahkan kode berikut:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTTP SCREEN MIRRORING</title>
    <style type="text/css">
        * {
            margin: 0;
            padding: 0;
        }
        body {
            display: block;
            background: black;
            width: 100vw;
            height: 100vh;
        }
        img {
            display: block;
            width: 100%;
            height: 100%;
            object-fit: contain;
        }
    </style>
</head>
<body>
    <img src="">

    <script type="text/javascript">
        var url = "/screenshot"
        var img_element = document.querySelector("img");
        var img_quality = 80;
        var img_size = 100;

        function load_image() {
            let r = Math.random()
            img_element.src = `${url}?quality=${img_quality}&size=${img_size}&r=${r}`
        }

        window.onload = function() {
            img_element.onload = load_image;
            img_element.onerror = load_image;
            load_image();
        }
    </script>
</body>
</html>
```

Kode di atas akan menampilkan tangkapan layar dalam elemen <img> dengan memuat tangkapan layar dari URL /screenshot yang disediakan oleh aplikasi Flask.

## Menjalankan Aplikasi

Setelah Anda membuat file server.py dan index.html, Anda dapat menjalankan aplikasi screen mirroring Anda. Untuk menjalankan aplikasi, Anda dapat menggunakan perintah berikut:

```bash
python server.py 

# atau
 
python3 server.py
```

Setelah itu, Anda dapat membuka browser dan mengunjungi URL yang diberikan untuk melihat aplikasi screen mirroring Anda.

Lihat kode example di github [disini](https://github.com/rakarmp/http-screen-mirroring)

## Kesimpulan

Dengan menggunakan Flask dan Pillow, kita dapat membuat aplikasi screen mirroring sederhana yang memungkinkan kita untuk mengambil tangkapan layar dari komputer kita dan menampilkannya secara real-time melalui jaringan menggunakan protokol HTTP. Dengan sedikit kreativitas, kita dapat mengembangkan aplikasi ini menjadi aplikasi yang lebih canggih dan berguna. Jadi, mari bersama-sama memanfaatkan kekuatan Python dan merangkul sedikit kreativitas dalam perjalanan pengembangan kita!


