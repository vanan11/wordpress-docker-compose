# WordPress Docker Compose

## Deskripsi Project

Project ini bertujuan untuk menjalankan WordPress menggunakan Docker Compose dengan konsep multi-container.
Dalam project ini digunakan 3 service utama yaitu WordPress sebagai aplikasi web, MySQL sebagai database, dan Redis sebagai object cache untuk meningkatkan performa website.

Melalui project ini mahasiswa dapat memahami cara kerja container orchestration, docker networking, penggunaan volume untuk persistence data, serta konfigurasi environment pada aplikasi berbasis container.

---

## Arsitektur Service

Project ini terdiri dari:

* **WordPress**
  Berfungsi sebagai CMS yang dapat diakses melalui browser pada port 8000.

* **MySQL**
  Digunakan sebagai database untuk menyimpan data user, post, page, dan konfigurasi WordPress.

* **Redis**
  Digunakan sebagai cache memory agar proses loading website menjadi lebih cepat.

---

## Cara Menjalankan Project

1. Masuk ke folder project
2. Jalankan perintah berikut:

docker compose up -d

3. Setelah container berjalan, buka browser dan akses:

http://localhost:8000

4. Lakukan instalasi WordPress melalui halaman web installer.

---

## Persistence Data

Pada project ini digunakan Docker Volume untuk memastikan data tidak hilang ketika container dihentikan atau dijalankan kembali.

Volume digunakan pada:

* Folder WordPress
* Folder database MySQL

Hal ini penting karena tanpa volume, data akan terhapus setiap container dihapus.

---

## Docker Networking

Semua container berada dalam satu network yang sama sehingga dapat saling berkomunikasi menggunakan nama service.

WordPress dapat terhubung ke database dengan hostname **mysql** dan ke cache dengan hostname **redis**.

---

## Redis Object Cache

Plugin Redis Object Cache diaktifkan pada WordPress untuk meningkatkan performa.

Dengan adanya Redis, query database yang sering digunakan akan disimpan di memory sehingga website dapat diakses lebih cepat.

Konfigurasi yang ditambahkan pada file `wp-config.php`:

define('WP_REDIS_HOST', 'redis');
define('WP_REDIS_PORT', 6379);
define('WP_CACHE', true);

---

## Screenshot Instalasi WordPress

![Install](screenshots/install.png)

## Screenshot Dashboard WordPress

![Dashboard](screenshots/dashboard.png)

## Screenshot Tampilan Post WordPress

![Post](screenshots/post.png)

## Screenshot Docker Container Running

![Docker](screenshots/docker-ps.png)

## Screenshot Redis Object Cache Connected

![Redis](screenshots/redis.png)

---

## Pengujian

Beberapa pengujian yang dilakukan:

* WordPress berhasil diakses melalui browser
* Post dapat dibuat dan tersimpan di database
* Data tetap ada setelah container di-restart
* Redis berhasil terkoneksi dan cache aktif

---

## Jawaban Pertanyaan

**Kenapa perlu volume untuk MySQL?**
Volume diperlukan agar data database tetap tersimpan walaupun container dihentikan atau dihapus.

**Apa fungsi depends_on?**
depends_on digunakan untuk memastikan container database dan redis berjalan terlebih dahulu sebelum WordPress dijalankan.

**Bagaimana cara WordPress container connect ke MySQL?**
WordPress terhubung ke MySQL melalui hostname service docker yaitu **mysql** yang dikonfigurasi pada environment variable `WORDPRESS_DB_HOST`.

**Apa keuntungan pakai Redis untuk WordPress?**
Redis berfungsi sebagai cache memory sehingga dapat mempercepat loading website, mengurangi beban query database, dan meningkatkan performa aplikasi.

---

## Author

Nama: GEDE PRADISTYA EVAN ARYAPUTRA
NIM: A11.2023.14886
Kelas: 4618
Mata Kuliah: Pemrograman Sisi Server
