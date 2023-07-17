---
title: Belajar JavaScript dengan Satu Project
description: "meta description"
date: 2022-07-17T05:00:00Z
image: "/images/posts/LearnJavascript.jpg"
categories: ["development"]
authors: ["Raka Rmp"]
tags: ["Javascript", "HTML5", "Css"]
draft: false
---

JavaScript adalah bahasa pemrograman yang populer dan kuat yang digunakan untuk mengembangkan aplikasi web interaktif. Salah satu cara efektif untuk belajar JavaScript adalah dengan melakukan proyek nyata yang melibatkan beberapa konsep dan keterampilan dalam bahasa tersebut. Dalam artikel ini, kita akan belajar JavaScript dengan membuat proyek sederhana yang melibatkan penggunaan fungsi, pengontrol aliran, manipulasi elemen HTML, dan array.

## Project: Mengembangkan Mesin Slot Sederhana

Tujuan dari proyek ini adalah membuat mesin slot sederhana di browser yang memungkinkan pengguna memasukkan deposit awal, mengatur taruhan per baris dan jumlah baris, serta melihat hasil spin mesin slot. Mesin slot akan menampilkan simbol-simbol acak pada masing-masing reel dan memberikan kemenangan jika beberapa simbol cocok pada baris taruhan.

## 1: Mempersiapkan HTML dan CSS

Kita akan memulai dengan menyiapkan struktur HTML dan gaya CSS untuk mesin slot. Buatlah berkas HTML dengan kode berikut:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mesin Slot Sederhana</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <h1>Mesin Slot Sederhana</h1>
    <div id="reels">
      <!-- Reel 1 -->
      <div class="reel" id="reel1">
        <div class="symbol">-</div>
        <div class="symbol">-</div>
        <div class="symbol">-</div>
        <div class="symbol">-</div>
      </div>

      <!-- Reel 2 -->
      <div class="reel" id="reel2">
        <div class="symbol">-</div>
        <div class="symbol">-</div>
        <div class="symbol">-</div>
        <div class="symbol">-</div>
      </div>

      <!-- Reel 3 -->
      <div class="reel" id="reel3">
        <div class="symbol">-</div>
        <div class="symbol">-</div>
        <div class="symbol">-</div>
        <div class="symbol">-</div>
      </div>
    </div>
    <div>
      <p>Saldo Anda: $<span id="balance">0</span></p>
      <p>
        Taruhan per Baris:
        <input type="number" id="betPerLine" value="1" min="1" max="10" />
      </p>
      <p>
        Jumlah Baris:
        <input type="number" id="numberOfLines" value="1" min="1" max="3" />
      </p>
      <button id="spinBtn">Spin</button>
      <p id="result"></p>
    </div>

    <script src="script.js"></script>
  </body>
</html>
```

Selanjutnya, buat berkas styles.css dengan kode berikut untuk mengatur tampilan mesin slot:

```css
body {
  font-family: Arial, sans-serif;
  text-align: center;
  margin: 30px;
}

h1 {
  color: #4caf50;
}

#reels {
  display: flex;
  justify-content: space-around;
  margin: 30px;
}

.reel {
  width: 100px;
  height: 150px;
  border: 2px solid #4caf50;
  border-radius: 5px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px;
}

.symbol {
  font-size: 24px;
  padding: 5px;
}

button {
  padding: 10px 20px;
  font-size: 18px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 20px;
}

button:hover {
  background-color: #45a049;
}

#result {
  font-size: 20px;
  margin-top: 20px;
}
```

## 2: Menulis JavaScript untuk Proyek

Kode JavaScript akan menangani logika mesin slot dan interaksi dengan pengguna. Buatlah berkas script.js dan masukkan kode berikut:

```js
const ROWS = 3;
const COLS = 3;

const SYMBOLS_ARRAY = ["A", "B", "C", "D"];

const SYMBOL_VALUES = {
  A: 5,
  B: 4,
  C: 3,
  D: 2,
};

let balance = 0;
let betPerLine = 1;
let numberOfLines = 1;

const updateBalance = () => {
  document.getElementById("balance").textContent = balance.toFixed(2);
};

const deposit = () => {
  const depositAmount = prompt("Masukkan jumlah deposit: ");
  const numberDepositAmount = parseFloat(depositAmount);

  if (isNaN(numberDepositAmount) || numberDepositAmount <= 0) {
    alert("Jumlah deposit tidak valid, coba lagi.");
    return deposit();
  }

  balance += numberDepositAmount;
  updateBalance();
};

const setBetAndLines = () => {
  betPerLine = parseInt(document.getElementById("betPerLine").value);
  numberOfLines = parseInt(document.getElementById("numberOfLines").value);
};

