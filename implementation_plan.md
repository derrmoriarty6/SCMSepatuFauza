# Sistem Informasi Pengolahan Kasir Toko Sepatu Fauza (SCM)

## Latar Belakang

Membuat project UAS Pemrograman Visual berupa **Sistem Informasi Pengolahan Kasir Berbasis Model WaterFall** pada **Toko Sepatu Fauza** dengan tema **SCM (Supply Chain Management)**. Project ini dibuat berdasarkan referensi code dari project latihan `AplNilaiMhs`, dengan pola CRUD yang sama (MySql.Data, ListView, Module koneksi, dsb).

## Mapping dari AplNilaiMhs → SCMSepatuFauza

| AplNilaiMhs (Referensi) | SCMSepatuFauza (Project Baru) | Keterangan |
|---|---|---|
| `tblmahasiswa` | `tblsepatu` | Data master produk sepatu |
| `tbldosen` | `tblsupplier` | Data master supplier |
| `tblmatakuliah` | `tblkategori` | Data master kategori sepatu |
| `tblnilai` + `querynilai` | `tbltransaksi` + `querytransaksi` | Transaksi penjualan (proses kasir) |
| `FormMahasiswa` | `FormSepatu` | CRUD data sepatu |
| `FormDosen` | `FormSupplier` | CRUD data supplier |
| `FormMataKuliah` | `FormKategori` | CRUD data kategori |
| `FormNilai` | `FormTransaksi` | Proses transaksi kasir |
| `FormCariMhs` | `FormCariSepatu` | Cari data sepatu |
| `FormCariDosen` | `FormCariSupplier` | Cari data supplier (untuk transaksi) |
| `FormCariMtk` | `FormCariKategori` | Cari data kategori (untuk transaksi) |
| `F_MenuUtama` | `F_MenuUtama` | Menu utama aplikasi |
| `BukaKoneksi` | `BukaKoneksi` | Module koneksi ke database |

## Desain Database: `db_sepatu_fauza`

### Tabel `tblsepatu` (Master Produk)
| Field | Tipe | Keterangan |
|---|---|---|
| `kd_sepatu` | VARCHAR(10) PK | Kode sepatu |
| `nama_sepatu` | VARCHAR(50) | Nama produk sepatu |
| `merk` | VARCHAR(30) | Merk sepatu |
| `ukuran` | VARCHAR(10) | Ukuran sepatu |
| `warna` | VARCHAR(20) | Warna sepatu |
| `jenis` | VARCHAR(20) | Jenis (Sneakers/Formal/Casual/Sport/Boots) |
| `stok` | INT(5) | Jumlah stok |
| `harga` | DOUBLE | Harga satuan |
| `kd_supplier` | VARCHAR(10) | FK ke tblsupplier |

### Tabel `tblsupplier` (Master Supplier)
| Field | Tipe | Keterangan |
|---|---|---|
| `kd_supplier` | VARCHAR(10) PK | Kode supplier |
| `nama_supplier` | VARCHAR(50) | Nama supplier |
| `alamat` | VARCHAR(100) | Alamat supplier |
| `telp` | VARCHAR(15) | Telepon supplier |

### Tabel `tblkategori` (Master Kategori)
| Field | Tipe | Keterangan |
|---|---|---|
| `kd_kategori` | VARCHAR(10) PK | Kode kategori |
| `nama_kategori` | VARCHAR(30) | Nama kategori |
| `keterangan` | VARCHAR(100) | Deskripsi kategori |

### Tabel `tbltransaksi` (Transaksi Penjualan)
| Field | Tipe | Keterangan |
|---|---|---|
| `id_transaksi` | INT(11) PK AUTO_INCREMENT | ID transaksi |
| `tgl_transaksi` | DATE | Tanggal transaksi |
| `kd_sepatu` | VARCHAR(10) | FK ke tblsepatu |
| `kd_kategori` | VARCHAR(10) | FK ke tblkategori |
| `kd_supplier` | VARCHAR(10) | FK ke tblsupplier |
| `jumlah` | INT(5) | Jumlah beli |
| `harga_satuan` | DOUBLE | Harga per item |
| `diskon` | DOUBLE | Persentase diskon |
| `total_harga` | DOUBLE | Total bayar |
| `metode_bayar` | VARCHAR(20) | Cash/Transfer/E-Wallet |
| `keterangan` | VARCHAR(50) | Keterangan status |

### View `querytransaksi`
JOIN `tbltransaksi` + `tblsepatu` + `tblsupplier` + `tblkategori` untuk menampilkan data lengkap di ListView.

## Tema Design VB.NET — Nuansa Toko Sepatu

