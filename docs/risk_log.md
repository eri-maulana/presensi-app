# Risk Log

| Risiko | Dampak | Kemungkinan | Mitigasi |
|--------|---------|--------------|-----------|
| GPS tidak akurat | Presensi ditolak meski di kampus | Sedang | Gunakan toleransi radius ±30 m |
| Foto gagal upload | Data presensi tidak tersimpan | Rendah | Implement retry upload |
| Spoofing foto | Presensi palsu | Sedang | Verifikasi wajah (opsional fase lanjut) |
| Privasi data | Pelanggaran data foto | Rendah | Enkripsi dan akses berbatas |
| Gangguan jaringan | Presensi gagal real-time | Sedang | Simpan offline → sinkronisasi otomatis |
