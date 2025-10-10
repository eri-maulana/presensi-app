# Acceptance Criteria (singkat)

## Presensi (MVP)
- Mahasiswa dapat memilih mata kuliah dari jadwal hari ini.
- Mahasiswa diminta izin GPS; jika diizinkan koordinat tampil.
- Sistem menghitung jarak; jika <= radius kampus tombol kamera aktif.
- Mahasiswa mengambil foto; foto dikirim ke endpoint /api/presensi.
- Server menyimpan record + foto, mengembalikan JSON sukses.

## Dosen - Verifikasi
- Dosen dapat melihat daftar presensi real-time (polling).
- Dosen dapat mengubah status presensi (pending → valid/rejected).
