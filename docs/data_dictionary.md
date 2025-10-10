# Data Dictionary — Aplikasi Presensi Kampus

> Versi ini disusun agar ukuran kolom realistis (tidak berlebihan / tidak kekecilan),
> serta memberikan rekomendasi index, constraint, dan opsi normalisasi (kelas/ruangan).

---

## Ringkasan tabel utama
- `users` — akun autentikasi & role (mahasiswa / dosen / admin)
- `mahasiswas` — profil mahasiswa (terhubung ke `users`)
- `dosens` — profil dosen (terhubung ke `users`)
- `mata_kuliahs` — data mata kuliah
- `jadwal_kuliahs` — jadwal per mata kuliah
- `lokasi_kampus` — pusat lokasi kampus & radius geofence
- `presensis` — catatan presensi (foto + GPS + status)
- opsional: `kelas`, `ruangan` — lookup tabel bila nilai terbatas

---

## TABEL: `users`
Deskripsi: akun login seluruh pengguna (role-based).

| Kolom | Tipe (MySQL) | Panjang / Detail | Atribut / Constraint |
|---|---:|---|---|
| id | BIGINT UNSIGNED | AI, PK |  |
| name | VARCHAR | 100 | NOT NULL |
| email | VARCHAR | 150 | NOT NULL, UNIQUE |
| password | VARCHAR | 255 | NOT NULL (hash bcrypt/argon2) |
| role | ENUM | ('mahasiswa','dosen','admin') | DEFAULT 'mahasiswa' |
| remember_token | VARCHAR | 100 | nullable |
| created_at / updated_at | TIMESTAMP | | timestamps |

**Indexes & catatan**
- index unik pada `email`.
- `password` pakai 255 untuk keamanan (cukup untuk bcrypt/argon2).

---

## TABEL: `mahasiswas`
Deskripsi: profil data mahasiswa, terpisah dari `users` untuk menyimpan atribut akademik.

| Kolom | Tipe | Panjang / Detail | Atribut / Constraint |
|---|---:|---|---|
| id | BIGINT UNSIGNED | AI, PK |  |
| user_id | BIGINT UNSIGNED | FK → users.id | ON DELETE CASCADE, NOT NULL |
| nim | VARCHAR | 20 | NOT NULL, UNIQUE |
| kelas_id | INT UNSIGNED | FK → kelas.id (opsional) | nullable OR gunakan `kelas` VARCHAR(10) |
| foto_profile | VARCHAR | 255 | nullable (path) |
| created_at / updated_at | TIMESTAMP | | timestamps |

**Indexes & catatan**
- UNIQUE index pada `nim`.
- Jika jumlah `kelas` terbatas (5–10), gunakan tabel lookup `kelas` dan simpan `kelas_id`. Lebih baik untuk konsistensi.

---

## TABEL: `dosens`
Deskripsi: profil dosen pengampu.

| Kolom | Tipe | Panjang / Detail | Atribut / Constraint |
|---|---:|---|---|
| id | BIGINT UNSIGNED | AI, PK |  |
| user_id | BIGINT UNSIGNED | FK → users.id | ON DELETE CASCADE, NOT NULL |
| nidn | VARCHAR | 20 | NOT NULL, UNIQUE |
| foto_profile | VARCHAR | 255 | nullable |
| created_at / updated_at | TIMESTAMP | | timestamps |

**Indexes & catatan**
- UNIQUE index pada `nidn`.

---

## TABEL: `mata_kuliahs`
Deskripsi: master mata kuliah.

| Kolom | Tipe | Panjang / Detail | Atribut / Constraint |
|---|---:|---|---|
| id | BIGINT UNSIGNED | AI, PK |  |
| kode_mk | VARCHAR | 20 | NOT NULL, UNIQUE |
| nama_mk | VARCHAR | 150 | NOT NULL |
| dosen_id | BIGINT UNSIGNED | FK → dosens.id | nullable (bisa belum diassign) |
| sks | TINYINT UNSIGNED | | nullable |
| created_at / updated_at | TIMESTAMP | | timestamps |

**Indexes & catatan**
- UNIQUE index pada `kode_mk`.
- `nama_mk` 150 cukup untuk nama panjang + subjudul.

---

## TABEL: `jadwal_kuliahs`
Deskripsi: jadwal per mata kuliah (hari, jam, kelas/ruangan).

| Kolom | Tipe | Panjang / Detail | Atribut / Constraint |
|---|---:|---|---|
| id | BIGINT UNSIGNED | AI, PK |  |
| mk_id | BIGINT UNSIGNED | FK → mata_kuliahs.id | ON DELETE CASCADE |
| hari | ENUM | ('Senin','Selasa','Rabu','Kamis','Jumat','Sabtu','Minggu') | NOT NULL |
| jam_mulai | TIME | | NOT NULL |
| jam_selesai | TIME | | NOT NULL |
| kelas_id | INT UNSIGNED | FK → kelas.id (opsional) | nullable OR `VARCHAR(10)` |
| ruangan_id | INT UNSIGNED | FK → ruangan.id (opsional) | nullable OR `VARCHAR(20)` |
| created_at / updated_at | TIMESTAMP | | timestamps |

**Indexes & catatan**
- Index pada `(mk_id, hari, jam_mulai)` berguna untuk query jadwal hari ini.
- Jika `kelas`/`ruangan` sedikit, buat tabel lookup untuk integritas.

---

