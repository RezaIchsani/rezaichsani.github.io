---
title: 'Cascade, Inheritance & Specificity'
date: 2023-11-22
draft: false
weight: 1
categories: ['Programming', 'CSS']
tags: ['CSS']
---

## "Cascade" dari Cascading Style Sheet

---

Konsep cascading dari CSS memiliki aturan mengenai style mana yang layak di prioritaskan. Berikut urutan prioritas style pada CSS dimulai dari yang paling kuat:

- User style
- Inline style
- Internal style dan eksternal style
- Web browser style

## Inheritance Style CSS

---

Inheritance atau penurunan adalah konsep dimana sebuah style bisa diturunkan dari parent kepada child element.

Contoh:

```css
body {
  color: green;
}
```

Kode diatas akan merubah seluruh text yang berada di dalam `body` menjadi warna hijau.

## Specificity Selector

---

Specificity adalah metode perhitungan nilai untuk menentukan selector mana yang akan di dahulukan.

Sesuai dengan namanya, semakin spesifik atau semakin detail sebuah selector, akan semakin tinggi nilainya.

| **Jenis Selector**      | **Contoh**           | **Nilai Specificity** |
| ----------------------- | -------------------- | --------------------- |
| Inline style            | `style="color:blue"` | 1000                  |
| id selector             | `\#paragrafPertama`  | 100                   |
| class selector          | `.paragraf`          | 10                    |
| attribute selector      | `[href]`             | 10                    |
| pseudo-class selector   | `:link`              | 10                    |
| element selector        | `p`                  | 1                     |
| pseudo-element selector | `::first-line`       | 1                     |
| universal selector      | `*`                  | 0                     |

Untuk selector gabungan seperti group selector, adjacent selectors atau child selectors. Nilai specificitynya dihitung dengan menambahkan setiap selector yang ada :

| **Selector**            | **Jenis Selector**                  | **Nilai Specificity** |
| ----------------------- | ----------------------------------- | --------------------- |
| `body #paragrafPertama` | element + id                        | 1 + 100 = 101         |
| `p.paragraf`            | element + class                     | 1 + 10 = 11           |
| `div > p`               | element + element                   | 1 + 1 = 2             |
| `h2 + p`                | element + element                   | 1 + 1 = 2             |
| `ul ol+li`              | element + element + element         | 1 + 1 + 1 = 3         |
| `ul ol li.red`          | element + element + element + class | 1 + 1 + 1 + 10 = 13   |
| `body #myID .red`       | element + id + class                | 1 + 100 + 10 = 111    |

## Keyword Sakti: `!important`

---

`!important` digunakan untuk menyelesaikan konflik antar selector CSS. Dengan menambah perintah `!important` sebuah property CSS akan memiliki prioritas paling tinggi dan hanya bisa dikalahkan oleh perintah `!important` lain yang lebih spesifik.

> Secara teknis, `!important` bekerja pada level declaration (property), bukan di dalam selector specificity. Nilai prioritas 1000 ini cuma sekedar gambaran betapa tingginya efek prioritas dari `!important`.

Dalam prakteknya, keyword `!important` sebaiknya hanya digunakan sebagai jalan terakhir. Karena perintah `!important` membuat konsep cascading, inheritance dan specificity menjadi tidak berdaya.
