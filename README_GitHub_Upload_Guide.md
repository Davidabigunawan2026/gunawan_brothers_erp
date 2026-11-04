# Panduan Upload Project ke GitHub Menggunakan Git

Dokumentasi ini menjelaskan langkah-langkah mengunggah project lokal ke
GitHub menggunakan **Git Command Prompt**. Contoh menggunakan project
**Gunawan Brothers ERP** pada Windows.

## 1. Persiapan

Pastikan:

-   Git sudah terpasang di komputer.
-   Akun GitHub sudah tersedia.
-   Repository GitHub sudah dibuat (untuk panduan ini:
    `gunawan_brothers_erp`).
-   Folder project sudah siap.

Contoh struktur folder:

``` text
D:\DAVID\ERP\
├── frontend\
├── .gitignore
├── readme.md
└── inventory.db
```

> Sesuaikan alamat folder dan nama repository dengan project Anda
> sendiri.

## 2. Buka Command Prompt dan masuk ke folder project

``` cmd
cd /d D:\DAVID\ERP
```

Periksa isi folder:

``` cmd
dir /a
```

## 3. Buat file `.gitignore`

File `.gitignore` menentukan file atau folder yang tidak boleh dikirim
ke repository.

Contoh isi `.gitignore` untuk project ERP:

``` gitignore
# Database files
*.db
*.sqlite
*.sqlite3
*.sqbpro
*.db-journal
*.db-wal
*.db-shm

# Dependencies
node_modules/
frontend/node_modules/

# Build files
frontend/dist/

# Environment files
.env
.env.*

# Logs
*.log

# Editor
.vscode/
```

Simpan file dengan nama tepat **`.gitignore`**, bukan `.gitignore.txt`,
di folder utama project.

**Penting:** Jangan upload database yang berisi data pribadi, data
perusahaan, kredensial, atau informasi rahasia ke repository Public.

## 4. Inisialisasi Git

Jalankan:

``` cmd
git init
```

Perintah ini membuat repository Git lokal di folder project.

Periksa status:

``` cmd
git status --short
```

## 5. Periksa apakah database diabaikan

Jalankan:

``` cmd
git check-ignore -v inventory.db
```

Jika aturan `.gitignore` bekerja, Git akan menampilkan aturan yang
mengabaikan `inventory.db`.

Periksa juga file backup database, jika ada:

``` cmd
git check-ignore -v inventory_stock_trans.sqbpro
```

Ganti nama file sesuai file database yang ada di project.

> Jika perintah tidak menampilkan hasil, periksa kembali nama file,
> lokasi `.gitignore`, dan pola aturannya. Jangan lanjut sebelum yakin
> database yang harus dirahasiakan tidak akan ikut diunggah.

## 6. Tambahkan file project ke staging area

``` cmd
git add .
```

Periksa file yang akan di-commit:

``` cmd
git status
```

Pastikan file database, file rahasia, `.env`, dan `node_modules` tidak
masuk daftar **Changes to be committed**.

Jika ada file yang tidak sengaja masuk staging, keluarkan dengan:

``` cmd
git rm --cached nama_file
```

Untuk folder:

``` cmd
git rm -r --cached nama_folder
```

Kemudian periksa kembali `git status`. Perintah `--cached` mengeluarkan
file dari Git staging/tracking, tetapi mempertahankan file lokal.

## 7. Buat commit pertama

``` cmd
git commit -m "Initial commit: Gunawan Brothers ERP"
```

Commit menyimpan snapshot perubahan project ke riwayat Git lokal.

Jika Git meminta identitas pembuat commit, atur nama dan email:

``` cmd
git config --global user.name "Nama Anda"
git config --global user.email "email-github-anda@example.com"
```

Gunakan email yang sesuai dengan pengaturan akun GitHub Anda. Setelah
itu, ulangi perintah `git commit`.

## 8. Hubungkan repository lokal dengan GitHub

Buat repository baru di GitHub melalui situs GitHub. Untuk contoh ini,
URL repository adalah:

``` text
https://github.com/Davidabigunawan2026/gunawan_brothers_erp.git
```

Tambahkan alamat remote:

``` cmd
git remote add origin https://github.com/Davidabigunawan2026/gunawan_brothers_erp.git
```

Periksa remote:

``` cmd
git remote -v
```

Jika remote `origin` sudah pernah ditambahkan dan URL-nya perlu
diperbaiki, gunakan:

``` cmd
git remote set-url origin https://github.com/Davidabigunawan2026/gunawan_brothers_erp.git
```

## 9. Gunakan branch `main`

``` cmd
git branch -M main
```

Perintah ini mengganti nama branch aktif menjadi `main`.

## 10. Upload project ke GitHub (push)

``` cmd
git push -u origin main
```

Tunggu sampai proses selesai. Jika berhasil, output biasanya menunjukkan
branch `main` telah dikirim ke `origin/main` dan branch lokal sudah
mengikutinya.

Jika GitHub meminta autentikasi, ikuti proses login yang ditampilkan.
Jangan pernah membagikan password, token, atau kredensial GitHub.

## 11. Verifikasi hasil upload

Buka repository GitHub:

https://github.com/Davidabigunawan2026/gunawan_brothers_erp

Refresh halaman dan periksa:

-   Folder `frontend` tampil.
-   File `.gitignore` tampil.
-   File `readme.md` tampil.
-   Branch yang dipilih adalah `main`.
-   File database dan file rahasia tidak tampil.

**Catatan:** File `.gitignore` hanya mencegah file yang belum dilacak
Git agar tidak ditambahkan. Jika database pernah ter-commit sebelumnya,
menambahkan pola ke `.gitignore` saja tidak menghapusnya dari riwayat
Git. Hapus file tersebut dari tracking/riwayat dengan prosedur yang
tepat, dan anggap kredensial atau data rahasia yang pernah terunggah
sudah terekspos.

------------------------------------------------------------------------

## 12. Cara upload perubahan berikutnya

Setelah project diperbarui, tidak perlu menjalankan `git init` atau
`git remote add origin` lagi. Masuk ke folder project, lalu jalankan:

``` cmd
git status
git add .
git commit -m "Update: deskripsi perubahan"
git push
```

Contoh:

``` cmd
git add .
git commit -m "Add inventory dashboard"
git push
```

GitHub akan menerima commit terbaru dari branch yang sedang terhubung.

## 13. Perintah Git yang sering digunakan

  -----------------------------------------------------------------------
  Perintah                            Fungsi
  ----------------------------------- -----------------------------------
  `git init`                          Membuat repository Git lokal

  `git status`                        Melihat status file

  `git status --short`                Melihat status secara ringkas

  `git add .`                         Menambahkan perubahan ke staging

  `git commit -m "pesan"`             Menyimpan snapshot perubahan

  `git remote -v`                     Melihat alamat remote

  `git remote add origin URL`         Menambahkan remote GitHub

  `git branch -M main`                Mengganti nama branch menjadi
                                      `main`

  `git push -u origin main`           Push pertama ke GitHub

  `git push`                          Mengirim commit berikutnya

  `git pull`                          Mengambil dan menggabungkan
                                      perubahan dari remote

  `git log --oneline`                 Melihat riwayat commit

  `git check-ignore -v file`          Memeriksa aturan `.gitignore` untuk
                                      file
  -----------------------------------------------------------------------

## 14. Catatan penting

1.  Jalankan perintah dari folder utama project yang benar.
2.  Periksa `git status` sebelum commit dan push.
3.  Jangan memasukkan database produksi, password, API key, token, file
    `.env`, atau data sensitif ke repository Public.
4.  Jangan menghapus atau mengganti file database lokal hanya untuk
    mengunggah source code.
5.  Jika muncul error, baca pesan error terlebih dahulu. Jangan
    mengulang perintah secara acak.
6.  Simpan salinan backup database secara terpisah di tempat yang aman.

------------------------------------------------------------------------

**Project:** Gunawan Brothers ERP\
**Repository:** `gunawan_brothers_erp`\
**Frontend:** Vue 3 + Vite\
**Database:** SQLite\
**Version Control:** Git & GitHub

*Dokumen panduan upload project ke GitHub --- Gunawan Brothers.*