## TABEL: `lokasi_kampus`
Deskripsi: titik pusat kampus & radius geofencing (m).

| Kolom | Tipe | Panjang / Detail | Atribut / Constraint |
|---|---:|---|---|
| id | BIGINT UNSIGNED | AI, PK |  |
| nama | VARCHAR | 80 | nullable |
| latitude | DECIMAL | (10,7) | NOT NULL |
| longitude | DECIMAL | (10,7) | NOT NULL |
| radius_m | INT UNSIGNED | | DEFAULT 300 |
| created_at / updated_at | TIMESTAMP | | timestamps |

**Indexes & catatan**
- Hanya diperlukan satu record default untuk single-campus. Untuk multi-campus, tambahkan `campus_id` di jadwal/presensi.

---

## TABEL: `presensis`
Deskripsi: setiap baris merepresentasikan satu aksi presensi (masuk / pulang).

| Kolom | Tipe | Panjang / Detail | Atribut / Constraint |
|---|---:|---|---|
| id | BIGINT UNSIGNED | AI, PK |  |
| user_id | BIGINT UNSIGNED | FK → users.id | ON DELETE CASCADE, NOT NULL |
| jadwal_kuliah_id | BIGINT UNSIGNED | FK → jadwal_kuliahs.id | nullable |
| mk_id | BIGINT UNSIGNED | FK → mata_kuliahs.id | nullable |
| type | ENUM | ('masuk','pulang') | DEFAULT 'masuk' |
| latitude | DECIMAL | (10,7) | nullable |
| longitude | DECIMAL | (10,7) | nullable |
| distance_m | INT UNSIGNED | | nullable |
| foto_selfie | VARCHAR | 255 | nullable (path) |
| foto_hash | VARCHAR | 64 | nullable (sha256) untuk deteksi replay) |
| status | ENUM | ('pending','valid','rejected') | DEFAULT 'pending' |
| keterangan | TEXT | | nullable |
| created_at / updated_at | TIMESTAMP | | timestamps |

**Indexes & catatan**
- Index pada `user_id`, `jadwal_kuliah_id`, `status`, dan composite `(jadwal_kuliah_id, created_at)` untuk rekap per sesi.
- Simpan `foto_hash` (sha256) untuk mendeteksi upload foto identik berulang (replay).

---

## OPSIONAL: Lookup tables (direkomendasikan jika nilai terbatas)

### TABEL: `kelas`
| Kolom | Tipe |
|---|---:|
| id | INT UNSIGNED AI |
| kode | VARCHAR(10) | ex: "A", "TI-2" |
| nama | VARCHAR(50) |
| created_at / updated_at | TIMESTAMP |

### TABEL: `ruangan`
| Kolom | Tipe |
|---|---:|
| id | INT UNSIGNED AI |
| kode | VARCHAR(20) | ex: "A101" |
| lantai | VARCHAR(10) | nullable |
| kapasitas | SMALLINT UNSIGNED | nullable |

**Keuntungan lookup**
- Konsistensi data (tidak ada variasi penulisan).
- Mudah menambahkan metadata (kapasitas, lantai).
- Mudah diubah tanpa migration dibandingkan ENUM.

---

## Rekomendasi Index & Performance
- `users.email` → UNIQUE
- `mahasiswas.nim` → UNIQUE + INDEX
- `mata_kuliahs.kode_mk` → UNIQUE
- `presensis.user_id`, `presensis.jadwal_kuliah_id`, `presensis.status` → INDEX
- Composite index: `(jadwal_kuliah_id, created_at)` untuk query rekap per sesi
- Pertimbangkan indexing `created_at` untuk tabel besar (archive/purge policy)

---

## Kolom panjang yang disarankan (ringkasan)
- Nama lengkap: `VARCHAR(100)`
- Email: `VARCHAR(150)`
- Password (hash): `VARCHAR(255)`
- NIM / NIDN: `VARCHAR(20)`
- Kode MK: `VARCHAR(20)`
- Nama MK: `VARCHAR(150)`
- Kelas: `VARCHAR(10)` (jika tidak normalisasi)
- Ruangan: `VARCHAR(20)` (jika tidak normalisasi)
- Foto path: `VARCHAR(255)`
- Foto hash: `VARCHAR(64)`

---

## Contoh potongan migration (Laravel) — sebagai referensi cepat

**create_presensis_table.php (potongan)**

```php
Schema::create('presensis', function (Blueprint $table) {
    $table->id();
    $table->foreignId('user_id')->constrained('users')->onDelete('cascade');
    $table->foreignId('jadwal_kuliah_id')->nullable()->constrained('jadwal_kuliahs')->onDelete('set null');
    $table->foreignId('mk_id')->nullable()->constrained('mata_kuliahs')->onDelete('set null');
    $table->enum('type', ['masuk', 'pulang'])->default('masuk');
    $table->decimal('latitude', 10, 7)->nullable();
    $table->decimal('longitude', 10, 7)->nullable();
    $table->unsignedInteger('distance_m')->nullable();
    $table->string('foto_selfie', 255)->nullable();
    $table->string('foto_hash', 64)->nullable();
    $table->enum('status', ['pending','valid','rejected'])->default('pending');
    $table->text('keterangan')->nullable();
    $table->timestamps();

    $table->index(['user_id']);
    $table->index(['jadwal_kuliah_id']);
    $table->index(['status']);
    $table->index(['jadwal_kuliah_id','created_at']);
});
