---
title: 'Cara Unzip File di Linux dengan Command Line'
date: 2024-01-02
draft: false
weight: 1
categories: ['CLI']
tags: ['Linux']
---

Mengextract file .zip dengan Command Linux cukup mudah dengan perintah `unzip` :

- Unzip file didalam folder yang sama.

```
unzip file.zip
```

atau 

- Unzip file ke tempat lain yang berbeda.

```
unzip file.zip -d /var/www/
```

Contoh 

```
unzip wordpress.org -d /opt/lampp/htdocs/
```

Setelah itu, kita bisa merename folder aslinya dengan perintah:

```
mv wordpress octavia
```

Perintah tersebut akan merename folder "wordpress" menjadi "octavia".