- **Warna utama**: Dark mode (ControlDarkDark) konsisten dengan referensi
- **Aksen warna**: Coklat/Tan (#8B4513, #D2691E) — nuansa kulit/sepatu
- **Font judul**: Microsoft Sans Serif 14pt Bold (sama dengan referensi)
- **Panel utama**: BackColor = DarkSlateGray / SaddleBrown
- **Judul form**: Menyesuaikan konteks toko sepatu

## Proposed Changes

### Database
#### [NEW] [db_sepatu_fauza.sql](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/db_sepatu_fauza.sql)
File SQL lengkap: CREATE DATABASE, CREATE TABLE (4 tabel + 1 view), sample data, dan indexes.

---

### Module Koneksi
#### [NEW] [BukaKoneksi.vb](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/BukaKoneksi.vb)
Module koneksi ke `db_sepatu_fauza` — pola identik dengan referensi.

---

### Form Menu Utama
#### [NEW] [F_MenuUtama.vb](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/F_MenuUtama.vb)
#### [NEW] [F_MenuUtama.Designer.vb](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/F_MenuUtama.Designer.vb)
#### [NEW] [F_MenuUtama.resx](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/F_MenuUtama.resx)
Menu: Data Master (Sepatu, Supplier, Kategori) → Transaksi → Cari Data → Laporan → Keluar

---

### Form CRUD Data Sepatu (≈ FormMahasiswa)
#### [NEW] [FormSepatu.vb](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormSepatu.vb)
#### [NEW] [FormSepatu.Designer.vb](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormSepatu.Designer.vb)
#### [NEW] [FormSepatu.resx](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormSepatu.resx)
Fields: Kode Sepatu, Nama, Merk, Ukuran, Warna, Jenis (CheckBox), Stok, Harga, Supplier. Pola CRUD persis referensi.

---

### Form CRUD Data Supplier (≈ FormDosen)
#### [NEW] [FormSupplier.vb](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormSupplier.vb)
#### [NEW] [FormSupplier.Designer.vb](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormSupplier.Designer.vb)
#### [NEW] [FormSupplier.resx](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormSupplier.resx)
Fields: Kode Supplier, Nama Supplier, Alamat, Telepon. Pola CRUD identik.

---

### Form CRUD Data Kategori (≈ FormMataKuliah)
#### [NEW] [FormKategori.vb](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormKategori.vb)
#### [NEW] [FormKategori.Designer.vb](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormKategori.Designer.vb)
#### [NEW] [FormKategori.resx](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormKategori.resx)
Fields: Kode Kategori, Nama Kategori, Keterangan. Pola CRUD identik.

---

### Form Transaksi Kasir (≈ FormNilai)
#### [NEW] [FormTransaksi.vb](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormTransaksi.vb)
#### [NEW] [FormTransaksi.Designer.vb](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormTransaksi.Designer.vb)
#### [NEW] [FormTransaksi.resx](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/FormTransaksi.resx)
Proses transaksi: pilih sepatu, supplier, kategori via popup → input jumlah → proses hitung (diskon, total) → simpan. Pola mirip FormNilai.

---

### Form Pencarian
#### [NEW] FormCariSepatu (.vb, .Designer.vb, .resx) — ≈ FormCariMhs
#### [NEW] FormCariSupplier (.vb, .Designer.vb, .resx) — ≈ FormCariDosen
#### [NEW] FormCariKategori (.vb, .Designer.vb, .resx) — ≈ FormCariMtk

---

### Project Configuration
#### [MODIFY] [SCMSepatuFauza.vbproj](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/SCMSepatuFauza.vbproj)
Tambah reference MySql.Data, tambah semua form files ke ItemGroup.

#### [NEW] [App.config](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/SCMSepatuFauza/App.config)
#### [MODIFY] My Project files (Application.myapp, Application.Designer.vb, AssemblyInfo.vb, Resources, Settings)

---

### Dokumentasi
#### [NEW] [Penjelasan.md](file:///c:/MAWAN%20KULIAH/SM4/Pemrograman%20Visual/PROJECT%20J/Pemrograman%20Visual/SCMSepatuFauza/Penjelasan.md)
Dokumen lengkap penjelasan code dan program untuk presentasi ke dosen.

## Open Questions

> [!IMPORTANT]
> 1. **Apakah form dan tabel yang saya rancang sudah sesuai** dengan kebutuhan UAS kamu? (Sepatu, Supplier, Kategori, Transaksi)
> 2. **Apakah perlu ada form Login** sebelum masuk ke Menu Utama?
> 3. **Apakah ada fitur tambahan** yang diminta dosen selain CRUD standar? (misalnya: cetak struk, laporan penjualan, grafik, dll)
> 4. **Nama anggota kelompok** untuk dicantumkan di About/dokumentasi?

## Verification Plan

### Manual Verification
1. Buka project di Visual Studio → pastikan build sukses tanpa error
2. Import `db_sepatu_fauza.sql` ke PHPMyAdmin → pastikan semua tabel dan view terbuat
3. Jalankan aplikasi → test semua operasi CRUD di setiap form
4. Test pencarian data di setiap form Cari
5. Test proses transaksi kasir (hitung diskon, total)
