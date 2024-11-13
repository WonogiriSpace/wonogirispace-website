---
title: "Menggunakan environment variable di Python"
description: "Menggunakan .env di python dengan pydantic settings"
date: 2024-11-13
image: ""
categories: ["python", "software development", "application development"]
authors: ["afrijaldz"]
tags: ["python"]
draft: false
---

Environment variable biasanya digunakan untuk menyimpan data-data yang sensitif untuk suatu project. Biasanya disimpan di file `.env` dan tidak ikut dipush ke repository.

Di python sendiri ada beberapa cara untuk mengambil virtual environment, salah satu dari salah duanya dengan menggunakan `os`

```python
import os

name = os.getenv("MY_NAME")
```

Cara tersebut aku hindari karena `environment variable` yang diambil adalah `env` dari `os` / `operating system` yang disimpan di dalam `$PATH` variable. Selama project yang aku kerjakan tidak membutuhkan `variable` dari sistem operasi maka aku rasa tidak perlu menggunakan itu, aku merasa kotor aja karena harus menambahkan `variable` ke dalam sistem operasi untuk suatu project dan tidak digunakan di banyak project (misal hanya satu).

Cara keduanya, bisa menggunakan `.env` yang akan aku bahas di sini.

Untuk bisa membaca value dari `.env` kita perlu menginstall module `pydantic-settings`

```sh
pip install pydantic-settings
```

atau (jika menggunakan uv)

```sh
uv add pydantic-settings
```

Pydantic setting menyediakan fitur untuk load setting dari environment variable.

Misal kita punya file `.env` dengan value

```
# .env
POSTGRES_USER="root"
POSTGRES_PASSWORD="admin"
```

Untuk meload nilai dari `.env`

```python
# db.py
from pydantic_settings import BaseSettings, SettingsConfigDict


class Settings(BaseSettings):
    model_config = SettingsConfigDict()

    POSTGRES_USER: str
    POSTGRES_PASSWORD: str

settings = Settings()
```

Setiap key dari `.env` harus di-declare agar dapat terbaca, lalu buat variable settings untuk membuat object dari class Settings untuk keperluan export module.

Untuk menggunakannya kita bisa import module `db.py` tersebut lalu menggunakan property dari settings yang sudah kita export.

Sebagai contoh kita akan gunakan di file terpisah `main.py`

```python
# main.py
from db import settings

print(settings.POSTGRES_USER, settings.POSTGRES_PASSWORD)

```

Maka value dari `POSTGRES_USER` dan `POSTGRES_PASSWORD` yang ada di `.env` akan muncul.

Untuk melihat semua nilai dari `settings` kita bisa menggunakan `model_dump()`


```python
# main.py
from db import settings

print(settings.POSTGRES_USER, settings.POSTGRES_PASSWORD)
print(settings.model_dump())

```

Sekian semoga bermanfaat