const spin = () => {
  const reels = [];
  for (let i = 0; i < COLS; i++) {
    reels.push([]);
    for (let j = 0; j < ROWS; j++) {
      const randomIndex = Math.floor(Math.random() * SYMBOLS_ARRAY.length);
      const selectedSymbol = SYMBOLS_ARRAY[randomIndex];
      reels[i].push(selectedSymbol);
    }
  }

  return reels;
};

const transpose = (reels) => {
  const rows = [];

  for (let i = 0; i < ROWS; i++) {
    rows.push([]);
    for (let j = 0; j < COLS; j++) {
      rows[i].push(reels[j][i]);
    }
  }

  return rows;
};

const printRows = (rows) => {
  for (const row of rows) {
    let rowString = "";
    for (const [i, symbol] of row.entries()) {
      rowString += symbol;
      if (i !== row.length - 1) {
        rowString += " | ";
      }
    }
    console.log(rowString);
  }
};

const getWinnings = (rows, bet, lines) => {
  let winnings = 0;

  for (let row = 0; row < lines; row++) {
    const symbols = rows[row];
    let allSame = true;

    for (const symbol of symbols) {
      if (symbol !== symbols[0]) {
        allSame = false;
        break;
      }
    }

    if (allSame) {
      winnings += bet * SYMBOL_VALUES[symbols[0]];
    }
  }

  return winnings;
};

const updateReels = (reels) => {
  for (let i = 0; i < COLS; i++) {
    const reel = document.getElementById(`reel${i + 1}`);
    const symbols = reel.getElementsByClassName("symbol");
    for (let j = 0; j < ROWS; j++) {
      symbols[j].textContent = reels[i][j];
    }
  }
};

const game = () => {
  deposit();
  updateBalance();

  document.getElementById("spinBtn").addEventListener("click", () => {
    setBetAndLines();
    balance -= betPerLine * numberOfLines;
    if (balance < 0) {
      alert(
        "Saldo Anda tidak mencukupi untuk bertaruh. Mohon isi saldo terlebih dahulu."
      );
      return;
    }
    const reels = spin();
    updateReels(reels);
    const rows = transpose(reels);
    printRows(rows);
    const winnings = getWinnings(rows, betPerLine, numberOfLines);
    balance += winnings;
    updateBalance();
    document.getElementById("result").textContent = `Anda menang $${winnings}.`;

    if (balance <= 0) {
      alert("Anda kehabisan uang!");
      document.getElementById("spinBtn").disabled = true;
    }
  });
};

game();
```

## Penjelasan

1. Variabel Konstan dan Penetapan Nilai: Variabel ROWS dan COLS digunakan untuk mengatur ukuran mesin slot. SYMBOLS_ARRAY adalah array yang berisi simbol-simbol yang akan digunakan dalam mesin slot. SYMBOL_VALUES adalah objek yang berisi nilai kemenangan untuk setiap simbol.

2. Variabel Global: Variabel balance, betPerLine, dan numberOfLines digunakan untuk melacak saldo pemain dan pengaturan taruhan.

3. Fungsi `deposit()``: Fungsi ini digunakan untuk meminta input pengguna untuk deposit awal dan memperbarui saldo.

4. Fungsi `setBetAndLines()``: Fungsi ini digunakan untuk mengambil nilai taruhan per baris dan jumlah baris dari elemen input di HTML.

5. **Fungsi spin()``**: Fungsi ini akan menghasilkan reel-reel acak dengan simbol-simbol dari array SYMBOLS_ARRAY`.

6. Implementasi Fungsi Lainnya: Fungsi updateReels(), updateBalance(), dan game() sama seperti sebelumnya.

## Running project

Simpan berkas-berkas tersebut (HTML, CSS, dan JavaScript) dengan nama yang sesuai, misalnya index.html, styles.css, dan script.js. Kemudian, buka index.html di browser Anda untuk melihat mesin slot sederhana yang telah Anda buat.

### Kesimpulan

Dengan menyelesaikan proyek mesin slot sederhana ini, Anda telah belajar JavaScript melalui praktik langsung. Proyek ini melibatkan konsep penggunaan fungsi, array, interaksi dengan elemen HTML, dan pengontrol aliran untuk membangun aplikasi web yang interaktif.

Anda dapat mengembangkan proyek ini lebih lanjut dengan menambahkan fitur-fitur seperti animasi spin reel, peningkatan grafis, dan sistem kemenangan yang lebih kompleks. Jangan ragu untuk berkreasi dan terus belajar untuk meningkatkan keterampilan Anda dalam bahasa pemrograman JavaScript. Selamat mencoba!
