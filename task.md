# ThinkAble — Daftar Tugas & Pelacak Kemajuan (`thinkable.html`)

Acuan: PRD ThinkAble v2.0, `rules.md`, Diagram Mermaid Evaluasi 2-Tahap & Rotasi CT 4-Tahap.
Keluaran utama: Berkas tunggal `thinkable.html`.
Tandai `[x]` bila tugas selesai dan lolos pengujian.

## Keputusan Kunci Terkunci

* [x] **K1**: Splash (`S1`) melakukan transisi otomatis ke Homescreen (`S2_HOME`).
* [x] **K2**: Navigasi utama: Splash → Homescreen → Login → Jenjang → Modul/Pulau → Peta 20 Langkah → Soal.
* [x] **K3**: Rotasi CT 4-tahap berulang setiap 4 langkah (Dekomposisi → Pola → Abstraksi → Algoritma).
* [x] **K4**: Mesin evaluasi 2-tahap tanpa branch "soal serupa". Salah ke-2 langsung menampilkan penjelasan + tombol "Lanjut".
* [x] **K5**: Akses Pengaturan (⚙️) melayang (*overlay*) dari mana saja tanpa mereset jawaban aktif.
* [x] **K6**: Tanpa gembok level, skor, poin, bintang penghargaan, timer, atau warna merah.

## Fase 1 — Fondasi, Stylesheet, Sprite SVG & Core Engine

**Selesai bila:** Kerangka `thinkable.html` siap, seluruh token visual, sprite ikon/maskot, router hash, dan pengelola state `store` berfungsi tanpa hambatan.

* [x] **T1.1** Kerangka Berkas `thinkable.html`: Structure layout (`<style>`, `<svg>` sprites, `#stage`, `<script>`).
* [x] **T1.2** Token CSS (`--ink`, `--bg`, `--surface`, `--pes`, `--ok`, `--almost`, `--line`): Mode Kontras Tinggi, Mode Tenang, Ukuran Teks (A/A+/A++).
* [x] **T1.3** Layout Stage 800×360 px: Skala contain `transform: scale()`, padding 8/48 px, bilah atas 38 px.
* [x] **T1.4** Peringatan Putar Layar (`X1`): Deteksi mode potret dan pengunci orientasi.
* [x] **T1.5** Hash Router (`#S1`, `#S2_HOME`, `#S5_MODUL`, dll.): Pengelola riwayat navigasi, pengangkut fokus keyboard, dan pengungum `aria-live`.
* [x] **T1.6** Objek Teks Terpusat (`STR`): Kamus bahasa Indonesia terstruktur untuk seluruh teks antarmuka.
* [x] **T1.7** Pengelola State & Local Storage (`store`): Skema penyimpanan `userSession`, `settings`, dan `progress` modul.
* [x] **T1.8** SVG Sprite Ikon (`i-*`): Panah, centang, silang, bohlam, info, gear/setting, sound, globe, user, qr, reset, undo, dsb.
* [x] **T1.9** SVG Sprite Maskot & Avatar: Maskot (Lumi, Orin, Kiko, Loreng, Uhu, Semi) dengan 5 ekspresi netral/positif + 8 Avatar Binatang.
* [x] **T1.10** Component Library Dasar: Tombol (`.bt`, `.b2`, `.bd`, `.bx`), Chip (`.ch`), Kartu (`.cd`), Slot Susun (`.dz`), Petak Jalur Grid, Kotak Petunjuk (`.hint`), Kotak Umpan Balik Warm (`.am`), Kotak Benar (`.ok`).
* [x] **T1.11** Layar Galeri Komponen (`#gallery`): Untuk pengujian visual seluruh komponen dan state.

## Fase 2 — Alur Navigasi Utama Aplikasi (`S1` s/d `S6_PETA`)

**Selesai bila:** Seluruh alur navigasi dari Splash Screen hingga Peta 20 Langkah Modul berjalan lancar, termasuk fungsi Login dan Pengaturan.

* [x] **T2.1** `S1` Splash Screen: Animasi penyambut logo ThinkAble & Maskot, auto-advance ke Homescreen dalam 2.5 detik.
* [x] **T2.2** `S2_HOME` Homescreen: Tombol Play besar, Toggle Suara, Toggle Bahasa, Tombol ⚙️ Setting, dan Status Login Akun.
* [x] **T2.3** `S3_LOGIN` Form Login Akun: Input Nama Panggilan / ID Peserta + Simulasi Pindai QR Code (`getUserMedia` / fallback simulasi).
* [x] **T2.4** `S4_JENJANG` Pilih Jenjang: Kartu pilihan Fase A (Kelas 1–2) dan Fase B (Kelas 3–4).
* [x] **T2.5** `S5_MODUL` Beranda Modul Ajar: Pulau tematik (Pertambahan, Pengurangan, Bangun Datar, Pengukuran) tanpa gembok level + Catatan Kemajuan.
* [x] **T2.6** `S6_PETA` Peta Petualangan 20 Langkah: Jalur 20 titik langkah naratif, indikator status titik (terisi/cincin/kosong), tombol kembali (`‹`) dan ⚙️ Setting.
* [x] **T2.7** `S11_SET` Modal Pengaturan Aksesibilitas (Overlay): Dapat dipanggil melayang di atas layar aktif tanpa mengosongkan progres.

## Fase 3 — Mesin Evaluasi Jawaban 2-Tahap & Layar Soal Interaktif

**Selesai bila:** Engine evaluasi 2-tahap berfungsi tepat, 9 template soal interaktif beroperasi halus dengan tombol Cek nonaktif berlabel alasan.

