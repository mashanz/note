---
title: Cara install Odoo 15, PostgreSQL, PgAdmin dengan Docker di semua OS
tags: Tutorial Odoo
date_update: 2021-11-26 00:00:00 +0000
---

## 1. Persiapan
Komputer yang akan di install atau server memiliki persyaratan:
- Minimum 1 Core CPU
- Minimum 1 GB Ram
- Minimum 10GB Drive

OS sudah terinstall Docker EE atau CE versi 19+. Apabila Komputer atau Server memiliki RAM kurang dari 4GB, 
disarankan jangan install Docker versi Desktop, Namun Install Docker versi CLI.
Untuk download dan instalasinya bisa lihat di [sini](https://www.docker.com/)

## 2. Konfigurasi
- Buatlah sebuah folder projek misal `projek_odoo_ku`
- buat sebuah file `docker-compose.yml` di dalam folder `projek_odoo_ku` 

```yml
version: "3.9"
services:
  # DB SERVER
  db_odoo_ku:
    image: "postgres:13"
    environment: 
      - POSTGRES_DB=${POSTGRES_DB}
      - POSTGRES_USER=${POSTGRES_USER}
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
    volumes:
      - ./docker_data/postgresql:/var/lib/postgresql/data

  # PG ADMIN
  pgadm_odoo_ku:
     image: "dpage/pgadmin4"
     environment: 
       - PGADMIN_DEFAULT_EMAIL=${PGADMIN_DEFAULT_EMAIL}
       - PGADMIN_DEFAULT_PASSWORD=${PGADMIN_DEFAULT_PASSWORD}
     volumes:
       - ./docker_data/pgadmin:/var/lib/pgadmin
     depends_on:
       - db_odoo_ku
     ports:
       - "${PGADMIN_EXPOSE_PORT}:80"

  # ODOO SERVER
  odoo_ku:
    image: "odoo:15"
    environment:
      - HOST=db_odoo_ku
      - USER=${POSTGRES_USER}
      - PASSWORD=${POSTGRES_PASSWORD}
    depends_on:
      - db_odoo_ku
    ports:
      - "${ODOO_EXPOSE_PORT}:8069"
    volumes:
      - ./addons:/mnt/extra-addons
      - ./odoo.conf:/etc/odoo/odoo.conf
      - ./docker_data/odoo:/var/lib/odoo
```

- Buat sebuah file `.env` di dalam folder `projek_odoo_ku` 

```env
POSTGRES_DB = postgres
POSTGRES_USER = odoo
POSTGRES_PASSWORD = odoo

PGADMIN_DEFAULT_EMAIL = emailku@gmail.com
PGADMIN_DEFAULT_PASSWORD = 123456

PGADMIN_EXPOSE_PORT = 8088
ODOO_EXPOSE_PORT = 8069
```

- Buat sebuah file `odoo.conf` di dalam folder `projek_odoo_ku`

```conf
[options]
addons_path = /mnt/extra-addons
admin_passwd = admin
xmlrpc_port = 8069
limit_time_cpu = 0
limit_time_real = 0
```

Apabila semua file telah dibuat, maka hirarki projek folder akan nampak seperti berikut:

```md
|- projek_odoo_ku
   |- .env
   |- docker-compose.yml
   |- odoo.conf
```

## 3. Runing Docker
masuk ke folder `projek_odoo_ku` dan jalankan perintah

```sh
docker-compose up -d
```

setelah itu, Odoo dapat dibuka di `http://localhost:8069` dan PgAdmin di halaman `http://localhost:8088`

Apabila odoo berhasil dibuka, hirarki folder akan terupdate menjadi berikut
{:.alert.alert-success}

```md
|- projek_odoo_ku           # [Folder] Project
   |- .env                  # [File] Docker Environment
   |- docker-compose.yml    # [File] Konfigurasi Docker
   |- odoo.conf             # [File] Konfigurasi Server Odoo
   |- addons                # [Folder] untuk menambahkan module baru/custom
   |- docker_data           # [Folder] penyimpanan Odoo, PgAdmin, dan PostgreSQL
```

Done 🎯
