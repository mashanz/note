---
title: Deploy Aplikasi React ke Github Pages
---

ReactJS adalah Framework frontend yang dapat digunakan untuk membuat aplikasi web.
Karena hasil build ReactJS berupa static assets, maka file nya dapat dihosting di static server seperti Github Pages.

Berikut tahapan deploy ReactJS app ke Github Pages.

## 1. Persiapkan Project ReactJS
Apabila sudah memiliki project react yang ingin di deploy, bisa lanjut ke tahap 2. Apabila belum, bisa lihat dokumentasi cara membuat react app [di sini](https://beta.reactjs.org)

## 2. Install Dependencies gh-pages
Untuk mendeploy aplikasi ke Github Pages, kita harus meng-install package `gh-pages` terlebih dahulu.
```sh
npm i gh-pages --save-dev
```
> untuk dokumentasi gh-pages, dapat dilihat [di sini](https://www.npmjs.com/package/gh-pages)
{:.alert.alert-success}

## 3. Modifikasi `package.json`
Tambahkan parameter `homepage` di dalam `package.json`
```json
...
"homepage": "usernamegithub.github.io" // atau gunakan custom domain seperti mashanz.com
...
```
Tambahkan `predeploy` dan `deploy` di parameters `script`
```json
...
"script": {
    ...
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
    ...
}
...
```
## 4. Tambahkan file `CNAME` di folder `public`
Apabila anda menggunakan domain custom, tambahkan file bernama `CNAME` di folder `public` dan isi dengan domain custom.
```
mashanz.com
```
> apabila anda tidak menggunakan domain custom, lewati tahap ini
{:.alert.alert-warning}

## 5. Eksekusi `deploy`
Jalankan script `deploy`
```sh
npm run deploy
```
script ini akan otomatis membuild aplikasi react ke dalam branch `gh-pages`
branch inilah yang akan di deploy di github pages

> push semua perubahan ke github

## 6. Deploy di github
buka github dan pilih repository react yg akan di deploy, pilih `setting > pages` kemudian pilih branch `gh-pages` dan save

lalu buka halaman usernamegithub.github.io atau domain custom untuk melihat hasil deploy aplikasi.

🔥🔥🔥