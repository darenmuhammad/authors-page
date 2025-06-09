
# 📡 Fetch API & Error Handling di JavaScript

Dokumen ini menjelaskan cara kerja `fetch()` beserta method chaining seperti `.then()`, `.json()`, `.catch()`, dan penggunaan `console.error`.

---

## 🔹 1. `fetch()`

Digunakan untuk melakukan permintaan (request) ke server dan mengambil data, umumnya dari API.

```javascript
fetch('https://api.example.com/data');
```


## 🔹 2. `.then()`

Digunakan untuk menangani hasil `Promise`. Setelah `fetch()` berhasil, kita bisa menggunakan `.then()` untuk melanjutkan ke proses berikutnya.

```javascript
fetch('https://api.example.com/data')
  .then((res) => {
    // melakukan sesuatu setelah response diterima
  });
```


## 🔹 3. `.json()`

Method dari `Response` object untuk mengubah response menjadi data JavaScript dari format JSON. Hasil dari `res.json()` juga berupa `Promise`.

```javascript
fetch('https://api.example.com/data')
  .then((res) => res.json()) // mengonversi response JSON menjadi object JS
  .then((data) => {
    console.log(data); // gunakan data di sini
  });
```


## 🔹 4. `.catch()`

Menangani error yang terjadi dalam `Promise chain`. Ini berguna jika request gagal atau ada masalah dalam proses.

```javascript
fetch('https://api.example.com/data')
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((err) => {
    console.error("Terjadi error:", err);
  });
```


## 🔹 5. `console.error()`

Digunakan untuk menampilkan pesan error ke console, sering dipakai dalam `catch()` untuk debugging.

```javascript
console.error("Ada masalah!", error);
```


## ✅ Contoh Lengkap:

```javascript
fetch('https://api.example.com/data')
  .then((res) => res.json())
  .then((data) => {
    console.log("Data diterima:", data);
  })
  .catch((error) => {
    console.error("Gagal fetch data:", error);
  });
```


## ⚠️ Validasi Status Respon

`fetch()` selalu *sukses* selama server merespons, bahkan jika statusnya 404. Untuk memastikan status sukses, periksa `res.ok` atau `res.status`.

```javascript
fetch('https://api.example.com/data')
  .then((res) => {
    if (!res.ok) throw new Error("Server error: " + res.status);
    return res.json();
  })
  .then((data) => console.log(data))
  .catch((err) => console.error(err));
```
