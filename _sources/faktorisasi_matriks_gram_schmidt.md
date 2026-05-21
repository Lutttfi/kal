# Faktorisasi Matriks: Proses Gram-Schmidt (Matriks 4x4)

Proses **Gram-Schmidt** bertujuan untuk mengambil sekumpulan vektor yang saling bebas linier (kolom-kolom dari matriks $A$) dan mengubahnya menjadi sekumpulan vektor **ortonormal** (kolom-kolom dari matriks $Q$).

Berikut adalah langkah-langkah detail pengerjaan faktorisasi QR untuk matriks $4 \times 4$.

---

## 1. Matriks Awal

Misalkan kita punya matriks $A$ ukuran $4 \times 4$ berikut (dipilih dengan angka yang menghasilkan perhitungan bulat tanpa akar yang rumit):

$$A = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & 1 & 0 & 0 \\ 1 & 0 & 1 & 0 \\ 1 & 0 & 0 & 1 \end{bmatrix}$$

Kolom-kolom dari matriks $A$ kita definisikan sebagai vektor $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3,$ dan \mathbf{a}_4$:

$$\mathbf{a}_1 = \begin{bmatrix} 1 \\ 1 \\ 1 \\ 1 \end{bmatrix}, \quad \mathbf{a}_2 = \begin{bmatrix} 1 \\ 1 \\ 0 \\ 0 \end{bmatrix}, \quad \mathbf{a}_3 = \begin{bmatrix} 1 \\ 0 \\ 1 \\ 0 \end{bmatrix}, \quad \mathbf{a}_4 = \begin{bmatrix} 1 \\ 0 \\ 0 \\ 1 \end{bmatrix}$$

---

## 2. Langkah-Langkah Matematis

### Langkah 1: Vektor Pertama ($\mathbf{q}_1$)
Ambil kolom pertama $\mathbf{a}_1$, lalu normalisasi agar panjangnya (norm) menjadi 1.

1. **Hitung panjang (norm) $\mathbf{a}_1$:**
   $$\|\mathbf{a}_1\| = \sqrt{1^2 + 1^2 + 1^2 + 1^2} = \sqrt{4} = 2$$

2. **Normalisasi menjadi vektor satuan $\mathbf{q}_1$:**
   $$\mathbf{q}_1 = \frac{\mathbf{a}_1}{\|\mathbf{a}_1\|} = \frac{1}{2} \begin{bmatrix} 1 \\ 1 \\ 1 \\ 1 \end{bmatrix} = \begin{bmatrix} 1/2 \\ 1/2 \\ 1/2 \\ 1/2 \end{bmatrix}$$

---

### Langkah 2: Vektor Kedua ($\mathbf{q}_2$)
Ambil kolom kedua $\mathbf{a}_2$, lalu buang komponen proyeksi $\mathbf{a}_2$ yang searah dengan $\mathbf{q}_1$. Sisa pengurangannya (residu) disebut $\mathbf{v}_2$.

1. **Cari komponen tegak lurus (residu $\mathbf{v}_2$):**
   $$\mathbf{v}_2 = \mathbf{a}_2 - (\mathbf{a}_2 \cdot \mathbf{q}_1)\mathbf{q}_1$$
   
   *Hitung dot product terlebih dahulu:*
   $$\mathbf{a}_2 \cdot \mathbf{q}_1 = (1)(1/2) + (1)(1/2) + (0)(1/2) + (0)(1/2) = 1$$
   
   *Substitusikan ke rumus:*
   $$\mathbf{v}_2 = \begin{bmatrix} 1 \\ 1 \\ 0 \\ 0 \end{bmatrix} - 1 \begin{bmatrix} 1/2 \\ 1/2 \\ 1/2 \\ 1/2 \end{bmatrix} = \begin{bmatrix} 1/2 \\ 1/2 \\ -1/2 \\ -1/2 \end{bmatrix}$$

2. **Normalisasi $\mathbf{v}_2$ untuk mendapatkan $\mathbf{q}_2$:**
   $$\|\mathbf{v}_2\| = \sqrt{(1/2)^2 + (1/2)^2 + (-1/2)^2 + (-1/2)^2} = \sqrt{\frac{1}{4} + \frac{1}{4} + \frac{1}{4} + \frac{1}{4}} = \sqrt{1} = 1$$
   $$\mathbf{q}_2 = \frac{\mathbf{v}_2}{\|\mathbf{v}_2\|} = \begin{bmatrix} 1/2 \\ 1/2 \\ -1/2 \\ -1/2 \end{bmatrix}$$

---

### Langkah 3: Vektor Ketiga ($\mathbf{q}_3$)
Ambil kolom ketiga $\mathbf{a}_3$, kurangi dengan proyeksinya terhadap semua vektor $\mathbf{q}$ yang sudah ditemukan sebelumnya ($\mathbf{q}_1$ dan $\mathbf{q}_2$).

1. **Cari komponen tegak lurus (residu $\mathbf{v}_3$):**
   $$\mathbf{v}_3 = \mathbf{a}_3 - (\mathbf{a}_3 \cdot \mathbf{q}_1)\mathbf{q}_1 - (\mathbf{a}_3 \cdot \mathbf{q}_2)\mathbf{q}_2$$
   
   *Hitung dot product:*
   $$\mathbf{a}_3 \cdot \mathbf{q}_1 = (1)(1/2) + (0)(1/2) + (1)(1/2) + (0)(1/2) = 1$$
   $$\mathbf{a}_3 \cdot \mathbf{q}_2 = (1)(1/2) + (0)(1/2) + (1)(-1/2) + (0)(-1/2) = 0$$
   
   *Substitusikan ke rumus:*
   $$\mathbf{v}_3 = \begin{bmatrix} 1 \\ 0 \\ 1 \\ 0 \end{bmatrix} - 1 \begin{bmatrix} 1/2 \\ 1/2 \\ 1/2 \\ 1/2 \end{bmatrix} - 0 \begin{bmatrix} 1/2 \\ 1/2 \\ -1/2 \\ -1/2 \end{bmatrix} = \begin{bmatrix} 1/2 \\ -1/2 \\ 1/2 \\ -1/2 \end{bmatrix}$$

