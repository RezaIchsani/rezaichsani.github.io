---
title: 'CSS Flexbox'
date: 2023-09-18
draft: false
weight: 1
categories: ['Programming']
tags: ['CSS']
---

## Flex Container

Untuk menggunakan flexbox, sebuah element harus berada didalam sebuah "flex container". Caranya dengan menambah property `display: flex` atau `display: inline-flex` ke dalam parent element.

Contoh :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CSS Flexbox</title>
    <style>
      .container {
        height: 150px;
        border: 2px solid #965e15;
        background-color: #aae3a7;
        margin-top: 1em;
      }
      .box {
        background-color: Honeydew;
        margin: 0.3em;
        padding: 0.3em;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <div class="box">box 1</div>
      <div class="box">box 2</div>
      <div class="box">box 3</div>
    </div>
    <div class="container" style="display: flex">
      <div class="box">box 1</div>
      <div class="box">box 2</div>
      <div class="box">box 3</div>
    </div>
    <div class="container" style="display: inline-flex">
      <div class="box">box 1</div>
      <div class="box">box 2</div>
      <div class="box">box 3</div>
    </div>
  </body>
</html>
```

## Jenis-jenis Flexbox Property

Property untuk flexbox dapat dibagi menjadi 2 kelompok, yakni property untuk flex container, dan property untuk flex item.

Flex container adalah element yang menampung semua flex item. Property yang ditulis kedalam flex container akan berpengaruh secara global.

Sedangkan flex item adalah sebutan dari setiap child element yang berada di dalam flex container.

Pada kode HTML diatas, box 1, box 2 dan box 3 adalah flex item.

**Property untuk flex container:**

- `flex-direction`
- `flex-wrap`
- `flex-flow` _shorthand_
- `justify-content`
- `align-items`
- `align-content`

**Property untuk flex item:**

- `order`
- `flex-grow`
- `flex-basis`
- `flex` _shorthand_

## Property flex-direction

Property flex-direction digunakan untuk mengatur urutan dan posisi element yang terdapat di dalam flex-container. Nilai yang bisa diisi adalah `row` (default), `row-reverse`, `column` dan `column-reverse`.

Contoh :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Flex Direction</title>
    <style>
      .container {
        height: 150px;
        border: 2px solid #965e15;
        background-color: #aae3a7;
        margin-top: 1em;
        display: flex;
      }
      .box {
        background-color: Honeydew;
        padding: 0.3em;
        margin: 0.3em;
      }
    </style>
  </head>
  <body>
    <div class="container" style="flex-direction: row">
      <div class="box">box 1</div>
      <div class="box">box 2</div>
      <div class="box">box 3</div>
    </div>
    <div class="container" style="flex-direction: row-reverse">
      <div class="box">box 1</div>
      <div class="box">box 2</div>
      <div class="box">box 3</div>
    </div>
    <div class="container" style="flex-direction: column">
      <div class="box">box 1</div>
      <div class="box">box 2</div>
      <div class="box">box 3</div>
    </div>
    <div class="container" style="flex-direction: column-reverse">
      <div class="box">box 1</div>
      <div class="box">box 2</div>
      <div class="box">box 3</div>
    </div>
  </body>
</html>
```

## Property flex-wrap

Property `flex-wrap` digunakan untuk menentukan apakah flex item diizinkan membuat baris baru jika flex container tidak cukup lebar.

Nilai yang bisa di isi adalah `nowrap` (default), atau `wrap`.

Property ini hanya berefek jika **flex container** di set dengan `flex-direction: row` atau `flex-direction: row-reverse` saja, dan akan diabaikan untuk `flex-direction: column` serta `column-reverse`.

Contoh :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Flex Wrap</title>
    <style>
      .container {
        height: 150px;
        border: 2px solid #965e15;
        background-color: #aae3a7;
        margin-top: 1em;
        display: flex;
        flex-direction: row;
      }
      .box {
        background-color: Honeydew;
        margin: 0.3em;
        padding: 0.3em;
      }
    </style>
  </head>
  <body>
    <div class="container" style="flex-wrap: nowrap">
      <div class="box">box 1</div>
      <div class="box">box ..</div>
      <div class="box">box 10</div>
    </div>
    <div class="container" style="flex-wrap: wrap">
      <div class="box">box 1</div>
      <div class="box">box ..</div>
      <div class="box">box 10</div>
    </div>
  </body>
</html>
```

Jika **flex container** di set dengan `flex-wrap: nowrap`, maka **flex item** akan terus diperkecil, sedangkan untuk `flex-wrap: wrap`, **flex item** akan pindah ke bawah membentuk baris baru.

Selain itu, apabila lebar **flex item** di set langsung dengan property `width`, pengaturan `flex-wrap: nowrap` akan menganggap `width` tersebut sebagai `max-width` dan masih bisa "dipaksa" untuk mengecil.

## Property flex-flow
