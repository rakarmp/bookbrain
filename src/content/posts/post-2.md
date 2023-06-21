---
title: Fetching Data API React.js
description: "meta description"
date: 2022-06-20T05:00:00Z
image: "/images/posts/ReactJS.png"
categories: ["development"]
authors: ["Raka Rmp"]
tags: ["API", "ReactJS", "Fetch"]
draft: false
---

React.js adalah sebuah library JavaScript yang digunakan untuk membangun antarmuka pengguna (UI) interaktif. Salah satu kegunaan umum dari React.js adalah mengambil data dari API (Application Programming Interface) eksternal. Dalam artikel ini, kita akan menjelaskan langkah-langkah untuk melakukan fetching data API di React.js menggunakan metode fetch().

## Membuat Komponen React

Pertama, kita perlu membuat komponen React di mana kita akan melakukan fetching data API. Berikut adalah contoh sederhana pembuatan komponen:

```js
import React, { useEffect, useState } from 'react';

const FetchDataComponent = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetchData();
  }, []);

  const fetchData = async () => {
    try {
      const response = await fetch('https://api.example.com/data');
      const jsonData = await response.json();
      setData(jsonData);
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  };

  return (
    <div>
      {data ? (
        <ul>
          {data.map((item) => (
            <li key={item.id}>{item.name}</li>
          ))}
        </ul>
      ) : (
        <p>Loading data...</p>
      )}
    </div>
  );
};

export default FetchDataComponent;
```

Pada contoh di atas, kita menggunakan useState hook untuk menyimpan data yang diambil dari API. Kemudian, kita menggunakan useEffect hook dengan dependensi kosong agar fetching data hanya dilakukan sekali saat komponen pertama kali dirender. Dalam fungsi fetchData, kita menggunakan fetch() untuk mengirim permintaan GET ke URL API yang diinginkan. Setelah menerima respon, kita menggunakan response.json() untuk mengubah respons tersebut menjadi objek JSON. Kemudian, data JSON disimpan ke dalam state menggunakan setData().

Pada saat render, kita menampilkan data jika sudah ada, atau menampilkan pesan "Loading data..." jika data masih sedang diambil.

## Menggunakan Komponen FetchDataComponent

Setelah kita membuat komponen FetchDataComponent, kita dapat menggunakannya dalam komponen utama atau di komponen lain sesuai dengan kebutuhan kita. Berikut adalah contoh penggunaan komponen tersebut:

```js
import React from 'react';
import FetchDataComponent from './FetchDataComponent';

const App = () => {
  return (
    <div>
      <h1>Data dari API</h1>
      <FetchDataComponent />
    </div>
  );
};

export default App;
```

Pada contoh di atas, kita menggunakan komponen FetchDataComponent di dalam komponen App. Kita juga dapat menambahkan elemen HTML lain atau komponen lain sesuai dengan kebutuhan kita.

## Kesimpulan

Melakukan fetching data API di React.js relatif mudah dengan menggunakan metode fetch(). Dalam artikel ini, kita telah menjelaskan langkah-langkah dasar untuk melakukan fetching data API di React.js. Namun, dalam pengembangan nyata, kita mungkin perlu mempertimbangkan penanganan kesalahan, status loading, dan lainnya.
