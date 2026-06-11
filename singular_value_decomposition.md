# Singular Value Decomposition (SVD)

Singular Value Decomposition (SVD) adalah teknik faktorisasi matriks yang menguraikan sebuah matriks menjadi tiga matriks komponen utama. Teknik ini sangat krusial dalam mengungkapkan aspek struktural penting dari sebuah matriks dan banyak diaplikasikan dalam pemrosesan sinyal, kompresi gambar, sistem rekomendasi, serta reduksi dimensi pada *machine learning*.

> **Prasyarat:** Sebelum mempelajari SVD, Anda diharapkan telah memahami konsep dasar aljabar linear seperti norma vektor/matriks, rank matriks, dekomposisi eigen (vektor eigen dan nilai eigen), vektor ortonormal, serta proyeksi linear.

---

## Definisi Matematis

Dekomposisi nilai singular dari sebuah matriks riil $A$ berukuran $m \times n$ adalah faktorisasi dalam bentuk:

$$
A = U\Sigma V^T
$$

Dimana setiap matriks memiliki karakteristik berikut:

* **$U$ (Matriks Ortogonal $m \times m$):** Kolom-kolomnya merupakan vektor-vektor ortonormal yang disebut sebagai **vektor singular kiri** dari $A$. Vektor-vektor ini merupakan vektor eigen dari matriks simetris $AA^T$.
* **$\Sigma$ (Matriks Diagonal Persegi Panjang $m \times n$):** Berisi bilangan riil non-negatif pada diagonal utamanya yang disusun secara berurutan menurun:
    $$
    \sigma_1 \ge \sigma_2 \ge \cdots \ge \sigma_r > 0
    $$
    Entri diagonal ini disebut **nilai singular** dari $A$. Banyaknya nilai singular yang tidak nol menunjukkan nilai *rank* dari matriks $A$.
* **$V$ (Matriks Ortogonal $n \times n$):** Kolom-kolomnya merupakan vektor-vektor ortonormal yang disebut **vektor singular kanan** dari $A$, yang diperoleh dari vektor eigen matriks simetris $A^TA$. Matriks $V^T$ adalah bentuk *transpose* dari $V$.

---

## Algoritma Perhitungan SVD

Prosedur lengkap untuk mendekomposisi matriks $A$ secara manual adalah sebagai berikut:

### Langkah 1: Menghitung Vektor Singular Kiri
1. Hitung matriks simetris $AA^T$ (berukuran $m \times m$).
2. Cari nilai-nilai eigen ($\lambda$) dari matriks $AA^T$ dengan menyelesaikan persamaan karakteristik $\det(AA^T - \lambda I) = 0$.
3. Banyaknya nilai eigen yang tidak nol menentukan nilai $\operatorname{Rank}(A) = k$.

### Langkah 2: Membentuk Matriks $U$
1. Tentukan vektor eigen $\mathbf{u}_1, \mathbf{u}_2, \ldots, \mathbf{u}_m$ yang berkorespondensi dengan masing-masing nilai eigen dari $AA^T$.
2. Normalisasi setiap vektor eigen tersebut agar panjangnya bernilai $1$ (ortonormal):
    $$
    \mathbf{u}_i = \frac{\mathbf{u}_i}{\|\mathbf{u}_i\|}
    $$
3. Susun vektor-vektor ortonormal ini sebagai kolom-kolom untuk membentuk matriks $U$.

### Langkah 3: Menghitung Nilai Singular & Matriks $\Sigma$
1. Urutkan nilai eigen dari yang terbesar ke terkecil.
2. Nilai singular ($\sigma_i$) diperoleh dari akar kuadrat nilai eigen utama tersebut:
    $$
    \sigma_i = \sqrt{\lambda_i}
    $$
3. Bentuk matriks $\Sigma$ berukuran $m \times n$ dengan menempatkan nilai singular pada diagonal utama dan mengisi entri lainnya dengan angka $0$.

### Langkah 4: Membentuk Matriks $V$ dan $V^T$
1. Hitung matriks simetris $A^TA$ (berukuran $n \times n$).
2. Tentukan vektor eigen $\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_n$ dari $A^TA$.
3. Normalisasi setiap vektor eigen tersebut:
    $$
    \mathbf{v}_i = \frac{\mathbf{v}_i}{\|\mathbf{v}_i\|}
    $$
4. Susun vektor-vektor ini sebagai kolom-kolom matriks $V$, kemudian lakukan *transpose* untuk memperoleh matriks $V^T$.

---

## Contoh Perhitungan Manual

Diberikan matriks $A$ berukuran $2 \times 3$:

$$
A = \begin{bmatrix} 3 & 1 & 1 \\ -1 & 3 & 1 \end{bmatrix}
$$

### 1. Menghitung $AA^T$
$$
AA^T = \begin{bmatrix} 3 & 1 & 1 \\ -1 & 3 & 1 \end{bmatrix} \begin{bmatrix} 3 & -1 \\ 1 & 3 \\ 1 & 1 \end{bmatrix} = \begin{bmatrix} 11 & 1 \\ 1 & 11 \end{bmatrix}
$$

### 2. Mencari Nilai Eigen dari $AA^T$
Persamaan karakteristik:
$$
\det(AA^T - \lambda I) = 0
$$
$$
\det \begin{bmatrix} 11-\lambda & 1 \\ 1 & 11-\lambda \end{bmatrix} = 0
$$
$$
(11-\lambda)^2 - 1 = 0 \implies \lambda^2 - 22\lambda + 120 = 0
$$
$$
(\lambda - 12)(\lambda - 10) = 0
$$
Didapatkan nilai eigen: $\lambda_1 = 12$ dan $\lambda_2 = 10$. Karena kedua nilai eigen tidak nol, maka $\operatorname{Rank}(A) = 2$.

