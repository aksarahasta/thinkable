# ThinkAble — User Flow Revisi (Versi 2.0)

Berdasarkan diagram alur resmi revisi v2.0 (Splash → Homescreen → Login → Jenjang → Modul → Peta 20 Langkah → Engine 2-Tahap).

## 1. Alur Navigasi Utama Aplikasi

```mermaid
flowchart TD
  S1["S1: Splash Screen\n(Penyambut Awal & Maskot)"] -->|"Animasi Otomatis / Ketuk Layar"| S2_HOME["S2: Homescreen / Menu Utama\n(Play, Suara, Bahasa, Setting, Status Login)"]
  
  S2_HOME -->|"Ketuk 'Play'"| S3_CHK{"Sudah Login?"}
  S2_HOME -->|"Ketuk 'Setting'"| S11_SET["S11: Modal Pengaturan Utama (Overlay)"]
  S2_HOME -.-|"Toggle 'Suara' & 'Bahasa'"| S2_HOME
  
  S3_CHK -->|"Belum Login"| S3_LOGIN["S3: Form Login Akun / Pindai QR"]
  S3_CHK -->|"Sudah Login"| S4_JENJANG["S4: Pilih Jenjang Belajar"]
  S3_LOGIN -->|"Login Berhasil"| S4_JENJANG
  
  S4_JENJANG -->|"Pilih Jenjang (Fase A / B)"| S5_MODUL["S5: Beranda Modul Ajar (Pulau)"]
  S4_JENJANG -->|"Kembali ke Menu Utama"| S2_HOME
  
  S5_MODUL -->|"Pilih Modul (misal: Pertambahan)"| S6_PETA["S6: Peta Petualangan (20 Langkah)"]
  S5_MODUL -->|"Kembali"| S4_JENJANG
  
  S6_PETA -->|"Pilih Langkah 1 s/d 20"| SOAL["Layar Soal Naratif (Siklus CT 4-Tahap)"]
  S6_PETA -->|"Kembali"| S5_MODUL
  
  SOAL -->|"Ketuk Ikon ⚙️ Setting di Header"| S11_SET
  SOAL --> ENGINE["Engine Evaluasi Jawaban 2-Tahap"]
  ENGINE -->|"Modul Selesai"| S10["S10: Ringkasan Petualangan"]
  
  S10 -->|"Lanjut Langkah"| S6_PETA
  S10 -->|"Ke Beranda Modul"| S5_MODUL

  classDef main fill:#DCE8FF,stroke:#3D7BFF,color:#1B2F63;
  classDef sub fill:#FFF0CC,stroke:#E08A00,color:#1B2F63;
  class S1,S2_HOME,S3_LOGIN,S4_JENJANG,S5_MODUL,S6_PETA,SOAL main;
  class S11_SET,S10,ENGINE sub;
```

## 2. Mesin Evaluasi Jawaban 2-Tahap

```mermaid
flowchart TB
    Q1["Layar Soal (Percobaan 1)"] -- "Ketuk 'Petunjuk'" --> H1["Kotak Petunjuk Eksploratif"]
    H1 --> Q1
    Q1 -- "Pilih/Susun & Ketuk 'Cek'" --> C1{"Hasil Percobaan 1"}
    
    C1 -- "Benar (Tanpa Petunjuk)" --> A1["A1/A2: 'Tepat sekali!'"]
    C1 -- "Benar (Pakai Petunjuk)" --> A3["A3: 'Berhasil! Kamu menemukan jalannya'"]
    C1 -- "Salah ke-1" --> A4["A4/A5: 'Belum tepat. Coba lagi ya!' + Petunjuk Warm Color"]
    
    A4 -- "Ketuk 'Coba Lagi'" --> Q2["Layar Soal (Percobaan 2 — Slot Terkosongkan)"]
    Q2 -- "Pilih/Susun & Ketuk 'Cek'" --> C2{"Hasil Percobaan 2"}
    
    C2 -- "Benar" --> A3
    C2 -- "Salah ke-2" --> A6["A6–A9: 'Yuk lihat jawabannya' (Jawaban Benar + Penjelasan)"]
    
    A1 --> NEXT{"Sudah Langkah ke-20?"}
    A3 --> NEXT
    A6 -- "Ketuk 'Lanjut'" --> NEXT
    
    NEXT -- "Belum" --> S5["Kembali ke Peta Langkah Modul"]
    NEXT -- "Ya" --> S10["S10: Modul Selesai"]

    classDef ok fill:#DDF6E8,stroke:#2FB36B,color:#1B2F63;
    classDef warm fill:#FFF0CC,stroke:#E08A00,color:#1B2F63;
    class A1,A3 ok;
    class H1,A4,A6 warm;
```
