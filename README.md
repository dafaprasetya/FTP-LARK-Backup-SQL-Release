# SQL Backup to Lark Drive & FTP

Aplikasi desktop Windows untuk membackup database MySQL dan PostgreSQL, lalu mengirim hasilnya ke Lark Drive dan, jika diaktifkan, ke server FTP/FTPS. Setiap hasil backup dilaporkan ke grup chat Lark.

Dikembangkan oleh Prahari Tech General Advisor (PTGA).

## Fitur

- Backup MySQL (memakai `mysqldump`) dan PostgreSQL (memakai `pg_dump`).
- Upload ke Lark Drive, dengan folder tujuan yang bisa berbeda untuk setiap database.
- Salinan tambahan ke FTP atau FTPS (explicit TLS), diatur per database.
- Notifikasi ke chat Lark untuk setiap backup yang berhasil atau gagal, ditambah ringkasan di akhir proses.
- Backup manual untuk database yang dipilih, atau backup otomatis setiap hari pada jam tertentu (WIB).
- Opsi menyimpan salinan backup di komputer lokal.
- Log disimpan satu file per proses di folder `logs`, dan bisa dilihat dari aplikasi dengan mengklik item status.
- Lisensi terikat pada perangkat (serial number) dan diaktivasi secara online.

## Persyaratan

- Windows 64-bit.
- Koneksi internet, untuk aktivasi lisensi dan upload ke Lark.
- Akun Lark dengan App ID, App Secret, Chat ID, dan folder Lark Drive tujuan.
- Akses jaringan dari komputer ini ke server database yang akan dibackup.
- Visual C++ Redistributable x64, jika muncul error `VCRUNTIME140.dll` atau `msvcp140.dll` tidak ditemukan.

## Instalasi

1. Unduh rilis terbaru dari halaman [Releases](../../releases) dan ekstrak.
2. Pastikan struktur foldernya seperti berikut:

```
FTP & LARK Backup SQL\
├── App.exe
├── logo.ico
├── assets
    ├── logo.ico
    └── logo.PNG
└── utils\
    ├── mysql\
    └── pgsql\
```

3. Jalankan `App.exe`.

File `key.prstya`, `settings.prstya`, dan `database.prstya` dibuat otomatis oleh aplikasi di folder yang sama dengan `App.exe`. Jangan dipindahkan atau dihapus, kecuali memang ingin mereset konfigurasi.

### PostgreSQL

Backup PostgreSQL membutuhkan `pg_dump`. Pastikan `pg_dump.exe` sudah terpasang dan terdaftar di `PATH` Windows. Gunakan versi yang sama atau lebih baru dari server PostgreSQL yang dibackup. Binary zip (tanpa installer) tersedia di <https://www.enterprisedb.com/download-postgresql-binaries>.

### MySQL

Rilis ini membawa `mysqldump` versi 8.0. Opsi `--column-statistics=0` sudah dipakai, sehingga kompatibel juga dengan server MySQL 5.7 dan MariaDB.

## Penggunaan

### 1. Aktivasi

Saat pertama dibuka, aplikasi menampilkan jendela Aktivasi berisi serial number perangkat. Masukkan license key lalu klik **Aktivasi**. Jika key diganti atau perangkat berpindah, kirim serial number tersebut ke admin.

### 2. Setting

Buka menu **Setting** dan isi:

| Bagian | Isi |
| --- | --- |
| Location | Nama lokasi, ditampilkan di notifikasi Lark |
| Backup time | Jam backup otomatis, format `HH:MM` |
| Local backup dir | Folder penyimpanan salinan lokal (default `backups`) |
| Keep local backup | Simpan salinan backup di komputer ini |
| Lark Profile | API base URL, App ID, App Secret, Chat ID, dan Drive domain |

### 3. Tambah database

Klik **+ Tambah Database**, lalu isi tipe database, host, port, nama database, user, password, dan folder Lark tujuan. Aktifkan **Kirim juga salinan backup ke FTP** jika perlu, lalu isi host, port, user, password, dan direktori FTP. Centang **Gunakan FTPS (TLS)** bila server mendukungnya.

Klik baris pada tabel untuk mengedit database. Menghapus entri hanya menghapus konfigurasinya di aplikasi, database di server tidak terpengaruh.

### 4. Jalankan backup

- **Run Backup**: pilih database dan tujuan (Lark Drive, FTP), lalu backup langsung dijalankan.
- **Auto Backup**: tentukan jam, database, dan tujuan. Backup berjalan otomatis setiap hari selama aplikasi terbuka. Status ditampilkan sebagai ACTIVE atau INACTIVE di bagian atas.

Aplikasi harus tetap berjalan agar backup otomatis dieksekusi.

## Lisensi dan pembelian key

Aplikasi ini membutuhkan license key untuk dijalankan. Key terikat pada satu perangkat dan dapat memiliki masa berlaku. Lisensi dicek ulang sebelum setiap backup, sehingga backup berhenti jika lisensi sudah kedaluwarsa.

Untuk membeli license key, perpanjangan, atau reset perangkat, hubungi:

**dafaprstya@ptga.my.id**

Sertakan nama perusahaan dan serial number perangkat (tampil di jendela Aktivasi dan di bagian bawah aplikasi).

## Pemecahan masalah

| Pesan | Penyebab dan solusi |
| --- | --- |
| Tidak bisa menghubungi server aktivasi | Periksa koneksi internet, proxy, atau firewall. |
| Aktivasi ditolak server (HTTP ...) | Pastikan jam dan zona waktu komputer akurat, lalu coba lagi. |
| key.prstya tidak cocok dengan perangkat ini | File lisensi berasal dari perangkat lain. Aplikasi memindahkannya ke `key.prstya.invalid` dan meminta aktivasi ulang. Hubungi admin untuk reset. |
| License kedaluwarsa | Hubungi admin untuk perpanjangan. |
| mysqldump / pg_dump tidak ditemukan | Pastikan `utils\mysql\bin\mysqldump.exe` ada, atau `pg_dump` ada di `PATH`. |
| Backup gagal tanpa pesan jelas | Buka log di folder `logs` atau klik item status di aplikasi. |

## Keamanan

Password database, App Secret Lark, dan password FTP tersimpan di `settings.prstya` dan `database.prstya` pada komputer ini. Batasi akses ke folder aplikasi hanya untuk pengguna yang berwenang, dan jangan membagikan file-file tersebut.

## Kontak

Prahari Tech General Advisor (PTGA)
Email: dafaprstya@ptga.my.id