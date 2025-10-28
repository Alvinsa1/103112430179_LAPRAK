# <h1 align="center">Laporan Praktikum Modul 2 <br> ARRAY </h1>
<p align="center">Alvinsa Hafizh Arkaan - 103112430179</p>

## Dasar Teori

Array dalam C++ merupakan struktur data yang menyimpan sekelompok elemen data dengan tipe yang seragam dalam tempat penyimpanan memori yang berdekatan, diakses melalui indeks yang dimulai dari nol. Array memiliki ukuran tetap yang ditentukan saat pembentukan, dan menawarkan cara efisien untuk menyimpan dan mengelola banyak data serupa, seperti angka atau string, dalam satu variabel


## Guided

### guided 1
   ```c++
#include <iostream>
using namespace std;

void kuadratkan(int &angka)
{
    angka = angka * angka;
}

int main()
{
    int nilai;

    cout << "Masukkan nilai awal yang ingin dikuadratkan: ";
    cin >> nilai;

    cout << "Nilai awal: " << nilai << endl;

    kuadratkan(nilai);

    cout << "Nilai setelah dikuadratkan: " << nilai << endl;

    return 0;
}

```

Program diatas ini bertujuan untuk menghitung kuadrat dari sebuah bilangan bulat yang dimasukkan pengguna, dan secara khusus mendemonstrasikan mekanisme Call by Reference (melewatkan berdasarkan referensi) pada fungsi. Program dimulai dengan mendeklarasikan variabel nilai untuk menyimpan input pengguna, Pengguna diminta untuk memasukkan angka, yang kemudian disimpan di nilai, nilai awal ditampilkan, lalu memanggil fungsi variabel nilai diteruskan ke fungsi kuadratkan. Karena fungsi menggunakan reference, nilai dari nilai di memori utama kini secara permanen diubah menjadi kuadratnya, terakhir program kemudian menampilkan nilai akhir dari nilai. Nilai yang ditampilkan adalah hasil kuadrat, yang membuktikan bahwa fungsi kuadratkan berhasil memodifikasi variabel nilai di luar lingkup fungsi itu sendiri.

> Output
> ![Screenshot bagian x](outputmodul2/Screenshot_guided1.png)



### guided 2


```c++
#include <iostream>
using namespace std;

void tukar(int *px, int *py);

int main()
{   
    int a = 10, b = 20;
    
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl; 
    
    tukar(&a, &b); 
    
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    
    return 0;
}

void tukar(int *px, int *py)
{
    int temp = *px; 
    
    *px = *py; 
    
    *py = temp; 
}
```
Program diataas ini bertujuan untuk menukar nilai dari dua variabel (a dan b) menggunakan mekanisme Call by Pointer (melewatkan berdasarkan pointer) atau juga dikenal sebagai Call by Address. Header fungsi menerima dua parameter, px dan py, yang merupakan pointer ke integer (ditandai dengan operator *). Artinya, px menyimpan alamat memori dari a, dan py menyimpan alamat memori dari b.

> Output
> ![Screenshot bagian x](outputmodul2/Screenshot_guided2.png)


## Unguided

### Soal 1

```c++
#include <iostream>
#include <iomanip>

using namespace std;

const int N = 3;

void input_matriks(int matriks[N][N]) {
    cout << "Masukkan elemen Matriks " << N << "x" << N << " (baris per baris):" << endl;
    
    for (int i = 0; i < N; ++i) {
        cout << "Baris " << i + 1 << ": ";
        for (int j = 0; j < N; ++j) {
            cin >> matriks[i][j];
        }
    }
}

void transpose_matriks(const int matriks_awal[N][N], int matriks_transpose[N][N]) {
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < N; ++j) {
            matriks_transpose[i][j] = matriks_awal[j][i];
        }
    }
}

void cetak_matriks(const int matriks[N][N], const char* judul) {
    cout << "\n" << judul << ":" << endl;
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < N; ++j) {
            cout << setw(3) << matriks[i][j];
        }
        cout << endl;
    }
}

int main()
{
    int matriks_awal[N][N];
    int matriks_transpose[N][N];
    
    input_matriks(matriks_awal);
    
    transpose_matriks(matriks_awal, matriks_transpose);
    
    cetak_matriks(matriks_awal, "Matriks Awal");
    cetak_matriks(matriks_transpose, "Matriks Hasil Transpose");

    return 0;
}
```
>

Program diatas ini adalah alat untuk melakukan operasi transpose pada matriks persegi 3×3 yang nilainya dimasukkan oleh pengguna. Program ini diorganisir dengan baik menggunakan beberapa fungsi terpisah (modular) untuk menangani setiap tugas: input, transpose, dan pencetakan. Fungsi input_matriks bertanggung jawab untuk mengambil input elemen matriks dari pengguna, menggunakan dua nested loop untuk mengiterasi baris (i) dan kolom (j), meminta pengguna memasukkan N×N elemen secara berurutan, matriks dilewatkan ke fungsi melalui Call by Reference implisit (untuk array dalam C++), sehingga nilai yang dimasukkan langsung tersimpan di matriks_awal pada fungsi main.
> Output
> ![Screenshot bagian x](outputmodul2/Screenshot_unguided1.png)



### Soal 2

soal nomor 2

```c++
#include <iostream>

using namespace std;

void kuadratkan(int &angka)
{
    angka = angka * angka;
}

int main()
{
    int nilai;

    cout << "Masukkan nilai awal yang ingin dikuadratkan: ";
    cin >> nilai;

    cout << "Nilai awal: " << nilai << endl;

    kuadratkan(nilai);

    cout << "Nilai setelah dikuadratkan: " << nilai << endl;

    return 0;
}
```

Program diatas ini adalah demonstrasi sederhana mengenai fungsi dan mekanisme Call by Reference (melewatkan berdasarkan referensi) untuk menghitung dan memperbarui nilai kuadrat dari sebuah bilangan bulat yang dimasukkan oleh pengguna. Fungsi kuadratkan bertujuan menghitung kuadrat dari angka yang diterima, mekanisme Kunci Parameter int &angka menggunakan simbol ampersand (&), yang mengubahnya menjadi referensi. Ini berarti variabel angka di dalam fungsi adalah alias atau nama lain untuk variabel asli yang diteruskan dari main, Aksi Baris angka = angka * angka; secara permanen memodifikasi nilai yang tersimpan di lokasi memori variabel asli (yaitu nilai di main).

> Output
> ![Screenshot bagian x](outputmodul2/Screenshot_unguided1.png)

