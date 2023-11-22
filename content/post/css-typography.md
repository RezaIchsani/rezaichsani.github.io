---
title: 'CSS Typography'
date: 2023-11-22
draft: false
weight: 1
categories: ['Programming', 'CSS']
tags: ['CSS']
---

Typography adalah sebuah seni mengatur huruf / teks untuk membuatnya lebih mudah dibaca dan menarik secara visual.

## Property `font-family`

---

Nilai dari property `font-family` adalah nama font yang ingin digunakan, contoh:

```css
p {
  font-family: Arial;
}
```

Property ini akan mencari font di dalam komputer client (pengunjung web kita) bukan di dalam komputer server.

Untuk mengantisipasi tidak tersedianya sebuah font, kita bisa menulis alternatif nama font pengganti, contoh:

```css
p {
  font-family: Arial, Helvetica, sans-serif;
}
```

Khusus untuk font yang terdiri dari beberapa kata atau mengandung spasi, harus ditulis dalam tanda kutip, contoh:

```css
p {
  font-family: 'Times New Roman', Georgia, serif;
}
```

## Property `font-size`

---

CSS menyediakan beragam satuan untuk mengatur ukuran font, yang semuanya di set melalui `font-size`, contoh:

```css
p {
  font-size: 14px;
}
```

Property `font-size` dan berbagai property CSS yang lain butuh nilai dalam satuan length, yakni satuan panjang seperti pixel, cm, mm, em ataupun persen.

Secara garis besar, nilai satuan _length_ dikategorikan dalam 2 kelompok: nilai absolut dan nilai relatif.

**Nilai Absolut** adalah satuan length yang nilainya tetap dan tidak terpengaruh oleh element di sekelilingnya. Contohnya ialah pixel (px), cm, mm, point (pt), inches (in) dan pica (pc).

**Nilai Relatif**, adalah nilai yang berubah-ubah tergantung posisi dan parent elementnya. Contoh dari satuan ini adalah persen (%), em dan rem.

#### Satuan Persen (%)

```css
p {
  font-size: 120%;
}
```

Kode tersebut akan mencari seluruh tag `p` kemudian men-set ukurannya sebesar 120% dari ukuran font-size parent elementnya. Jika ukuran font-size parent elementnya tidak di set, maka teks akan tampil dengan ukuran 19.2 px.

Angka 19.2 px didapat dari ukuran default font-size dari tag `body`, yakni 16 px. Sehingga angka 120% \* 16 = 19.2 px.

Yang perlu diperhatikan dari satuan persen adalah, nilai persen ini bisa terakumulasi, contoh:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      body {
        font-size: 16px;
      }
      div {
        font-size: 110%;
      }
    </style>
  </head>
  <body>
    <div>
      Child element 1
      <div>
        Child element 2
        <div>
          Child element 3
          <div>Child element 4</div>
        </div>
      </div>
    </div>
  </body>
</html>
```

Pada kode diatas, terdapat tag div didalam tag div, sehingga hasilnya tag div pertama memiliki ukuran 17.6 px dan tag div terdalam akan memiliki ukuran 23.43px yang didapat dari 110% _ 110% _ 110% _ 110% _ 16px = 23.43px.

#### Satuan Em

Satuan em berasal dari istilah typography media cetak yang merujuk pada tinggi karakter `m` pada suatu font. Dalam CSS, em sangat mirip seperti %, dimana hasilnya juga dihitung berdasarkan nilai parent element.

Nilai dari 1em sama dengan 100%, sehingga 1.2em sama dengan 120%, dst. Seperti halnya persen, satuan em juga bersifat akumulatif, contoh:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      body {
        font-size: 16px;
      }
      div {
        font-size: 1.1em;
      }
    </style>
  </head>
  <body>
    <div>
      Child element 1
      <div>
        Child element 2
        <div>
          Child element 3
          <div>Child element 4</div>
        </div>
      </div>
    </div>
  </body>
</html>
```

**Apa bedanya % dengan em?**

Saat satuan em dan % dipakai untuk `font-size` keduanya nyaris tidak berbeda. Namun ketika diterapkan pada property lain seperti lebar dan tinggi element (width & height) maka keduanya akan terlihat berbeda.

Ketika menggunakan nilai % untuk lebar sebuah element (menggunakan property width), lebar itu dihitung dari width parent elementnya. Sedangkan jika kita menggunakan nilai em, lebar element akan dihitung berdasarkan nilai `font-size` parent elementnya.

