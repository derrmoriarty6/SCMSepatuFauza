# Sistem Informasi Pengolahan Kasir Berbasis Model WaterFall
## Pada Toko Sepatu Fauza
**Tema:** SCM (Supply Chain Management)

---

### Daftar Anggota Kelompok
1. **Nur Syafira Sihombing** (NIM: 24220033)
2. **Ratna Engeli** (NIM: 24220035)
3. **Siti Fauza Adawiyah Br Damanik** (NIM: 24220041)

---

### Penjelasan Program
Project **SCMSepatuFauza** merupakan Sistem Informasi Pengolahan Kasir untuk Toko Sepatu Fauza yang dikembangkan menggunakan **Visual Basic .NET (VB.NET)** dan **MySQL** sebagai database. Aplikasi ini menerapkan pola *Supply Chain Management* sederhana yang mengelola entitas master (Sepatu, Supplier, Kategori) hingga terjadinya transaksi penjualan (Kasir).

Program ini dibangun berdasarkan struktur dan standarisasi CRUD (Create, Read, Update, Delete) yang diadaptasi dari referensi *project latihan (AplNilaiMhs)* sesuai arahan dosen. 

#### Arsitektur dan Komponen Utama:
1. **Database (`db_sepatu_fauza`)**:
   - `tbladmin`: Menyimpan data username dan password untuk fitur Login.
   - `tblsepatu`: Data master produk sepatu (dengan default Merk = "Bunut").
   - `tblsupplier`: Data pemasok / distributor sepatu ke toko.
   - `tblkategori`: Kategori sepatu (Pria, Wanita, Anak-anak).
   - `tbltransaksi`: Data transaksi penjualan kasir (pembelian sepatu oleh pelanggan).
   - `querytransaksi`: Sebuah *VIEW* yang menggabungkan (JOIN) tabel transaksi dengan tabel master untuk menampilkan data penjualan yang informatif di layar kasir.

2. **Koneksi Database (`BukaKoneksi.vb`)**:
   - Modul ini menggunakan `MySql.Data.MySqlClient` untuk melakukan koneksi ke database. Semua form akan memanggil `Call KoneksiKeDatabase()` sebelum melakukan operasi data.

3. **Form Login (`FormLogin`)**:
   - Merupakan gerbang keamanan aplikasi. Pengguna (Admin/Kasir) harus memasukkan *Username* dan *Password* yang valid (berdasarkan `tbladmin`) untuk dapat mengakses Menu Utama.

4. **Menu Utama (`F_MenuUtama`)**:
   - Form navigasi (MDI / Dashboard) yang mengarahkan pengguna ke berbagai form data master, proses transaksi, maupun pencarian.

5. **Form Data Master (`FormSepatu`, `FormSupplier`, `FormKategori`)**:
   - Form-form ini menerapkan konsep CRUD lengkap. Pengguna dapat menambah (SAVE), mengubah (EDIT), menghapus (DELETE), serta melakukan pencarian data. Komponen utama yang digunakan untuk menampilkan data adalah `ListView`.

6. **Form Transaksi Kasir (`FormTransaksi`)**:
   - Form ini menangani proses utama kasir. Pengguna dimudahkan dengan adanya fitur form pencarian *popup* (`FormCariSepatu`, `FormCariSupplier`, `FormCariKategori`) saat menginput data. Sistem akan mengkalkulasi **Total Harga** secara otomatis berdasarkan rumus: `(Jumlah * Harga Satuan) - (Nilai Persentase Diskon)`.

---

### Cara Instalasi dan Penggunaan
1. **Persiapan Database**:
   - Pastikan XAMPP (Apache & MySQL) berjalan.
   - Buka `phpMyAdmin` (http://localhost/phpmyadmin).
   - Impor (Import) file `db_sepatu_fauza.sql` yang telah disediakan di folder project ke dalam MySQL.

2. **Menjalankan Program**:
   - Buka file `SCMSepatuFauza.sln` menggunakan Microsoft Visual Studio.
   - Pastikan *Reference* `MySql.Data` sudah terbaca dengan baik.
   - Jalankan program (Tekan F5 atau klik Start).

3. **Login Aplikasi**:
   - Masukkan Username: `admin`
   - Masukkan Password: `admin`
   - Klik **LOGIN**.

4. **Alur Kerja (Workflow)**:
   - Mulailah dengan memasukkan data di **Data Master** (Supplier, Kategori, lalu Sepatu). *Catatan: Data sepatu memerlukan Kode Supplier, pastikan supplier sudah diinput lebih dulu.*
   - Setelah master data terisi, masuk ke menu **Transaksi -> Transaksi Kasir**.
   - Gunakan tombol `...` untuk mencari dan memilih Sepatu, Kategori, dan Supplier secara otomatis.
   - Masukkan `Jumlah` beli dan `Diskon` (jika ada), maka `Total Harga` akan terhitung.
   - Pilih `Metode Bayar` lalu klik **SAVE**.

---
*Dokumen ini disusun untuk melengkapi syarat presentasi Ujian Akhir Semester (UAS) mata kuliah Pemrograman Visual.*