### 3. Menentukan Matriks $U$
Selesaikan sistem persamaan $(\lambda I - AA^T)\mathbf{x} = 0$:

* **Untuk $\lambda_1 = 12$:**
    $$
    \begin{bmatrix} 1 & -1 \\ -1 & 1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies x_1 = x_2 \implies \mathbf{u}_1 = \begin{bmatrix} 1 \\ 1 \end{bmatrix}
    $$
    Normalisasi ($\|\mathbf{u}_1\| = \sqrt{2}$):
    $$
    \hat{\mathbf{u}}_1 = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}
    $$

* **Untuk $\lambda_2 = 10$:**
    $$
    \begin{bmatrix} -1 & -1 \\ -1 & -1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies x_1 = -x_2 \implies \mathbf{u}_2 = \begin{bmatrix} 1 \\ -1 \end{bmatrix}
    $$
    Normalisasi ($\|\mathbf{u}_2\| = \sqrt{2}$):
    $$
    \hat{\mathbf{u}}_2 = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} \end{bmatrix}
    $$

Maka, diperoleh matriks $U$:
$$
U = \begin{bmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \end{bmatrix}
$$

### 4. Menentukan Matriks $\Sigma$
Nilai singular didapatkan dari akar nilai eigen:
$$
\sigma_1 = \sqrt{12} = 2\sqrt{3}, \quad \sigma_2 = \sqrt{10}
$$
Matriks $\Sigma$ berukuran $2 \times 3$ dibentuk sebagai berikut:
$$
\Sigma = \begin{bmatrix} 2\sqrt{3} & 0 & 0 \\ 0 & \sqrt{10} & 0 \end{bmatrix}
$$

### 5. Menentukan Matriks $V$
Hitung terlebih dahulu matriks $A^TA$:
$$
A^TA = \begin{bmatrix} 3 & -1 \\ 1 & 3 \\ 1 & 1 \end{bmatrix} \begin{bmatrix} 3 & 1 & 1 \\ -1 & 3 & 1 \end{bmatrix} = \begin{bmatrix} 10 & 0 & 2 \\ 0 & 10 & 4 \\ 2 & 4 & 2 \end{bmatrix}
$$

Cari vektor eigen melalui persamaan $(A^TA - \lambda I)\mathbf{v} = 0$:
* **Untuk $\lambda_1 = 12$:** diperoleh $\mathbf{v}_1 = [1, 2, 1]^T$, ternormalisasi menjadi:
    $$
    \hat{\mathbf{v}}_1 = \frac{1}{\sqrt{6}}\begin{bmatrix} 1 \\ 2 \\ 1 \end{bmatrix}
    $$
* **Untuk $\lambda_2 = 10$:** diperoleh $\mathbf{v}_2 = [2, -1, 0]^T$, ternormalisasi menjadi:
    $$
    \hat{\mathbf{v}}_2 = \frac{1}{\sqrt{5}}\begin{bmatrix} 2 \\ -1 \\ 0 \end{bmatrix}
    $$
* **Untuk $\lambda_3 = 0$:** diperoleh $\mathbf{v}_3 = [1, 2, -5]^T$, ternormalisasi menjadi:
    $$
    \hat{\mathbf{v}}_3 = \frac{1}{\sqrt{30}}\begin{bmatrix} 1 \\ 2 \\ -5 \end{bmatrix}
    $$

Menyusun matriks $V$ dan $V^T$:
$$
V = \begin{bmatrix} \frac{1}{\sqrt{6}} & \frac{2}{\sqrt{5}} & \frac{1}{\sqrt{30}} \\ \frac{2}{\sqrt{6}} & -\frac{1}{\sqrt{5}} & \frac{2}{\sqrt{30}} \\ \frac{1}{\sqrt{6}} & 0 & -\frac{5}{\sqrt{30}} \end{bmatrix} \implies V^T = \begin{bmatrix} \frac{1}{\sqrt{6}} & \frac{2}{\sqrt{6}} & \frac{1}{\sqrt{6}} \\ \frac{2}{\sqrt{5}} & -\frac{1}{\sqrt{5}} & 0 \\ \frac{1}{\sqrt{30}} & \frac{2}{\sqrt{30}} & -\frac{5}{\sqrt{30}} \end{bmatrix}
$$

---

## Integrasi Kode Interaktif (SageMath / Python)

Gunakan blok kode interaktif di bawah ini pada halaman web Anda untuk mendemonstrasikan penghitungan otomatis menggunakan pustaka NumPy:

```html
<script src="https://sagecell.sagemath.org/static/embedded_sagecell.js"></script>
<script>
sagecell.makeSagecell({
    inputLocation: '.sage'
});
</script>

<div class="sage">
<script type="text/x-sage">
import numpy as np

# Inisialisasi Matriks A awal
A = np.array([[3, 1, 1], [-1, 3, 1]])

# Proses Komputasi SVD
U, S_vektor, VT = np.linalg.svd(A)

# Membuat matriks diagonal Sigma berukuran 2x3
Sigma = np.zeros((2, 3))
Sigma[:2, :2] = np.diag(S_vektor)

# Rekonstruksi kembali matriks A
A_reconstructed = U @ Sigma @ VT

print("Matriks Ortogonal U (Vektor Singular Kiri):")
print(np.round(U, 4))
print("\nMatriks Diagonal Sigma (Nilai Singular):")
print(np.round(Sigma, 4))
print("\nMatriks V Transpose (V Vektor Singular Kanan):")
print(np.round(VT, 4))
print("\nHasil Rekonstruksi U @ Sigma @ VT:")
print(np.round(A_reconstructed, 4))
</script>
</div>