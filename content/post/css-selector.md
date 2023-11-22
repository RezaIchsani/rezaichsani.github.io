---
title: 'CSS Selector'
date: 2023-11-22
draft: false
weight: 1
categories: ['Programming', 'CSS']
tags: ['CSS']
---

## Universal Selector

---

**Universal Selector** -> ditulis menggunakan karakter bintang (\*) :

```css
* {
  color: blue;
  background-color: white;
}
```

## Attribute Selectors

---

**Attribute Selectors** -> dipakai untuk mencari tag HTML berdasarkan ada atau tidaknya sebuah attribut. Attribut ini mirip dengan class atau id selector, namun bersifat lebih global, contoh :

```
<a href="https://rezaichsani.com/home/">
```

Tag diatas dapat diakses menggunakan element selector "a", namun kali ini saya ingin menggunakan attribute selector :

```css
[href] {
  color: brown;
}
```

Artinya, ubah warna teks menjadi brown, untuk seluruh tag html yang memiliki attribute href.

Contoh lain :

```css
a[href] {
  color: brown;
}
```

Artinya, hanya akan mencari tag "a" yang memiliki attribut href. Yang perlu diperhatikan, antara huruf "a" dengan kurung siku tidak boleh ada space.

Selain mengakses nama attribut, kita juga bisa mengakses element HTML dari nilai attribut tersebut, contoh:

```css
[title='kota bandung'] {
  color: green;
}
```

Kita juga bisa mencari seluruh attribut title yang mengandung kata "kota", contoh:

```css
[title~='kota'] {
  color: green;
}
```

Jika kita ingin mencari attribut yang mengandung kata "ba", ini tidak bisa dilakukan dengan karakter tilde (~), karena karakter ini membutuhkan pemisah spasi. Namun kita bisa menggunakan karakter bintang (\*), contoh:

```css
[title*='ba'] {
  color: green;
}
```

Untuk mencari attribut berdasarkan posisi, bisa menggunakan karakter pangkat "^" dan dollar "\$". Karakter "^" akan mencari diawal attribut, sedangkan karakter "\$" akan mencari di akhir attribut.

Misal, untuk menyeleksi hanya attribut href yang diawali dengan karakter https, bisa menggunakan selector berikut:

```css
[href^='https'] {
  color: green;
}
```

Attribut selector sangat powerfull karena bisa dipakai untuk menyeleksi struktur HTML dengan detail. Pada proses desain form HTML, selector ini sangat membantu.

Struktur form HTML yang sebagian besar menggunakan tag `input` hanya dibedakan berdasarkan attribut `type`. Misalnya, untuk mencari seluruh checkbox bisa memakai attribut selector: `input[type="checkbox"]`.

## Group Selector

---

Group selector bukanlah selector murni, namun sebuah sebutan untuk cara menggabungkan beberapa selector kedalam satu perintah, contoh:

```css
h1,
h2,
p {
  color: red;
}
```

Penggunaan group selector juga bisa digunakan untuk menyatukan selector lain, contoh:

```css
.judul-utama,
#headerKedua,
[title~='serius'] {
  color: purple;
}
```

## Element Spesific Selector

---

Element spesific selector juga berupa penggabungan beberapa selector untuk membuat selector yang lebih spesific, contoh:

```css
/* contoh 1 */
h2.judul {
  color: purple;
}

/* contoh 2 */
p#penting {
  color: yellow;
}

/* contoh 3 */
p.pesan,
h2#judul,
span[title] {
  color: blue;
}
```

## Descendent Selector

---

Adalah sebutan untuk selector yang mencari tag HTML berdasarkan "parent-child relationship". Dalam DOM (Document Objek Model), setiap tag bisa menjadi parent dan child.

Agar dapat menggunakan descendent selector, kita harus paham bagaimana strutktur HTML yang ada. Jika tidak, maka tidak akan bisa menggunakan descendent selector.

