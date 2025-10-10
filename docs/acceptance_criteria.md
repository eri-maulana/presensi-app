# Acceptance Criteria (Kriteria Penerimaan)

## 1. Login / Autentikasi
- Pengguna dapat login menggunakan email + password.
- Role yang benar diarahkan ke dashboard sesuai: mahasiswa, dosen, admin.
- Validasi form wajib (tidak boleh kosong).

## 2. Presensi Mahasiswa
- Mahasiswa membuka halaman presensi hari ini.
- Sistem meminta izin GPS, lalu menampilkan koordinat & jarak ke titik kampus.
- Tombol “Ambil Selfie” aktif hanya jika berada di dalam radius ≤ 100 m.
- Setelah foto diambil, data (foto + koordinat + waktu) dikirim ke server.
- Data tersimpan dan status awal = `pending`.

## 3. Dosen – Verifikasi Presensi
- Dosen melihat daftar presensi berdasarkan jadwal kuliah yang diampu.
- Dosen dapat menyetujui atau menolak presensi.
- Riwayat verifikasi tersimpan (oleh siapa dan kapan).

## 4. Admin
- Admin dapat mengelola data master (mahasiswa, dosen, jadwal, mata kuliah).
- Admin dapat mengekspor laporan kehadiran per mata kuliah.

## 5. Umum / Teknis
- Semua endpoint API memiliki validasi token (JWT).
- Respons API dikembalikan dalam format JSON standar.