* [x] **T3.1** Core Engine Evaluasi 2-Tahap:
  * Validasi jawaban (pilih tunggal, pilih banyak, susun langkah, grid jalur).
  * Percobaan ke-1 Salah (`A4`/`A5`): Warna hangat `--almost`, petunjuk eksploratif, slot terkosongkan, tanpa kunci jawaban.
  * Percobaan ke-2 Salah (`A6`–`A9`): Kunci jawaban benar + penjelasan visual + tombol **Lanjut** (tanpa percabangan soal serupa).
  * Benar (`A1`/`A2`/`A3`): Apresiasi hangat, penyelesaian langkah.
* [x] **T3.2** Komponen Soal Algoritma:
  * `S6`: Robot Kurir pilih 1 arah (3 opsi).
  * `S6b`: Robot Kurir susun 2–4 langkah (ketuk chip ke slot, chip pengecoh tersedia).
* [x] **T3.3** Komponen Soal Pola:
  * `G1`: Lanjutkan Irama (pilih 1 dari 3).
  * `G2`: Ubin yang Hilang (pilih 1 dari 3, ubin dibedakan bentuk + motif garis).
  * `G7`: Isi 2 Batu Kosong (susun 2 chip).
* [x] **T3.4** Komponen Soal Abstraksi:
  * `G3`: Bawa yang Penting (pilih 1 dari 3).
  * `G4`: Peta Sederhana (pilih 1 dari 3).
  * `G8`: Pilih 2 Benda Penting dari 4 Opsi (pilih banyak / checkbox).
* [x] **T3.5** Komponen Soal Dekomposisi:
  * `G5`: Rute Bertahap Singgah (pilih 1 dari 3).
  * `G6`: Bangun Rumah Pohon (pilih 1 dari 3).
  * `G9`: Susun Bagian Pengerjaan (susun 3–4 chip ke slot).
* [x] **T3.6** Logic Tombol Cek Nonaktif: Memunculkan label alasan dinamis (misal: `Cek (Pilih 1 arah dulu)`).

## Fase 4 — Bank Soal Naratif & Integrasi Rotasi CT 4-Tahap

**Selesai bila:** Setiap modul memiliki 20 langkah soal naratif yang mengikuti rotasi CT 4-tahap secara presisi.

* [x] **T4.1** Skema Bank Soal (`DATA.questions`):
  * ID Langkah (1–20), Pilar CT (Dekomposisi / Pola / Abstraksi / Algoritma), Narasi Cerita, Template Layar, Opsi/Chip, Jawaban, Petunjuk Eksploratif, Penjelasan.
* [x] **T4.2** Modul Pulau Pertambahan (20 Langkah Utuh):
  * Siklus 1 (L1 Dekomposisi, L2 Pola, L3 Abstraksi, L4 Algoritma).
  * Siklus 2 (L5 Dekomposisi, L6 Pola, L7 Abstraksi, L8 Algoritma).
  * Siklus 3 (L9 Dekomposisi, L10 Pola, L11 Abstraksi, L12 Algoritma).
  * Siklus 4 (L13 Dekomposisi, L14 Pola, L15 Abstraksi, L16 Algoritma).
  * Siklus 5 (L17 Dekomposisi, L18 Pola, L19 Abstraksi, L20 Algoritma Puncak).
* [x] **T4.3** Layar `S10` Ringkasan Petualangan Modul: Ditampilkan setelah Langkah 20 selesai, opsi "Lanjut ke Modul Lain" atau "Ke Beranda".

## Fase 5 — Aksesibilitas, Modal Overlay, & Audit Aturan Keras

**Selesai bila:** Aplikasi lolos audit aksesibilitas, bebas dari kata terlarang, dan tidak melanggar aturan keras `rules.md`.

* [x] **T5.1** Audit Aksesibilitas Keyboard & Screen Reader: Urutan Tab logis, `aria-live="polite"` untuk umpan balik soal, label aksesibel pada ikon.
* [x] **T5.2** Audit Pembesaran Teks 150% (A++): Bebas dari komponen terpotong atau tumpang tindih pada layar 800×360 px.
* [x] **T5.3** Audit Tanpa Penilaian & Tanpa Warna Merah:
  * [x] Tidak ada variabel/teks `score`, `points`, `rank`, `level`, `timer`, `lives`.
  * [x] Tidak ada kode warna merah (hue 345°–15°).
  * [x] Tidak ada kata `Salah!`, `Gagal`, `Kalah`, `Menang`, `Skor`.
* [x] **T5.4** Audit Interaksi: Bebas dari ketergantungan gestur *drag-and-drop* atau tekan lama.
* [x] **T5.5** Pengujian Lintas Perangkat (Potret vs Lanskap): Layar `X1` muncul tepat saat perangkat berorientasi potret.

## Ringkasan Progres Layar Prototipe (Total 10 Layar Utama + Template Soal)

* [x] `S1` Splash Screen
* [x] `S2_HOME` Homescreen / Menu Utama
* [x] `S3_LOGIN` Form Login Akun / QR Code
* [x] `S4_JENJANG` Pilih Jenjang Belajar
* [x] `S5_MODUL` Beranda Modul Ajar (Pulau)
* [x] `S6_PETA` Peta Petualangan 20 Langkah
* [x] `SOAL` Layar Soal Naratif (Template `S6`, `S6b`, `G1`–`G9`)
* [x] `S10` Ringkasan Petualangan Modul
* [x] `S11_SET` Modal Pengaturan Aksesibilitas (Overlay)
* [x] `X1` Layar Peringatan Putar Layar (Potret)
