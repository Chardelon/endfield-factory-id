# Endfield Production DB

Database resep produksi **Arknights: Endfield 1.2.5** dalam format ringkas berbasis ID.

Dibuat oleh **Chardelon**.

Repository:
https://github.com/Chardelon/endfield-factory-id

## Tujuan

Database ini dibuat agar resep produksi Endfield lebih mudah dipakai untuk:

* kalkulator produksi
* analisis rantai bahan
* simulasi kebutuhan mesin
* perhitungan input/output
* pembacaan oleh AI atau program

Format data dibuat ringkas memakai ID. Nama barang dan mesin disimpan satu kali, lalu resep cukup memakai ID agar tidak banyak pengulangan.

## Struktur Folder

```txt
endfield-production-db/
├── README.md
├── data/
│   ├── compact.json
│   └── compact.min.json
├── items/
│   └── items.json
├── machines/
│   └── machines.json
└── recipes/
    └── recipes.json
```

## Isi File

* `items/items.json`
  Kamus ID barang.

* `machines/machines.json`
  Kamus ID mesin atau unit produksi.

* `recipes/recipes.json`
  Daftar resep produksi memakai ID barang dan ID mesin.

* `data/compact.json`
  Gabungan dari items, machines, dan recipes dalam satu file. File ini paling cocok untuk AI atau program.

* `data/compact.min.json`
  Versi kecil/minified dari `compact.json`.

## Format Resep

Setiap resep memakai format array:

```txt
[id, nama, mesin, durasi, input, utama, samping]
```

Keterangan:

* `id` = ID resep.
* `nama` = nama resep.
* `mesin` = ID mesin dari `machines/machines.json`.
* `durasi` = durasi produksi dalam detik.
* `input` = daftar bahan masuk dengan format `[[id_barang, jumlah], ...]`.
* `utama` = hasil utama dengan format `[id_barang, jumlah]`, atau `[]` jika tidak ada hasil utama.
* `samping` = daftar hasil samping dengan format `[[id_barang, jumlah], ...]`, atau `[]` jika tidak ada hasil samping.

Contoh:

```json
[1, "Produksi Contoh", 3, 10, [[12, 2], [15, 1]], [20, 1], [[21, 1]]]
```

Artinya:

* Resep ID `1`.
* Nama resep: `Produksi Contoh`.
* Menggunakan mesin ID `3`.
* Durasi produksi `10` detik.
* Input:

  * barang ID `12` sebanyak `2`
  * barang ID `15` sebanyak `1`
* Hasil utama:

  * barang ID `20` sebanyak `1`
* Hasil samping:

  * barang ID `21` sebanyak `1`

## Format Barang

File `items/items.json` berisi pasangan ID dan nama barang.

Contoh:

```json
{
  "1": "Bubuk Originium",
  "2": "Bubuk Originium Padat",
  "3": "Xircon"
}
```

Jika resep memakai:

```json
[[2, 20], [3, 5]]
```

Maka artinya:

* `20` Bubuk Originium Padat
* `5` Xircon

## Format Mesin

File `machines/machines.json` berisi pasangan ID dan nama mesin/unit produksi.

Contoh:

```json
{
  "1": "Unit Pengemas",
  "2": "Unit Giling",
  "3": "Unit Pencacah"
}
```

Jika resep memakai:

```json
"mesin": 1
```

Maka artinya resep tersebut menggunakan:

```txt
Unit Pengemas
```

## Catatan Nama Barang

Nama barang dibuat tidak ambigu, terutama untuk botol atau item yang bisa berisi cairan berbeda.

Contoh:

* `Botol Ferrium kosong`
* `Botol Ferrium berisi Air Bersih`
* `Botol Ferrium berisi Cairan Sisa Proses Xircon`

Ini mencegah item berbeda terlihat sama hanya karena nama dasarnya sama-sama botol.

## Rekomendasi Pemakaian

Untuk AI atau program, gunakan file:

```txt
data/compact.json
```

Raw link:

```txt
https://raw.githubusercontent.com/Chardelon/endfield-factory-id/main/data/compact.json
```

Versi minified:

```txt
https://raw.githubusercontent.com/Chardelon/endfield-factory-id/main/data/compact.min.json
```

## Contoh Prompt ke AI

```txt
Ini database produksi Endfield saya:
https://raw.githubusercontent.com/Chardelon/endfield-factory-id/main/data/compact.json

Hitung bahan mentah untuk membuat 10 Baterai KS.
```

## Versi Data

* Game: **Arknights: Endfield**
* Versi data: **1.2.5**
* Bahasa data: **Indonesia**
* Format: **compact ID**

## Attribution

Data ini disusun dan diolah oleh **Chardelon**.

Jika memakai, menyalin, memodifikasi, atau membagikan database ini, mohon cantumkan atribusi:

```txt
Data resep produksi Endfield 1.2.5 oleh Chardelon
```

## Disclaimer

Repository ini adalah database komunitas/fan-made untuk membantu analisis produksi di Arknights: Endfield.

Arknights: Endfield dan seluruh aset/nama terkait adalah milik pemegang hak cipta masing-masing.