Contoh:

```css
div h2 {
  color: red;
}
```

Perintah diatas akan mengubah warna teks menjadi merah untuk setiap tag `h2` yang berada di dalam tag `div`.

## Child Selector

---

Mirip dengan descendent selector, child selector menggunakan struktur DOM dan parent child relationship. Bedanya, child selector hanya akan mencari tag HTML yang menjadi anak pertama (first child) dari struktur DOM.

Contoh:

```css
div > p {
  color: green;
}
```

Penulisan tanda ">" pada child selector boleh dipisah dengan spasi ataupun tanpa spasi.

Contoh lain:

```css
ol ul > li {
  color: red;
}
```

Artinya, ubah warna teks menjadi merah untuk tag `li` yang merupakan first child dari tag `ul`, dimana tag `ul` harus berada di dalam tag `ol`.

## Adjacent Selector

---

Adjacent selector masih berhubungan dengan struktur DOM, kali ini yang akan disinggung adalah sibling relationship (hubungan saudara).

Adjacent selector bisa dipakai untuk mencari tag HTML berdasarkan sibling relationship dan harus saling berdekatan.

Contoh:

```css
h2 + p {
  color: purple;
}
```

Artinya, cari 1 tag `p` yang berada setelah tag `h2` dan merupakan sibling (saudara).

## General Sibling Selector

---

General sibling selector mirip dengan adjacent selector. Bedanya, pada adjacent selector hanya cocok dengan satu tag yang menjadi sibling, sedangkan general sibling selector akan cocok dengan seluruh sibling.

Contoh:

```css
h2 ~ p {
  color: purple;
}
```

Artinya, cari seluruh tag `p` yang berada setelah tag `h2` dan merupakan sibling.

## Dynamic Pseudo Class Selector

---

Pseudo class selector adalah selector yang digunakan untuk mencari element HTML yang tidak terlihat secara langsung (tidak ada didalam struktur DOM). Penulisannya diawali dengan titik dua, contoh: `:hover, :active, :visited`.

Selector ini diapakai untuk mencari struktur HTML berdasarkan suatu hal yang berubah karena interaksi user. Terdapat beberapa jenis dynamic pseudo class selector dalam CSS, diantaranya:

- `:link`
- `:visited`
- `:hover`
- `:active`
- `:target`
- `:focus`

## UI Element State Pseudo Class Selector

---

Adalah jenis selector CSS yang dipakai untuk mencari element HTML berdasarkan kondisi dari element tersebut. Umumnya digunakan untuk element form HTML.

Selector ini terdiri dari tiga jenis, yaitu :

- `:disabled`
- `:enabled`
- `:checked`

## Structured Pseudo Class Selectors

---

Selector ini diapakai untuk menemukan element HTML yang cukup kompleks dimana selector biasa tidak bisa digunakan. Dalam beberapa hal kita juga bisa melakukan pencocokan pola (pattern matching) untuk mencari element HTML.

Berbeda dengan dynamic pseudo selector, structural pseudo class selectors tetap mencari element HTML yang ada di dalam struktur DOM.

8 jenis structural pseudo class selectors:

- `:first-child`
- `:last-child`
- `:first-of-type`
- `:last-of-type`
- `:nth-child()`
- `:nth-last-child()`
- `:nth-of-type()`
- `:nth-last-of-type()`
- `:not`

**:first-child** dan **:last-child** digunakan untuk mencari first child dan last child dari struktur DOM.

Contoh :

```css
li:first-child {
  background-color: magenta;
}
li:last-child {
  background-color: aqua;
}
```

**:first-of-type** dan **:last-of-type** hampir mirip dengan selector `:first-child` dan `:last-child`. Bedanya, kali ini ada tambahan bahwa element HTML tersebut harus menjadi first child dari tipenya sendiri.

