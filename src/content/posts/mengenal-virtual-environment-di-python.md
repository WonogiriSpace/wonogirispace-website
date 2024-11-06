---
title: "Mengenal Virtual Environment di Python"
description: "Apa itu virtual environment di python"
date: 2024-11-06
image: "/images/posts/virtual-environment.png"
categories: ["python", "software development", "application development"]
authors: ["afrijaldz"]
tags: ["python"]
draft: false
---

Python pada dasarnya akan secara default terinstall di OS yang kita gunakan. Python yang sudah terinstall itu digunakan oleh sistem kita untuk menjalankan aplikasi - aplikasi bawaan.

Saat kita ingin mengembangkan sebuah aplikasi dengan Python diperlukan sebuah virtual environment. Mengapa butuh itu? karena bisa saja module yang kita gunakan akan berbeda versi dengan apa yang sudah ada di sistem kita yang sudah terinstall secara global.

Anggap saja di sistem kita sudah terinstall module A dengan versi 2.0.0, namun saat kita ingin mengembangkan suatu aplikasi membutuhkan module A versi 4.5.9, jika kita menggunakan module global aplikasi kita ga jalan dan harus diupgrade versinya, namun ketika kita upgrade versinya, akan merusak tatanan dunia.

Oleh sebab itu kita membutuhkan sebuah tempat khusus yang terisolasi dengan sistem, itu yang dinamakan virtual environment.

Dengan virtual environment, kita bisa menggunakan versi python, pip, dan module - module yang kita butuhkan sesuai kebutuhan aplikasi, tanpa merusak tatanan dunia. Karena terisolasi.

Ibaratnya, jika di sistem operasi kita terinstall `python@3.5` kita bisa menggunakan `python@3.13` di virtual environment dan menginstall module dengan versi terbaru.

Kita cukup memasang virtual environment di directory yang diinginkan.

Misal kita punya directory `project-monitoring-gunung-slamet` dan kita ingin mengembangkan aplikasi dengan python di directory tersebut, sehingga kita perlu memasang virtual environment di directory tersebut.

Ada dua cara untuk memasangnya, yaitu dnegan module `venv` atau dengan `uv`

##### venv

Untuk memasang virtual environment dengan `venv` kita cukup mengetikkan

```sh
# di dalam directory `project-monitoring-gunung-slamet`

python3 -m venv .venv
```

Kita menggunakan python3 (bawaan) untuk menjalankan module `venv` membuat virtual environment bernama `.venv`

##### uv

Pastikan `uv` sudah terinstall, jika belum kamu bisa menginstallnya dengan [Homebrew](https://brew.sh).

```sh
brew install uv
```

jika `uv` sudah terinstall, untuk membuat virtual environment menggunakan

```sh
uv venv
```

Nama `.venv` adalah lazimnya penamaan virtual environment, kamu bisa mengubahnya dengan apa saja.

Untuk mengaktifkan virtual environmentnya, kita bisa melakukan

```sh
source .venv/bin/activate
```

dan untuk mengecek apakan virtual environment tersebut sudah aktif / sedang digunakan bisa menggukanan

```sh
which python
```

Jika python mengarahkan ke direktori dimana virtual environment tersebut berada, maka virtual environment sudah aktif.

Untuk menonaktifkan virtual environment sendiri, kita bisa menggunakan perintah 

```sh
deactivate
```

Misal kamu sedang membangun aplikasi dengan python lebih dari satu, pastikan ketika kamu berpindah-pindah project selalu mengecek virtual environment mana yang aktif. Karena jika tidak, ketika salah environment maka module yang digunakan dan bila menginstall module baru akan menggukanan environment yang sedang aktif.

Untuk membuat virtual environment, aku sendiri prefer menggunakan `uv` karena dengan `uv` selain untuk membuat virtual environment tersebut lebih singkat, tapi dengan `uv` sudah terdapat `pip` dengan versi terbaru.

Jika menggunakan `venv` kita perlu mengupdate versi pipnya terlebih dahulu.

Selain itu directory `.venv` sudah otomatis terdapat file `.gitignore` untuk mencegah directory tersebut ikut terpush ke git repository.

Untuk menggunakan `pip` di `uv` kita bisa menggunakannya dengan `uv pip`.

misal saat kita ingin ngefreeze module untuk disimpan ke dalam file `requirements.txt`, maka kita bisa menggunakan

```sh
uv pip freeze > requirements.txt
```

begitu juga saat mau menginstall module

```sh
uv pip install -r requirements.txt
```

atau 

```sh
uv pip install [nama-module]
```

Sebagai tambahan, jika kamu menemukan suatu module yang tidak bisa diinstall atau package registry dari module itu tidak ditemukan dengan pip dari virtual environment, kamu bisa menginstallnya dengan `brew`.

Contohnya saat kamu mau menginstall module `python-tkinter`. Kamu tidak akan bisa mengintallnya dengan `uv pip install tkinter`, begitu pula dengan `pip` global.

Tapi kamu bisa menginstall module itu dengan `brew`

```sh
brew install python-tkinter
```
