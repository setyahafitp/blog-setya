---
title: "Dark Web Secara Teknis: Arsitektur, Enkripsi, dan Mekanisme Onion Routing"
date: 2026-02-26T22:30:00+07:00
draft: false
summary: "Catatan teknis saya tentang bagaimana Dark Web bekerja di level jaringan: onion routing, hidden services, enkripsi berlapis, dan arsitektur desentralisasinya."
tags: ["Network Security", "Dark Web", "Tor", "Encryption", "Cybersecurity"]
---

Saat orang mendengar istilah “Dark Web”, yang terbayang biasanya adalah pasar ilegal dan aktivitas kriminal.  
Namun secara teknis, Dark Web bukanlah entitas mistis. Ia adalah implementasi arsitektur jaringan berbasis anonimitas.

Di jurnal ini, saya membedahnya secara teknis.

---

## 1. Definisi Teknis

Dark Web adalah bagian dari internet yang:

- Tidak terindeks search engine tradisional
- Menggunakan jaringan overlay anonim
- Mengakses layanan dengan domain khusus (.onion)

Jaringan paling terkenal adalah **:contentReference[oaicite:0]{index=0}**.

Browser yang digunakan: **:contentReference[oaicite:1]{index=1}**

---

## 2. Arsitektur Tor: Onion Routing

Konsep inti Tor adalah Onion Routing.

Bagaimana cara kerjanya?

Misalkan user ingin mengakses server .onion.

### Step 1 — Circuit Creation
Client Tor membangun jalur acak melalui 3 node:
- Entry Node (Guard)
- Relay Node
- Exit Node (untuk akses internet biasa)

Untuk hidden service (.onion), tidak ada exit node publik.

### Step 2 — Layered Encryption
Data dienkripsi berlapis seperti bawang:

Encrypt 1 → untuk Exit Node  
Encrypt 2 → untuk Relay Node  
Encrypt 3 → untuk Entry Node  

Setiap node hanya mengetahui:
- Dari mana paket datang
- Ke mana harus diteruskan

Node tidak pernah tahu:
- Siapa pengirim asli
- Tujuan akhir sebenarnya

Inilah prinsip anonimitas terdistribusi.

---

## 3. Hidden Service (.onion) Secara Teknis

Website .onion tidak memiliki IP publik.

Sebagai gantinya:

1. Server membuat pasangan public/private key.
2. Public key di-hash menjadi alamat .onion.
3. Server mendaftarkan dirinya ke Tor directory nodes.
4. Client membangun rendezvous circuit.
5. Client dan server bertemu di middle relay tanpa mengetahui IP satu sama lain.

Artinya:
- Server tidak tahu IP client
- Client tidak tahu IP server

Ini adalah mutual anonymity.

---

## 4. Kenapa Sulit Dilacak?

Karena:

- Tidak ada DNS tradisional
- Tidak ada IP publik langsung
- Routing terenkripsi end-to-end
- Jalur selalu berubah (circuit rotation)

Selain itu, Tor bersifat volunteer-based network.

Semakin banyak node, semakin kompleks pelacakan.

---

## 5. Realitas Keamanan

Anonimitas ≠ Kebal.

Beberapa kelemahan:
- Traffic correlation attack
- Malicious exit node
- Browser fingerprinting
- Human error (leak metadata)

Marketplace seperti **:contentReference[oaicite:2]{index=2}** pernah ditutup bukan karena Tor rusak, tetapi karena kesalahan operasional dan investigasi forensik digital.

Artinya:
Keamanan sistem sering runtuh karena manusia, bukan algoritma.

---

## 6. Dark Web vs Deep Web (Teknis)

Deep Web:
- Database privat
- Panel admin
- Tidak terindeks
- Masih pakai HTTP biasa

Dark Web:
- Overlay network
- Enkripsi berlapis
- Domain kriptografis
- Hidden service architecture

---

## 7. Refleksi Teknis

Dark Web bukanlah “internet jahat”.

Ia adalah eksperimen jaringan anonim berskala global.

Masalahnya bukan pada onion routing.
Masalahnya pada bagaimana manusia menggunakannya.

Sebagai developer, memahami ini penting bukan untuk eksplorasi ilegal — tetapi untuk:

- Memahami ancaman distribusi data breach
- Mengerti konsep anonymization network
- Mengembangkan sistem yang lebih aman

Karena keamanan bukan hanya soal backend.
Ia soal memahami ekosistem jaringan secara utuh.