2. **Normalisasi $\mathbf{v}_3$ untuk mendapatkan $\mathbf{q}_3$:**
   $$\|\mathbf{v}_3\| = \sqrt{(1/2)^2 + (-1/2)^2 + (1/2)^2 + (-1/2)^2} = \sqrt{1} = 1$$
   $$\mathbf{q}_3 = \frac{\mathbf{v}_3}{\|\mathbf{v}_3\|} = \begin{bmatrix} 1/2 \\ -1/2 \\ 1/2 \\ -1/2 \end{bmatrix}$$

---

### Langkah 4: Vektor Keempat ($\mathbf{q}_4$)
Ambil kolom keempat $\mathbf{a}_4$, lalu kurangi dengan proyeksinya terhadap $\mathbf{q}_1, \mathbf{q}_2,$ dan $\mathbf{q}_3$.

1. **Cari komponen tegak lurus (residu $\mathbf{v}_4$):**
   $$\mathbf{v}_4 = \mathbf{a}_4 - (\mathbf{a}_4 \cdot \mathbf{q}_1)\mathbf{q}_1 - (\mathbf{a}_4 \cdot \mathbf{q}_2)\mathbf{q}_2 - (\mathbf{a}_4 \cdot \mathbf{q}_3)\mathbf{q}_3$$
   
   *Hitung dot product:*
   $$\mathbf{a}_4 \cdot \mathbf{q}_1 = (1)(1/2) + (0)(1/2) + (0)(1/2) + (1)(1/2) = 1$$
   $$\mathbf{a}_4 \cdot \mathbf{q}_2 = (1)(1/2) + (0)(1/2) + (0)(-1/2) + (1)(-1/2) = 0$$
   $$\mathbf{a}_4 \cdot \mathbf{q}_3 = (1)(1/2) + (0)(-1/2) + (0)(1/2) + (1)(-1/2) = 0$$
   
   *Substitusikan ke rumus:*
   $$\mathbf{v}_4 = \begin{bmatrix} 1 \\ 0 \\ 0 \\ 1 \end{bmatrix} - 1 \begin{bmatrix} 1/2 \\ 1/2 \\ 1/2 \\ 1/2 \end{bmatrix} - 0 - 0 = \begin{bmatrix} 1/2 \\ -1/2 \\ -1/2 \\ 1/2 \end{bmatrix}$$

2. **Normalisasi $\mathbf{v}_4$ untuk mendapatkan $\mathbf{q}_4$:**
   $$\|\mathbf{v}_4\| = \sqrt{(1/2)^2 + (-1/2)^2 + (-1/2)^2 + (1/2)^2} = \sqrt{1} = 1$$
   $$\mathbf{q}_4 = \frac{\mathbf{v}_4}{\|\mathbf{v}_4\|} = \begin{bmatrix} 1/2 \\ -1/2 \\ -1/2 \\ 1/2 \end{bmatrix}$$

---

## 3. Hasil Akhir: Matriks Q dan R

Setelah semua komponen didapatkan, kita bisa menyusun matriks $Q$ (ortogonal) dan matriks $R$ (segitiga atas).

### Matriks $Q$
Berisi kumpulan vektor satuan $\mathbf{q}_1, \mathbf{q}_2, \mathbf{q}_3, \mathbf{q}_4$ sebagai kolom-kolomnya:

$$Q = \begin{bmatrix} 1/2 & 1/2 & 1/2 & 1/2 \\ 1/2 & 1/2 & -1/2 & -1/2 \\ 1/2 & -1/2 & 1/2 & -1/2 \\ 1/2 & -1/2 & -1/2 & 1/2 \end{bmatrix}$$

### Matriks $R$
Berisi nilai-nilai hasil proyeksi dan norm yang membentuk matriks segitiga atas:

$$R = \begin{bmatrix} 
\mathbf{a}_1 \cdot \mathbf{q}_1 & \mathbf{a}_2 \cdot \mathbf{q}_1 & \mathbf{a}_3 \cdot \mathbf{q}_1 & \mathbf{a}_4 \cdot \mathbf{q}_1 \\ 
0 & \mathbf{a}_2 \cdot \mathbf{q}_2 & \mathbf{a}_3 \cdot \mathbf{q}_2 & \mathbf{a}_4 \cdot \mathbf{q}_2 \\ 
0 & 0 & \mathbf{a}_3 \cdot \mathbf{q}_3 & \mathbf{a}_4 \cdot \mathbf{q}_3 \\ 
0 & 0 & 0 & \mathbf{a}_4 \cdot \mathbf{q}_4 
\end{bmatrix}$$

Jika kita masukkan nilai dot product dan norm yang sudah dihitung di atas, diperoleh:

$$R = \begin{bmatrix} 2 & 1 & 1 & 1 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

Dengan demikian, faktorisasi $A = QR$ terpenuhi dengan tepat dan siap ditampilkan menggunakan engine visualisasi matematika static web seperti MathJax atau KaTeX di Jupyter Book.