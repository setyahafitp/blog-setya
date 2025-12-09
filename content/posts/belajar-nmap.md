---
title: "Belajar Basic Network Scanning dengan Nmap"
date: 2025-12-10
author: "Setya Hafit"
tags: ["Networking", "Kali Linux", "Tutorial"]
draft: false
---

Dalam cybersecurity, tahap pertama yang paling krusial adalah **Reconnaissance** (Pengumpulan Informasi). Tools andalan saya adalah Nmap.

### 1. Scanning Dasar
Untuk melakukan scan cepat ke target, kita bisa gunakan perintah ini di terminal:

```bash
nmap -sC -sV 192.168.1.1