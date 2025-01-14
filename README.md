# Sanbercode TypeScript App
## Introduction
Project akhir Sanbercode Node.Js berupa API untuk melakukan CRUD pada fitur categories, products, orders serta beberapa fitur seperti login dan register user, melihat dan edit profile user, dan upload file pada layanan cloudinary

### Public URL (Railway) 


### Fitur Utama
* Login & register user
* Edit & view user profile (memerlukan middleware autentikasi & otorisasi `(khusus view user profile)`)
* CRUD categories
* CRUD products
* CRUD orders (memerlukan middleware autentikasi)
* Mengirim invoice pada user pada saat membuat product berdasarkan email yang telah terdaftar
* Upload single & multiple file pada cloudinary

### Panduan Instalasi
* Clone repository [ini](https://github.com/blackdevelopa/ProjectSupport.git).
* Jalankan perintah `npm install` untuk menginstall semua dependencies
* Siapkan database MongoDB dengan tipe replica set (disarankan menggunakan MongoDB Atlas karena mendukung pembuatan replica set secara otomatis)
* Siapkan akun cloudinary dan simpan semua data konfigurasi yang diperlukan untuk integrasi
* Buatlah file .env dalam root folder project dan tambahkan environment variabel yang dibutuhkan add your variables. Untuk lebih jelasnya, lihat file .env.example yang disediakan di repository

### Panduan Penggunaan
* Jalankan perintah `npm run dev` untuk memulai aplikasi dalam mode development
* Jika sudah dalam tahap production, jalankan aplikasi menggunakan perintah `npm run start`
* Aplikasi akan berjalan pada port `3000` atau pada port yang telah ditentukan pada file .env
* Buka url utama `("/")` untuk melihat endpoint apa saja yang dapat digunakan atau dapat melihat keterangan pada file README.md
* Uji API menggunakan software postman

### Layanan yang digunakan
* Node.Js
* JSON Web Token (JWT)
* MongoDB
* Cloudinary

### Library

| Library   | Deskripsi             |
| ---      | ---                   |
| `body-parser`   | Middleware untuk express, digunakan untuk parsing request body, seperti parsing JSON dan url-encoded |
| `cloudinary`   | Mengintegrasikan penggunaan layanan cloudinary |
| `dotenv`   | Memuat environment variable dari file `.env` |
| `ejs`   | Templating engine yang digunakan untuk menghasilkan HTML dengan JavaScript di sisi server |
| `express`   | Framework web minimalis Node.js untuk membuat aplikasi web dan API |
| `jsonwebtoken`   | Membuat dan memverifikasi JSON Web Token (JWT)  |
| `mongoose`   | ODM (Object Data Modeling) untuk MongoDB dan Node.js, menyediakan skema dan validasi data |
| `multer`   | Middleware untuk menangani multipart/form-data, digunakan untuk mengunggah file di Express |
| `nodemailer`   | Mengirim email dari node.js |
| `tsconfig-paths`   | Plugin untuk ts-node dan webpack yang memungkinkan penggunaan path mapping di tsconfig.json. |
| `ts-node-dev`   | Pengembangan dan restart server otomatis untuk aplikasi TypeScript (mirip nodemon pada JavaScript) |
| `typescript`   | Superset JavaScript yang menambahkan tipe statis opsional, menyediakan alat yang lebih baik untuk pengembangan skala besar |
| `yup`   | Melakukan validasi skema objek JavaScript dan TypeScript |

#### Library `@types`
Library yang berperan sebagai konvensi penamaan untuk mendukung definisi tipe TypeScript pada library JavaScript.
| Library   | Deskripsi             |
| ---      | ---                   |
| `@types/body-parser`   | Definisi tipe untuk library yang didukung |
| `@types/dotenv`   | |
| `@types/ejs`   | |
| `@types/express`   | |
| `@types/jsonwebtoken`   | |
| `@types/multer`   | |
| `@types/node`   | |
| `@types/nodemailer`   | |
| `@types/yup`   | |

### API Endpoints

#### Authentication

| Method   | Endpoints             | Deskripsi                              |
| ---      | ---                   | ---                                 |
| `POST`   | `/api/auth/register`  | Register user baru                  |
| `POST`   | `/api/auth/login`     | Login user                          |
| `GET`    | `/api/auth/me`        | Mendapatkan user profile            |
| `PUT`    | `/api/auth/profile`   | Edit user profile                   |

#### Categories

| Method   | Endpoints             | Deskripsi                              |
| ---      | ---                   | ---                                 |
| `GET`    | `/api/categories`     | Mendapatkan semua categories        |
| `GET`    | `/api/categories/:id` | Mendapatkan category berdasarkan id |
| `POST`   | `/api/categories`     | Menambahkan category baru           |
| `PUT`    | `/api/categories/:id` | Edit category berdasarkan id        |
| `DELETE` | `/api/categories/:id` | Hapus category berdasarkan id       |

#### Products

| Method   | Endpoints             | Deskripsi                              |
| ---      | ---                   | ---                                 |
| `GET`    | `/api/products`       | Mendapatkan semua products          |
| `GET`    | `/api/products/:id`   | Mendapatkan product berdasarkan id  |
| `POST`   | `/api/products`       | Menambahkan product baru            |
| `PUT`    | `/api/products/:id`   | Edit product berdasarkan id         |
| `DELETE` | `/api/products/:id`   | Hapus product berdasarkan id        |

#### Orders

| Method   | Endpoints             | Deskripsi                              |
| ---      | ---                   | ---                                 |
| `GET`    | `/api/orders`         | Mendapatkan semua orders            |
| `GET`    | `/api/orders/:id`     | Mendapatkan order berdasarkan id    |
| `POST`   | `/api/orders`         | Menambahkan order baru              |
| `PUT`    | `/api/orders/:id`     | Edit order berdasarkan id           |
| `DELETE` | `/api/orders/:id`     | Hapus order berdasarkan id          |

#### Upload File

| Method   | Endpoints             | Deskripsi                              |
| ---      | ---                   | ---                                 |
| `POST`   | `/api/upload`         | Upload single file                  |
| `POST`   | `/api/uploads`        | Upload multiple file                |

### Middleware
| Middleware   | Method             | Endpoint                              | Deskripsi |
| ---      | ---                   | ---                                 | --- |
| `authMiddleware`   | `GET`         | `/api/auth/me`                  | Untuk melakukan autentikasi user berdasarkan token JWT yang diberikan pada request header pada endpoint yang ditentukan untuk dapat mengakses fitur lainnya yang memerlukan autentikasi user
|    | `PUT`         | `/api/auth/profile`                  | 
|    | `GET`         | `/api/orders`                  |
|    | `GET`         | `/api/orders/:id`                  |
|    | `POST`         | `/api/orders`                  |
|    | `PUT`         | `/api/orders/:id`                  |
|    | `DELETE`         | `/api/orders/:id`                  |
| `aclMiddleware(["<role1>", "<role2>", ... <role-n>])`   | `GET`         | `/api/auth/me`                  | Untuk melakukan otorisasi pengguna berdasarkan peran (role) yang dimiliki, sehingga pengguna dapat mengakses endpoint atau melakukan tindakan tertentu yang memerlukan peran tersebut
| `uploadMiddleware.single`   | `POST`         | `/api/upload`                  | Untuk mengunggah 1 file
| `uploadMiddleware.multiple`   | `POST`         | `/api/uploads`                  | Untuk mengunggah lebih 1 file

## Contoh Format Request dan Response

### Request Header
* Key   : Authorization
* Value : Bearer `<JWT Token>`

### Request Body & Response (POST Method)

### POST auth/register

Contoh: http://example.gov/api/auth/register

Request body :

    {
        "email": "samueldjodi@email.com",
        "fullName": "Samuel Djodi",
        "password": "12341234",
        "username": "samueldjodi",
        "roles": ["admin", "user"]
    }

Response body :

    {
        "message": "User registered successfully",
        "data": {
            "fullName": "Samuel Djodi",
            "username": "samueldjodi",
            "email": "samueldjodi@email.com",
            "roles": [
                "admin",
                "user"
            ],
            "profilePicture": "default.jpg",
            "_id": "66871bc6914900e905ad0376",
            "createdAt": "2024-07-04T22:01:42.223Z",
            "updatedAt": "2024-07-04T22:01:42.223Z",
            "__v": 0
        }
    }

### POST auth/login

Contoh: http://example.gov/api/auth/login

Request body :

    {
        "email": "samueldjodi@email.com",
        "password": "12341234"
    }

Response body :

    {
        "message": "User logged in successfully",
        "data": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY2ODcxYmM2OTE0OTAwZTkwNWFkMDM3NiIsInJvbGVzIjpbImFkbWluIiwidXNlciJdLCJpYXQiOjE3MjAxMzA1OTYsImV4cCI6MTcyMDE1MjE5Nn0.wVdAzCK9F5SjtOyhaOy7IRgp88iYAxeD3OLGchRWoAc"
    }

### POST /upload & POST /uploads

Contoh: http://example.gov/api/upload atau http://example.gov/api/uploads

Request body (multipart/form-data) :
- Key   : file (/upload) atau files (/uploads)
- Value : `Input Gambar Anda`

Response body :

    {
        "message": "File uploaded",
        "data": {
            "asset_id": "82e813e81975c96e4010e9e917704452",
            "public_id": "ivj5yzmibqfoogtkl43p",
            "version": 1720139820,
            "version_id": "4654deaeae581dbe9d583e2a04d484r3",
            "signature": "b59916a6e38dfc7f8f6d2b2a0b5a97bcf3e8524p",
            "width": 1509,
            "height": 795,
            "format": "png",
            "resource_type": "image",
            "created_at": "2024-07-04T21:59:10Z",
            "tags": [],
            "bytes": 55738,
            "type": "upload",
            "etag": "cf0f014ef04a19f95bf56169fa5743va",
            "placeholder": false,
            "url": "http://res.cloudinary.com/ameidornf/image/upload/1720139820/ivj5yzmibqfoogtkl43p.png",
            "secure_url": "https://res.cloudinary.com/ameidornf/image/upload/1720139820/ivj5yzmibqfoogtkl43p.png",
            "asset_folder": "",
            "display_name": "ivj5yzmibqfoogtkl43p",
            "api_key": "048480340843934"
        }
    }

### POST /categories

Contoh: http://example.gov/api/categories

Request body :

  {
  "name": "electronic"
  }

Response body :

    {
        "message": "Success create category",
        "data": {
            "name": "kitchenware",
            "products": [],
            "_id": "6687188d914900e905ad0364",
            "createdAt": "2024-07-04T21:47:57.460Z",
            "updatedAt": "2024-07-04T21:47:57.460Z",
            "__v": 0
        }
    }

### POST /products

Contoh: http://example.gov/api/products

Request body :

    {
        "name": "Nipis Madu",
        "description": "Minuman soda yang menyegarkan",
        "images": ["gambar1.png", "gambar2.png"],
        "price": 5000,
        "quantity": 20,
        "category": "{{categories_id}}"
    }

Response body :

    {
        "message": "Success create product",
        "data": {
            "name": "Nipis Madu",
            "description": "Minuman soda yang menyegarkan",
            "images": [
                "gambar1.png",
                "gambar2.png"
            ],
            "price": 5000,
            "quantity": 20,
            "category": "6676eb1cf3af1ba4b11a6e24",
            "_id": "668719cc914900e905ad0373",
            "createdAt": "2024-07-04T21:53:16.749Z",
            "updatedAt": "2024-07-04T21:53:16.749Z",
            "slug": "nipis-madu",
            "__v": 0
        }
    }

### POST /orders

Contoh: http://example.gov/api/orders

Request Header
* Key   : Authorization
* Value : Bearer `<JWT Token>`

Request body :

    {
        "orderItems": [
            {
              "productId": "6676eabaf3af1ba4b11a6e12", 
              "quantity": 3
            },
            {
              "productId": "6676e98ef3af1ba4b11a6e04",
              "quantity": 2
            }
        ]
    }

Response body :

    {
        "message": "Success create order",
        "data": [
            {
                "grandTotal": 19000000,
                "orderItems": [
                    {
                        "name": "Laptop",
                        "productId": "6676eb4cf3af1ba4b11a6e2a",
                        "price": 5000000,
                        "quantity": 3,
                        "_id": "6686f942f7d6cd82312606f9"
                    },
                    {
                        "name": "Smartphone",
                        "productId": "6676eb66f3af1ba4b11a6e2f",
                        "price": 2000000,
                        "quantity": 2,
                        "_id": "6686f942f7d6cd82312606fa"
                    }
                ],
                "createdBy": "6686f4e771b17d12f8d2215b",
                "status": "pending",
                "_id": "6686f942f7d6cd82312606f8",
                "createdAt": "2024-07-04T19:34:26.363Z",
                "updatedAt": "2024-07-04T19:34:26.363Z",
                "__v": 0
            }
        ]
    }

Invoice 
![Invoice Image](https://res.cloudinary.com/dkyazovdn/image/upload/v1720130350/ivj5yzmibqfoogtkl20n.png)