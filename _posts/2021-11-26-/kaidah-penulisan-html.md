---
title: Kaidah Penulisan HTML
---

## 1. Penulisan File HTML
File html adalah sebuah file dengan ekstenensi `.html`. Di dalam file ini terdapat `tag` yang digunakan untuk penanda dalam membuat tampilan antar muka website. Contoh penulisan file html adalah sebagai berikut:

```html
<html>
</html>
```

Jika diperhatikan, terdapat tag `<html>` dan `</html>`. Tag ini disebut sebagai tag `berpasangan`. Ada tag pembuka `<nama_tag>` dan tag penutup `</nama_tag>`.

Perhatikan ilustrasi dibawah berikut!

```
<html>      <---+
                |
   ( isi )      | (Penanda HTML)
                |
</html>     <---+
```
{:.alert.alert-success}

Setiap tag yang berpasangan harus ditulis dengan format di atas. Karna itu berfungsi sebagai penanda/marking pada browser. Sehingga browser dapat mengetahui mulai darimana dan sampai mana element harus di Render.
{:.alert.alert-success}

## 2. Komponen di dalam file tag HTML

Di dalam tag `html` terdapat 2 komponen yaitu `head` dan `body`. Tag `head` digunakan untuk menyimpan informasi halaman dan tag `body` digunakan untuk menyimpan konten website.

untuk penulisan struktur tag `head` dan `body` dapat dilihat di bawah ini:

```html
<html>
    <head></head>
    <body></body>
</html>
```

Penjelasan dari struktur tag `head` dan `body`:

```
<html>          <---------------------------+
                                            |
    <head>      <---+                       |
                    | (informasi halaman)   |
    </head>     <---+                       |
                                            | (Penanda HTML)
    <body>      <---+                       |
                    | (kontent)             |
    </body>     <---+                       |
                                            |
</html>         <---------------------------+
```
{:.alert.alert-success}

<div class="container-fluid border-top pt-3">
    <div class="row text-center">
        <a href="#" class="col fw-bold text-left">Back</a>
        <a href="https://mashanz.com/note/2021/11/23/belajar-dasar-html.html" class="col fw-bold">ToC</a>
        <a href="#" class="col fw-bold text-right">Next</a>
    </div>
</div>