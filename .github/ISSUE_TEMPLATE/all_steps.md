# Step 1 - Setup Repositori & Manajemen Proyek
Setup struktur repo, branch, label, dan project board.

# Step 2 - Inisialisasi Laravel & Konfigurasi Dasar
Install Laravel, konfigurasi .env, setup database & auth scaffolding.

# Step 3 - Desain Database & ERD Final
Buat migration sesuai ERD (users, mahasiswa, dosen, mata_kuliah, jadwal, presensi, lokasi).

# Step 4 - Seeder & Factory Data Awal
Buat data dummy untuk mahasiswa, dosen, mata kuliah, dan jadwal.

# Step 5 - Setup Autentikasi Multi-Role
Gunakan Laravel Breeze / Fortify, konfigurasi guard untuk mahasiswa, dosen, dan admin.

# Step 6 - Dashboard Role-Based
Buat tampilan dashboard berbeda per role (mahasiswa, dosen, admin).

# Step 7 - Modul Manajemen Data Mahasiswa
CRUD data mahasiswa.

# Step 8 - Modul Manajemen Data Dosen
CRUD data dosen.

# Step 9 - Modul Manajemen Mata Kuliah & Jadwal
CRUD mata kuliah & jadwal perkuliahan.

# Step 10 - Modul Manajemen Lokasi Kampus & Radius
CRUD lokasi kampus, gunakan Google Maps API atau Leaflet.js.

# Step 11 - Integrasi GPS & Geolocation API
Validasi lokasi user terhadap radius kampus.

# Step 12 - Modul Kamera Selfie
Gunakan getUserMedia() & simpan foto ke storage.

# Step 13 - Validasi Foto & Lokasi
Pastikan presensi hanya bisa dilakukan jika posisi & foto valid.

# Step 14 - Simpan Data Presensi
Buat controller dan API endpoint POST /api/presensi.

# Step 15 - Riwayat Presensi Mahasiswa
Tampilkan daftar presensi, lokasi, waktu, dan foto.

# Step 16 - Presensi Pulang
Tambahkan fitur check-out dan waktu selesai perkuliahan.

# Step 17 - Dashboard Dosen
Tampilkan jadwal hari ini dan daftar mahasiswa yang hadir real-time.

# Step 18 - Kontrol Presensi Dosen
Fitur Buka/Tutup Presensi, pantau mahasiswa yang absen.

# Step 19 - Laporan Presensi Dosen
Ekspor data ke PDF/Excel.

# Step 20 - Dashboard Admin
Pantau semua aktivitas presensi real-time.

# Step 21 - Monitoring & Laporan Admin
Filter, cari, dan ekspor laporan kehadiran.

# Step 22 - Backup & Restore Data
Fitur backup otomatis & manual database.

# Step 23 - Pengaturan Sistem
Atur tahun akademik, role user, hak akses, aturan presensi.

# Step 24 - Notifikasi & Alert
Gunakan SweetAlert2 atau Toastify untuk feedback user.

# Step 25 - Middleware & Proteksi Akses
Pastikan role-based access control (RBAC) berjalan.

# Step 26 - Desain UI/UX Responsif
Gunakan Tailwind + Flowbite atau Bootstrap modern.

# Step 27 - Optimasi PWA (Progressive Web App)
Tambahkan service worker, offline cache, dan manifest.json.

# Step 28 - Integrasi Kamera Mobile
Tes di Android/iPhone untuk kompatibilitas.

# Step 29 - Uji Validasi Presensi
Tes GPS dan foto selfie dari berbagai device.

# Step 30 - Audit Log & Riwayat Aktivitas
Catat setiap aksi user di tabel audit.

# Step 31 - Dokumentasi API
Gunakan Laravel Swagger / scribe.

# Step 32 - Testing Otomatis
Buat unit & feature test dasar.

# Step 33 - Deployment ke Hosting
Deploy ke VPS / cPanel / Laravel Forge.

# Step 34 - Setup CI/CD Workflow
Gunakan GitHub Actions untuk otomatisasi testing & deploy.

# Step 35 - Maintenance & Logging
Pantau log, error, dan gunakan Sentry / Laravel Telescope.

# Step 36 - Finalisasi & Presentasi Project
Buat dokumentasi, laporan akhir, dan demo aplikasi.
