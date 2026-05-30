# README — UAS Kalkulus Integral Kelompok 6

## Identitas

| Item | Keterangan |
|------|------------|
| Mata Kuliah | Kalkulus Integral |
| Topik | Misi 3 (Multi-Fase / Piecewise) |
| Skenario | Pemodelan jarak tempuh mobil di jalan tol (3 fase: akselerasi, kecepatan konstan, deselerasi) |
| Kelompok | Kelompok 6 |
| Jumlah anggota | 6 orang |

## File dalam paket ini

| File | Keterangan |
|------|------------|
| `Pemodelan Jarak tempuh mobil di jalan tol.ipynb` | Notebook utama (import, simbolik, numerik, validasi, visualisasi) |
| `README.md` | File ini |

## Cara menjalankan

### Opsi 1: Google Colab (paling mudah, disarankan)

1. Buka <https://colab.research.google.com>
2. **File → Upload notebook** → pilih `Pemodelan Jarak tempuh mobil di jalan tol.ipynb`
3. **Runtime → Run all**
4. Tunggu semua sel selesai (sekitar 10–15 detik)

### Opsi 2: Jupyter lokal

1. Pastikan Python 3.8+ terpasang
2. Install dependensi:

   ```bash
   pip install numpy sympy matplotlib jupyter
   ```

3. Jalankan:

   ```bash
   jupyter notebook "Pemodelan Jarak tempuh mobil di jalan tol.ipynb"
   ```

4. **Cell → Run All**

## Dependensi

| Library | Fungsi di notebook |
|---------|---------------------|
| `numpy` | Komputasi numerik & trapesium (`np.piecewise`, `np.trapezoid`) |
| `sympy` | Komputasi simbolik (`sp.integrate`) |
| `matplotlib` | Visualisasi kurva, area per fase, plot posisi |

**Catatan:**

- Kode kompatibel dengan NumPy 1.x (`np.trapz`) maupun NumPy 2.x (`np.trapezoid`) lewat shim otomatis (`_trapz`) di awal notebook.
- Google Colab saat ini memakai NumPy 2.x; shim sudah menanganinya.

## Ringkasan model dan hasil

### Fungsi piecewise v(t)

$$
v(t) = \begin{cases}
2t & 0 \le t \le 10 & \text{(Fase 1: akselerasi)} \\
20 & 10 < t \le 60 & \text{(Fase 2: konstan)} \\
80 - t & 60 < t \le 80 & \text{(Fase 3: deselerasi)}
\end{cases}
$$

**Kontinuitas terverifikasi** di $t = 10$, $t = 60$, dan $t = 80$.

### Hasil integral per fase

| Fase | Bentuk | Hasil | Verifikasi geometris |
|------|--------|-------|----------------------|
| 1 (akselerasi) | $\int_0^{10} 2t \, dt$ | **100 m** | Segitiga ½·10·20 = 100 m ✓ |
| 2 (konstan) | $\int_{10}^{60} 20 \, dt$ | **1000 m** | Persegi panjang 50·20 = 1000 m ✓ |
| 3 (deselerasi) | $\int_{60}^{80} (80-t) \, dt$ | **200 m** | Segitiga ½·20·20 = 200 m ✓ |
| **TOTAL** | | **1300 m** | **= 1,3 km** |

### Konvergensi metode

- Hasil simbolik (SymPy) per fase = 1300 m total (konsisten dengan jumlah per fase) ✓
- Error numerik vs simbolik: **~0** (orde 10⁻¹³ atau lebih kecil, semata floating-point) ✓
- Metode trapesium **eksak** untuk fungsi linear/konstan, sehingga error matematis nol pada semua resolusi $n$.

## Pembagian peran (6 anggota)

| No | Peran | Nama, NIM |
|----|-------|-----------|
| 1 | Koordinator Proyek | Feza Himawan, 25051130067 |
| 2 | Modeling Lead | Muhammad Saktya Raisyananta, 25051130059 |
| 3 | Symbolic Lead (SymPy) | Tatag Gangsar Pinilih, 25051130080 |
| 4 | Numeric Lead (NumPy) | Arfaeliriva Budiharjo, 25051130030 |
| 5 | Validation Lead (Error Analysis) | Junneo Athashabri, 25051130084 |
| 6 | Visualization & Reporting Lead | Azzahra Ornas Santika, 25051130072 |

## Struktur notebook

| Bagian | Isi |
|--------|-----|
| Model Lead | Parameter model & deskripsi fungsi piecewise 3 fase |
| Symbolic (SymPy) | Solusi simbolik integral per fase dengan `sp.integrate` |
| Numeric (NumPy) | Implementasi `v_num()` dengan `np.piecewise` + metode trapesium per fase |
| Validation | Tabel error absolut & relatif per fase untuk beberapa resolusi $n$ |
| Visualization & Reporting | Plot piecewise 3 warna + arsiran area per fase, dan plot posisi kumulatif $s(t)$ |

## Catatan integritas akademik

- Seluruh kode dan narasi ditulis oleh kelompok sendiri.
- Bantuan AI digunakan untuk: drafting struktur notebook, debugging kompatibilitas NumPy (`np.trapz` vs `np.trapezoid`), dan formatting tabel.
- Tidak ada notebook dari kelompok lain yang disalin.