#### Satuan Rem

Rem merupakan singkatan dari "root em", artinya rem bergantung pada "root element". Di dalam struktur DOM HTML, root element ini adalah tag `html`.

Ketika membuat `font-size: 1.2rem` artinya ukuran font-size itu diset sebesar 120% dari ukuran font-size tag `html`, tidak peduli dimana paragraf tersebut berada. Artinya tidak ada efek akumulasi pada satuan rem.

Selain diisi dengan satuan angka, font-size juga bisa di isi dengan keyword, berikut satuan keyword absolut untuk property font-size:

- `xx-small`
- `x-small`
- `small`
- `medium`
- `large`
- `x-large`
- `xx-large`

Untuk ukuran relatif terdapat 2 nilai, yakni `smaller` dan `larger`.

## Property `color`

---

Penggunaan property color dan background-color sangat mudah, contoh :

```css
h1,
p {
  color: White;
  background-color: Black;
}
```

#### Satuan Color CSS

CSS mendukung setidaknya 4 notasi penulisan warna :

- `keyword`, contoh : white, purple, black, dll.
- `#RRGGBB` / `#RGB`, contoh : \#FFFFFF, #000000, dll
- `rgb(rr, gg, bb)` / `rgba(rr, gg, bb, aa)`, contoh : `rgb(255,0,255)`.
- `hsl(hh, ss, ll)` / `hsla(hh, ss, ll, aa)`, contoh : `hsl(300,100%,50%)`.

## Property `font-weight`

---

Property `font-weight` bertujuan untuk menebalkan teks (bold). Nilai untuk property ini bisa berupa angka 100, 200, 300 sampai 900 serta nilai berupa keyword seperti normal, bold, bolder dan lighter.

Perlu diketahui, bahwa nilai-nilai tersebut bisa digunakan jika font yang dipakai juga mendukungnya. Namun kebanyakan font hanya mendukung teks normal atau bold saja.

Contoh penggunaan font-weight :

```css
h1 {
  font-weight: 700;
}
p {
  font-weight: bold;
}
```

## Property `font-style`

---

Property `font-style` berfungsi untuk memringkan teks (italic), nilai yang bisa diinput adalah normal, italic dan oblique, contoh:

```css
p {
  font-style: italic;
}
```

## Property `text-decoration`

---

Property `text-decoration` digunakan untuk membuat dekorasi teks, seperti garis bawah, atas atau garis tercoret.

Nilai untuk property ini adalah salah satu dari keyword underline, overline, line-through dan none. Kita juga bisa menggunakan 2 atau lebih efek dekorasi sekaligus, contoh:

```css
.satu {
  text-decoration: underline;
}
.dua {
  text-decoration: underline overline;
}
```

Warna garis yang muncul akan menyesuaikan dengan warna teks.

Pada CSS3, kita bisa mengatur warna dan jenis garis. Untuk melakukannya, property `text-decoration` dipecah menjadi 3 property baru :

- `text-decoration-line` untuk mengatur posisi garis.
- `text-decoration-style` untuk mengatur jenis garis.
- `text-decoration-color` untuk mengatur warna garis.

Contoh:

```css
.satu {
  text-decoration-line: underline;
  text-decoration-style: solid;
  text-decoration-color: purple;
}
```

Untuk menyederhanakan penulisan, kita bisa menulisnya secara singkat (shorthand), contoh:

```css
.satu {
  text-decoration: underline solid puprle;
}
```

## Property `text-transform`

---

Property `text-transform` dapat diisi dengan salah satu keyword: capitalize, uppercase, lowercase, atau none, contoh :

```css
.satu {
  text-transform: capitalize;
}
```

## Property `font-variant`

---

Property `font-variant` dipakai untuk membuat variasi font, tetapi nilai yang didukung saat ini hanya ada 2: `small-caps` dan `normal`.

Contoh:

```css
.satu {
  font-variant: small-caps;
}
```

## Property `text-align`

---

Property `text-align` memiliki beberapa nilai, diantaranya adalah: left, center, right, dan justify.

Contoh:

```css
.satu {
  text-align: center;
}
```

## Property `line-height`

---

Property `line-height` digunakan untuk mengatur line spacing. Nilai dari property ini bisa diisi dengan berbagai satuan length, seperti px, em, persen, bahkan tanpa satuan (hanya angka).

