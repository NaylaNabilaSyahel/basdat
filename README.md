# basdat

# Sistem Perpustakaan Digital

Sistem ini dirancang untuk mengelola manajemen perpustakaan digital, termasuk anggota, buku, peminjaman, pengembalian, dan petugas.

## ERD (Entity Relationship Diagram)

Berikut adalah ERD untuk sistem perpustakaan digital:

```mermaid
erDiagram
    ANGGOTA ||--o{ PEMINJAMAN : melakukan
    PEMINJAMAN ||--o{ PENGEMBALIAN : memiliki
    PEMINJAMAN }|--|| PETUGAS : dicatat_oleh
    PENGEMBALIAN }|--|| PETUGAS : dicatat_oleh
    PEMINJAMAN }|--|| EKSEMPLAR : meminjam
    EKSEMPLAR }|--|| BUKU : merupakan_bagian_dari
    BUKU ||--o{ KATEGORI_BUKU : memiliki
    KATEGORI_BUKU }|--|| KATEGORI : termasuk_dalam

    ANGGOTA {
        ID_anggota INT PK
        Nama VARCHAR
        Alamat TEXT
        No_Telepon VARCHAR
        Email VARCHAR
    }
    
    BUKU {
        ID_buku INT PK
        Judul VARCHAR
        Penulis VARCHAR
        Penerbit VARCHAR
        Tahun_Terbit INT
    }
    
    EKSEMPLAR {
        ID_eksemplar INT PK
        ID_buku INT FK
        Status ENUM("Tersedia", "Dipinjam")
    }
    
    KATEGORI {
        ID_kategori INT PK
        Nama_Kategori VARCHAR
    }
    
    KATEGORI_BUKU {
        ID_buku INT FK
        ID_kategori INT FK
    }
    
    PEMINJAMAN {
        ID_peminjaman INT PK
        ID_anggota INT FK
        ID_eksemplar INT FK
        ID_petugas INT FK
        Tanggal_Pinjam DATE
        Batas_Pengembalian DATE
        Status_Pengembalian ENUM("Dipinjam", "Dikembalikan")
    }
    
    PENGEMBALIAN {
        ID_pengembalian INT PK
        ID_peminjaman INT FK
        ID_petugas INT FK
        Tanggal_Kembali DATE
        Denda DECIMAL(10,2)
    }
    
    PETUGAS {
        ID_petugas INT PK
        Nama VARCHAR
        Jabatan VARCHAR
        No_Kontak VARCHAR
    }
```

## Deskripsi
- **Anggota**: Pengguna yang terdaftar di perpustakaan.
- **Buku**: Koleksi buku yang tersedia untuk dipinjam.
- **Eksemplar**: Salinan fisik dari buku dengan ID unik.
- **Kategori**: Klasifikasi buku berdasarkan jenisnya.
- **Peminjaman**: Transaksi peminjaman buku oleh anggota.
- **Pengembalian**: Proses pengembalian buku, termasuk pencatatan denda.
- **Petugas**: Staf perpustakaan yang mengelola peminjaman dan pengembalian.

## Cara Menggunakan
1. **Fork dan Clone Repo**
   ```sh
   git clone https://github.com/username/library-system.git
   ```
2. **Jalankan sistem berdasarkan ERD ini**

---
Dikembangkan untuk kebutuhan sistem perpustakaan digital.
