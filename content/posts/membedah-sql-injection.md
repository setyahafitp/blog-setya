---
title: "Membedah SQL Injection: Ancaman Klasik yang Masih Mematikan"
date: 2026-01-20T23:15:00+07:00
draft: false
summary: "Catatan mendalam saya tentang SQL Injection (SQLi). Bagaimana sebuah input sederhana bisa memanipulasi database backend, dan kenapa 'Prepared Statements' adalah penyelamat."
tags: ["Web Security", "SQL Injection", "OWASP Top 10", "Hacking", "Defense"]
---

Jujur saja, saat pertama kali mendengar tentang **SQL Injection (SQLi)**, saya pikir ini adalah teknik "kuno" yang mungkin sudah jarang ditemui di web modern. Tapi setelah mendalaminya lebih jauh di materi keamanan aplikasi web, saya sadar betapa salahnya anggapan itu.

SQL Injection ternyata masih menjadi salah satu ancaman paling berbahaya (langganan OWASP Top 10) karena dampaknya yang fatal: dari pencurian data user, *bypass* login, hingga penghapusan seluruh isi database.

Di jurnal ini, saya ingin mendokumentasikan pemahaman teknis saya tentang bagaimana serangan ini bekerja, dan yang terpenting, bagaimana cara mencegahnya dengan benar.

### Apa Itu SQL Injection? (Versi Simpel)

Bayangkan Anda sedang mengisi formulir di sebuah website, misalnya kolom "Username". Normalnya, website mengharapkan Anda memasukkan nama, seperti `setya`.

Website kemudian mengambil nama itu dan menyusunnya menjadi kalimat perintah untuk database (SQL Query), kira-kira bunyinya: *"Hei database, carikan pengguna yang namanya 'setya'"*.

Nah, SQL Injection terjadi ketika penyerang tidak memasukkan nama. Alih-alih nama, mereka memasukkan potongan **perintah SQL tambahan** di kolom tersebut. Jika website tidak memfilter input ini dengan benar, database akan "tertipu" dan menjalankan perintah tambahan tersebut.

Singkatnya: Ini adalah seni "menitipkan" perintah jahat ke dalam input data biasa.

### Bedah Teknis: Bagaimana Serangan Bekerja

Mari kita lihat contoh paling klasik: **Login Bypass**.

Anggaplah ada sebuah website dengan form login (username dan password). Di sisi server (backend), kode programnya (misalnya PHP) mungkin terlihat seperti ini saat memproses login:

```sql
/* PERINGATAN: Ini contoh kode yang RENTAN */
$username = $_POST['user'];
$password = $_POST['pass'];

$sql = "SELECT * FROM users WHERE username = '$username' AND password = '$password'";