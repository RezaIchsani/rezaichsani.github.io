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