Misalnya, `line-height: 140%` maka web browser akan mengatur tinggi baris 140% dari ukuran teks saat ini (diambil dari property font-size).

Jika diisi dengan nilai angka saja, seperti `line-height: 1.9` artinya tinggi teks akan di set 1.9 kali ukuran font saat ini.

Contoh:

```css
.satu {
  line-height: 1.2em;
}
```

## Property `margin-bottom`

---

Property `margin-bottom` digunakan untuk mengatur jarak (spasi) antar paragraf (dan juga element lain). Nilai yang bisa diisi adalah semua satuan length seperti px, em, dan juga persen (%).

Contoh:

```css
* {
  margin: 0; /* menghapus margin bawaan web browser */
}
.satu {
  margin-bottom: 1.8em;
}
```

> Property `margin-bottom` sebenarnya bagian dari konsep Box Model.

## Property `letter-spacing` & `word-spacing`

---

Property `letter-spacing` & `word-spacing` digunakan untuk mengatur jarak antar huruf dan kata. Property ini bida diisi satuan px, em atau rem dan juga bisa bernilai negatif.

Contoh:

```css
.satu {
  letter-spacing: 5px;
  word-spacing: 0.1em;
}
```

## Property `text-indent`

---

Indentasi adalah sebutan untuk baris pertama paragraf yang menjorok ke arah dalam. Umumnya indentasi dipakai dalam tulisan formal. Dalam CSS pengaturan indentasi bisa dilakukan dengan property `text-indent`.

Contoh:

```css
p {
  text-indent: 40px;
}
```

## Font Shorthand Notation

---

Shorthand notation adalah property khusus yang berisi gabungan dari berbagai property lain. Property `font` bisa dipakai untuk menyingkat penulisan 6 property sekaligus, yakni:

- `font-style`
- `font-variant`
- `font-weight`
- `font-size`
- `line-height`
- `font-family`

Penulisan property font harus mengikuti urutan ini, namun tidak semuanya harus ditulis, contoh penulisan property font:

```css
/* size | family */
font: 2em 'Open Sans', sans-serif;

/* style | size | family */
font: italic 2em 'Open Sans', sans-serif;

/* style | variant | weight | size/line-height | family */
font: italic small-caps bolder 16px/2 cursive;
```

## Property `text-shadow`

---

Efek `text-shadow` menyediakan 4 pilihan pengaturan: `offset-x`, `offset-y`, `blur-radius` dan `color`.

Nilai minimal yang harus di setakan pada property `text-shadow` adalah offset-x dan offset-y.

Nilai offset-x berfungsi untuk mengatyr seberapa jauh bayangan yang dihasilkan dari teks asli ke arah sumbu x (horizontal), sedangkan offset-y ke arah sumbu y (vertical).

Satuan yang bisa diinput berupa nilai length seperti px, em atau rem. Nilainya juga bisa positif atau negatif, dan akan menentukan arah bayangannya.

Contoh:

```css
.satu {
  text-shadow: -10px 2px;
}
.dua {
  text-shadow: 5px 0px red;
}
.tiga {
  text-shadow: blue -10px 0px 10px;
}
```

## Mengenal CSS Vendor Prefix

---

Apa kegunaan dari vendor prefix?, CSS3 dikembangkan dengan konsep modul. Dengan demikian, property-property baru bisa hadir dengan lebih cepat.

Untuk mengimbanginya, web browser modern juga berupaya mendukung property baru ini, bahkan ketika property tersebut belum resmi selesai (masih dalam tahap draft di w3C).

Property yang belum selesai ini diimplementasikan oleh web browser dengan menggunakan vendor prefix. Sehingga, kita sebagai web designer bisa menguji coba property tersebut.

Penulisan vendor prefix sesuai dengan inisial web browser atau layout engine yang digunakan.

Berikut adalah awalan vendor prefix pada web browser:

- `-webkit-` (Chrome, dan versi terbaru dari Operasi)
- `-moz-` (Firefox)
- `-o-` (Opera versi lama)
- `-ms-` (Internet Explorer)

Contoh penggunaan vendor prefix untuk membuat efek text shadow:

```css
.satu {
  -webkit-text-shadow: 2px 2px 5px red;
  -moz-text-shadow: 2px 2px 2px red;
  -o-text-shadow: 2px 2px 2px red;
  -ms-text-shadow: 2px 2px 2px red;
  text-shadow: 2px 2px 2px red;
}
```
