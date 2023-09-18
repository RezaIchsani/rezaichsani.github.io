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
