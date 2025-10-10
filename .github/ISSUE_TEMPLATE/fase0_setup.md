name: "Fase 0 — Setup & Environment Preparation"
description: "Checklist persiapan awal sebelum pengembangan aplikasi presensi Laravel dimulai"
title: "[Fase 0] Setup & Environment Preparation"
labels: ["fase-0", "setup", "planning"]
assignees: []

body:
  - type: markdown
    attributes:
      value: |
        ## 🎯 Tujuan
        Fase ini bertujuan menyiapkan seluruh fondasi proyek sebelum pengembangan dimulai.  
        Pastikan semua checklist telah selesai ✅ sebelum lanjut ke Fase 1 (Perancangan Database & Struktur Kode).

  - type: checkboxes
    id: tools
    attributes:
      label: "🧰 Persiapan Tools & Software"
      options:
        - label: "Install PHP (versi 8.2 atau lebih baru)"
        - label: "Install Composer"
        - label: "Install Node.js & NPM"
        - label: "Install Git & membuat akun GitHub"
        - label: "Install Laravel CLI (`composer global require laravel/installer`)"
        - label: "Install VSCode atau editor pilihan"
        - label: "Install XAMPP / Laragon / Valet (untuk server lokal)"

  - type: checkboxes
    id: project_setup
    attributes:
      label: "🚀 Persiapan Proyek Laravel"
      options:
        - label: "Membuat proyek baru: `laravel new presensi-web`"
        - label: "Menjalankan `php artisan serve` untuk memastikan project berjalan"
        - label: "Membuat `.env` dan menyesuaikan konfigurasi database"
        - label: "Menjalankan `php artisan key:generate`"
        - label: "Membuat struktur folder dasar (Models, Controllers, Views, Routes, dll)"
        - label: "Menambahkan TailwindCSS dan Vite untuk frontend"
        - label: "Menambahkan autentikasi dasar menggunakan Laravel Breeze / Fortify"

  - type: checkboxes
    id: repo_setup
    attributes:
      label: "📦 Pengaturan Git & GitHub"
      options:
        - label: "Inisialisasi git (`git init`)"
        - label: "Buat repository baru di GitHub"
        - label: "Hubungkan proyek lokal ke repo GitHub (`git remote add origin ...`)"
        - label: "Push pertama (`git add . && git commit -m 'Initial commit' && git push -u origin main`)"
        - label: "Tambahkan file `.gitignore` sesuai template Laravel"
        - label: "Tambahkan file `README.md` berisi deskripsi singkat proyek"

  - type: checkboxes
    id: docs_setup
    attributes:
      label: "🧾 Dokumentasi Awal"
      options:
        - label: "Buat folder `docs/` untuk menyimpan dokumen (ERD, Mockup, Data Dictionary)"
        - label: "Upload ERD terbaru"
        - label: "Upload file Mockup aplikasi"
        - label: "Tambahkan file `docs/data_dictionary.md` (sudah dibuat sebelumnya)"
        - label: "Pastikan seluruh dokumentasi disinkronkan dengan struktur database"

  - type: checkboxes
    id: verification
    attributes:
      label: "✅ Verifikasi Akhir Fase 0"
      options:
        - label: "Proyek Laravel berjalan normal di browser"
        - label: "Koneksi database berhasil (`php artisan migrate:fresh` berjalan tanpa error)"
        - label: "Repository GitHub sinkron dengan folder lokal"
        - label: "Semua dokumen awal (ERD, Mockup, Data Dictionary) sudah tersimpan di folder `docs/`"
        - label: "Sudah siap lanjut ke **Fase 1 — Desain Database & Relasi Model**"

  - type: textarea
    id: notes
    attributes:
      label: "📝 Catatan Tambahan"
      description: "Tuliskan hal yang perlu diperhatikan, kendala, atau catatan selama setup."
      placeholder: "Contoh: Masih perlu setup SSL di XAMPP, atau belum install Node.js"
