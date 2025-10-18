# Requirements - Aplikasi Presensi Kampus

## Tujuan
Membangun sistem presensi berbasis web progresif (PWA) untuk mahasiswa, dosen, dan admin dengan fitur selfie dan validasi lokasi (GPS). Aplikasi ini mempermudah proses presensi harian, mengurangi kecurangan, dan menyediakan laporan kehadiran yang akurat dan real-time.

## Fitur Utama
1. **Autentikasi & Role**
   - Login untuk mahasiswa, dosen, dan admin.
   - Manajemen akun pengguna (CRUD oleh admin).

2. **Presensi Mahasiswa**
   - Presensi masuk & pulang dengan foto selfie dan GPS.
   - Validasi lokasi berdasarkan radius kampus.
   - Deteksi presensi ganda atau di luar area.

3. **Verifikasi Dosen**
   - Melihat daftar mahasiswa yang sudah presensi.
   - Menyetujui atau menolak presensi (pending → valid/invalid).

4. **Manajemen Data**
   - CRUD data mahasiswa, dosen, mata kuliah, dan jadwal kuliah.
   - Penjadwalan otomatis berdasarkan semester aktif.

5. **Laporan & Statistik**
   - Rekap kehadiran per mata kuliah.
   - Ekspor ke PDF/XLSX.
   - Dashboard statistik kehadiran.

6. **Keamanan & Privasi**
   - Data foto disimpan dengan izin pengguna.
   - Sistem mengenkripsi password & melindungi data lokasi.

## Batasan & Asumsi
- Pengguna wajib mengizinkan kamera dan GPS agar presensi dapat dilakukan.
- Foto selfie hanya digunakan untuk verifikasi kehadiran.
- Aplikasi berjalan optimal di browser modern & mobile (Android/iOS).

## Acceptance Criteria
Lihat: [docs/acceptance_criteria.md](./acceptance_criteria.md)
