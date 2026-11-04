# ThinkAble — Aturan Desain (Revisi v2.0)

Aturan ini berlaku untuk seluruh prototipe HTML `thinkable.html`. Jika ada konflik: **user-flow / PRD v2.0 menang untuk alur navigasi**, **`rules.md` menang untuk batasan perilaku dan visual**. Aturan bertanda **[KERAS]** tidak boleh dilanggar dalam kondisi apa pun.

---

## 1. Filosofi

ThinkAble mengajak anak mencoba, bukan menilai. Setiap layar harus terasa aman, tenang, dan menghargai usaha. Kemajuan ditulis sebagai catatan atau jejak petualangan ("Kamu sudah mencoba 5 langkah di Pulau Pertambahan"), bukan angka penilaian, persentase, atau peringkat.

---

## 2. Aturan Keras (Hard Rules)

- **[KERAS] Tanpa penilaian:** tidak ada skor, poin, bintang (sebagai penghargaan), peringkat, nyawa, timer/hitung mundur, atau gembok level. Dalam kode: dilarang ada variabel, kelas, atribut, atau teks bernama `score`, `points`, `rank`, `lives`, `timer`, `level`.
- **[KERAS] Tanpa merah** untuk kesalahan. Gunakan warna hangat `--almost` (#E08A00) + ikon info (`i-info`) + teks ramah.
- **[KERAS] Makna tidak hanya lewat warna.** Selalu padukan warna + ikon + teks atau bentuk (contoh: ubin G2 dibedakan bentuk & motif garis, bukan hanya warna).
- **[KERAS] Landscape terkunci**, acuan 800×360 px (rasio 20:9) dengan `transform: scale()` (contain). Mode potret (*portrait*) menampilkan layar `X1` (Putar Layar).
- **[KERAS] Target sentuh ≥ 48 px. Teks ≥ 14 sp.** Layout utuh dan tidak terpotong pada pembesaran teks 150% (A++).
- **[KERAS] Hanya ketuk.** Tidak ada seret-dan-lepas (*drag-and-drop*) sebagai satu-satunya cara interaksi. Susun langkah memakai ketuk chip ke slot.
- **[KERAS] Teks terpusat dari `STR`.** Semua teks antarmuka berasal dari objek `STR` (Bahasa Indonesia), bukan *hardcode* di markup.
- **[KERAS] Jawaban benar tidak tampil sebelum salah ke-2.** 
  - *Salah ke-1*: Menampilkan petunjuk hangat + mengosongkan slot jawaban.
  - *Salah ke-2*: Menampilkan jawaban benar + penjelasan + tombol "Lanjut" (tanpa percabangan soal serupa).
- **[KERAS] Modal Setting ⚙️ melayang (overlay).** Pengaturan `S11` dapat dibuka kapan saja tanpa mereset atau mengosongkan progres/jawaban aktif di latar belakang.

---

## 3. Istilah dan Kata Baku

### Istilah Baku
| Pakai | Jangan pakai |
|---|---|
| Algoritma, Pola, Abstraksi, **Dekomposisi** | "Pecah", "Pecah Masalah" |
| **Peserta** / **Petualang** | Siswa, murid, anak (sebagai peran) |
| **Jenjang**, **Fase** | Tingkat kelas, grade |
| **Modul Ajar**, **Pulau** | Stage, map, level |
| **Langkah** (1–20) | Level 1–20, stage |
| **Percobaan** | Tes, kuis, ujian |

### Kata Terlarang di Antarmuka
`Salah!`, `Gagal`, `Skor`, `Level`, `Peringkat`, `Kalah`, `Menang`, `Nilai`, `Poin`, `Bintang` (sebagai penghargaan).

### Nada Bahasa
- Kalimat pendek, positif, satu gagasan per kalimat.
- Salah ke-1: "Belum tepat. Coba lagi ya!" + petunjuk hangat.
- Salah ke-2: "Yuk lihat jawabannya" + penjelasan visual.
- Benar: "Tepat sekali!" (percobaan 1) atau "Berhasil! Kamu menemukan jalannya." (percobaan 2 / dibantu petunjuk).
- Selesai modul: "Hebat sudah menyelesaikan petualangan ini!", bukan pujian berbasis statistik hasil.
- Kemajuan: "Kamu sudah mencoba 5 langkah di Pulau Pertambahan". Jangan gunakan persentase atau "n dari 20 selesai".

---

## 4. Tata Letak & Navigasi

- Bingkai tetap **800×360 px**, padding **8 px atas/bawah, 48 px kiri/kanan**.
- Bilah atas (*header*) minimal **38 px**: kiri tombol Kembali (`‹`), tengah judul layar / indikator langkah, kanan ikon ⚙️ Pengaturan & Profil.
- Skala bingkai memakai `transform: scale()` (contain). Pengaturan ukuran teks pengguna mengabaikan skala dan mengubah `font-size` dasar dasar (100%, 125%, 150%).
- Satu aksi utama per layar di kanan bawah. Aksi sekunder tombol garis tepi (`.b2`), aksi opsional garis putus-putus (`.bx`).

---

## 5. Token Warna (CSS Variables)

| Token | Nilai Hex | Pemakaian |
|---|---|---|
| `--ink` | `#1B2F63` | Teks utama, border tebal (2–3 px), tombol utama |
| `--bg` | `#F6F8FF` | Latar belakang layar (mode terang) |
| `--surface` | `#FFFFFF` | Latar kartu, modal, slot |
| `--pes` / `--pes-bg` | `#3D7BFF` / `#DCE8FF` | Aksen Peserta, petunjuk, fokus, tombol aktif |
| `--ok` / `--ok-bg` | `#2FB36B` / `#DDF6E8` | Umpan balik benar (`A1`, `A2`, `A3`) |
| `--almost` / `--almost-bg` | `#E08A00` / `#FFF0CC` | Belum tepat (`A4`, `A5`, `A6`), dialog, petunjuk |
| `--line` / `--muted` | `#C9C9C2` / `#5F5F5A` | Garis pembatas, teks sekunder |

*Aturan Warna:*
- **Dilarang keras menggunakan warna merah** (hue 345°–15°) di token atau CSS mana pun.
- Kontras teks minimal **4.5:1**; pada Mode Kontras Tinggi minimal **7:1** (`--ink` #000, garis 3 px, tanpa latar pola).
- Mode Tenang menurunkan saturasi 40% dan mematikan animasi.

---

## 6. Tipografi

- **Fredoka 700**: Judul layar (20 sp), tombol (16 sp), angka langkah.
- **Atkinson Hyperlegible 400/700**: Instruksi, isi cerita, dan penjelasan (14–16 sp, **minimal 14 sp**).
- Fallback font: `system-ui, sans-serif`. Tinggi baris 1.25–1.4.

---

## 7. Sistem Alur Jawaban 2-Tahap Engine

```
[Soal Percobaan 1] ──(Salah 1)──> [Layar A4/A5: Petunjuk Warm + Slot Kosong] ──(Coba Lagi)──> [Soal Percobaan 2]
       │                                                                                             │
    (Benar)                                                                                       (Salah 2)
       │                                                                                             │
       ▼                                                                                             ▼
[Layar A1/A2/A3: Benar]                                                                 [Layar A6-A9: Penjelasan]
       │                                                                                             │
       └─────────────────────────────> [Tombol "Lanjut"] <───────────────────────────────────────────┘
```

1. **Tombol Cek Nonaktif**: Tidak disembunyikan. Tampil garis putus + label alasan lengkap, misal `Cek (Pilih 1 arah dulu)` atau `Cek (Isi 3 langkah dulu)`.
2. **Tanpa Percabangan Soal Serupa**: Setelah salah ke-2 dan melihat penjelasan di A6–A9, anak langsung mengetuk tombol **Lanjut** ke langkah berikutnya.

---

## 8. Rotasi CT 4-Tahap di Peta 20 Langkah Modul

Dalam 20 langkah petualangan di setiap modul, tipe soal CT berputar konsisten tiap 4 langkah:
- **Langkah 1, 5, 9, 13, 17**: **Dekomposisi** (Membagi masalah besar menjadi bagian kecil — `G9`, `G6`).
- **Langkah 2, 6, 10, 14, 18**: **Pola** (Mencari urutan / irama berulang — `G1`, `G2`, `G7`).
- **Langkah 3, 7, 11, 15, 19**: **Abstraksi** (Fokus pada informasi penting saja — `G3`, `G4`, `G8`).
- **Langkah 4, 8, 12, 16, 20**: **Algoritma** (Menyusun urutan langkah logis — `S6`, `S6b`).

---

## 9. Pengaturan Aksesibilitas (`S11`)

- Dapat diakses dari **Homescreen (`S2_HOME`)** atau dari ikon **⚙️ Pengaturan** di bilah atas saat pengerjaan soal.
- Dipanggil sebagai **overlay modal**. Pengerjaan soal di latar belakang terjeda tanpa mereset status jawaban.
- Opsi Pengaturan: Ukuran Teks (A / A+ / A++), Audio, Getar (Haptic), Kurangi Gerak, Mode Tenang, Kontras Tinggi.

---

## 10. Daftar Periksa Sebelum Menutup Layar / Komponen

- [ ] ID Layar sesuai dengan `PRD v2.0` (`S1`, `S2_HOME`, `S3_LOGIN`, `S4_JENJANG`, `S5_MODUL`, `S6_PETA`, `SOAL`, `S10`, `S11_SET`, `X1`).
- [ ] Tidak ada warna merah, skor, poin, bintang penghargaan, timer, atau nyawa.
- [ ] Warna + Ikon + Teks/Bentuk pada setiap penyampaian makna.
- [ ] Target sentuh ≥ 48 px, teks ≥ 14 px, utuh pada pembesaran teks 150%.
- [ ] Interaksi hanya ketuk; tidak ada *drag-and-drop*.
- [ ] Teks tampilan diambil dari objek `STR`.
- [ ] Fokus keyboard dan pembaca layar (`aria-live`, `aria-label`) lolos audit.