Jadi walaupun sebuah tag tidak berada di posisi pertama, tapi selama itu adalah yang pertama dari jenisnya sendiri, tetap akan ditangkap oleh selector `:fist-of-type`.

Contoh :

```css
p:first-of-type {
  color: red;
}
```

**:nth-child()** dan **:nth-last-child()** adalah tempat bagi angka yang dipakai untuk mencari tag HTML berdasarkan urutannya atau pola tertentu. Ini mirip seperti argument function pada bahasa pemrograman.

Selain angka, bisa juga menulis keyword khusus seperti "odd" atau "even", serta pola matematis seperti penambahan.

Berikut penjelasan beberapa contoh pola untuk selector `:nth-child()`:

- `li:nth-child(2)`: cari tag `li` yang berada pada urutan kedua dalam sebuah parent element.
- `li:nth-child(even)`: cari tag `li` yang berada pada urutan genap (even) dalam sebuah parent element.
- `li:nth-child(odd)`: cari tag `li` yang berada pada urutan ganjil (odd) dalam sebuah parent element.
- `li:nth-child(2n+1)`: cari tag `li` yang berada pada urutan pertama, kemudian 2 tag setelahnya hingga akhir. Hasilnya seperti `:nth-child(odd)`.
- `li:nth-child(2n+0)`: cari tag `li` yang berada pada urutan 0, kemudian 2 tag setelahnya secara berulang hingga akhir. Hasilnya seperti `:nth-child(even)`.
- `li:nth-child(4n-3)`: cari tag `li` yang berada pada setiap perulangan ke 4, tapi mulai dari tag kedua.

**:not()** cukup unik, yakni berfungsi untuk mencari element HTML selain yang ditulis. Selector ini juga dikenal dengan negation pseudo-class selector.

Contoh:

```css
p:not(.tes) {
  color: red;
}
```

## Pseudo Element Selector

---

Selector ini berfungsi menyeleksi konten atau isi element daripada struktur HTML. Pseudo element juga memiliki fitur generated content, dimana kita bisa menambah sesuatu ke dalam HTML menggunakan CSS.

Berikut 4 jenis pseudo element selector:

- `::first-line`
- `::first-letter`
- `::before`
- `::after`

**::first-line** dipakai untuk mengakses baris pertama dari sebuah element HTML :

```css
p::first-line {
  color: green;
}
```

**::first-letter** dipakai untuk mengakses huruf pertama dari sebuah element. Dengan :first-letter, kita bisa membuat efek drop cap:

```css
p::first-letter {
  color: red;
  font-size: 2em;
}
```

**::before** dan **::after** dikenal juga sebagai selector generated content. Dengan selector ini kita bisa menyisipkan kontent di awal atau akhir struktur HTML.

Contoh :

```css
a::before {
  content: 'Sejarah';
}

a::after {
  content: ' (Sejarah dan perkembangannya)';
}
```

CSS3 menyediakan beragam fitur lain untuk generated content, misalnya menyisipkan gambar, mengambil nilai atribut hingga membuat nomor urut yang dihasilkan dari CSS.

Untuk mengambil nilai attribut, kita bisa menggunakan property `content:attr(nama_attribut)`. Misalnya untuk mengambil alamat link dari sebuah tag `a`, bisa menggunakan property `content:attr(href)`.

Contoh:

```css
a::after {
  content: attr(href);
}

a::after {
  content: ' (' attr(href) ') ';
  color: purple;
}
```

Sebagai contoh terakhir, kita bisa menggunakan nilai property `counter` dan `counter-increment` untuk menghasilkan nomor urut dari sebuah element HTML.

Contoh:

```css
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link href="css/style.css" rel="stylesheet" />
    <style>
      h3::after {
        content: ' ke - ' counter(nourut);
      }
      h3 {
        counter-increment: nourut;
      }
    </style>
  </head>
  <body>
    <h3>Judul</h3>
    <h3>Judul</h3>
    <h3>Judul</h3>
  </body>
</html>
```
