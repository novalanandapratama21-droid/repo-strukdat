  # <h1 align="center">Laporan Praktikum Modul ABSTRACT DATA TYPE (ADT)</h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

ADT adalah TYPE dan sekumpulan PRIMITIF (operasi dasar) terhadap TYPE tersebut. Selain itu, dalam
sebuah ADT yang lengkap, disertakan pula definisi invarian dari TYPE dan aksioma yang berlaku. ADT
merupakan definisi STATIK.
## Guided 

### 1. [ABSTRACT DATA TYPE (ADT)]

```C++
#include <iostream>
using namespace std;

int main() {
    // --- Array 1 Dimensi ---
    int arr[5] = {10, 20, 30, 40, 50};
    cout << "Array 1 Dimensi:" << endl;
    for (int i = 0; i < 5; i++) {
        cout << "Element ke-" << i << ": " << arr[i] << endl;
    }
    cout << endl;

    // --- Array 2 Dimensi ---
    int arr2D[2][3] = {
        {1, 2, 3},
        {4, 5, 6},
    };
    cout << "Array 2 Dimensi:" << endl;
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 3; j++) {
            cout << "arr2D[" << i << "][" << j << "]: " << arr2D[i][j]
            << " ";
        }
        cout << endl;
    }
    // --- Array Multi Dimensi (3D) ---
    int arr3D[2][2][3] = {
        { {1, 2, 3}, {4, 5, 6} },
        { {7, 8, 9}, {10, 11, 12} },
    };
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            for (int k = 0; k < 3; k++) {
                cout << "arr3D[" << i << "][" << j << "]["
                << k << "]: " << arr3D[i][j][k] << endl;
            }
        }
    }

    return 0;
}
```
Kode di atas berfungsi untuk menampilkan contoh array satu dimensi, dua dimensi, dan tiga dimensi. Program menggunakan perulangan for untuk menampilkan setiap elemen dari masing-masing array, sehingga pengguna dapat melihat cara mengakses dan menampilkan data pada array dengan berbagai dimensi.

## Unguided 

### 1. [Soal]

```C++
#include <iostream>

using namespace std;

struct Mhs{
    char nama[30];
    char nim[10];
    float uts, uas, tugas, akhir;
};

float akhir(float uts, float uas, float tugas){
    return (0.3 * uts) + (0.4 * uas) + (0.3 * tugas);
}

int main(){
    Mhs mhs[10];
    int n;

    cout << "Masukkan jumlah mahasiswa: ";
    cin >> n;   

    for(int i = 0; i < n; i++){
        cout << "Masukkan data mahasiswa ke-" << (i + 1) << ":\n";
        cout << "Nama: ";
        cin >> mhs[i].nama;
        cout << "NIM: ";
        cin >> mhs[i].nim;
        cout << "Nilai UTS: ";
        cin >> mhs[i].uts;
        cout << "Nilai UAS: ";
        cin >> mhs[i].uas;
        cout << "Nilai Tugas: ";
        cin >> mhs[i].tugas;

        mhs[i].akhir = akhir(mhs[i].uts, mhs[i].uas, mhs[i].tugas);
    }

    cout << "\nData Mahasiswa:\n";
    for(int i = 0; i < n; i++){
         cout << "\nNama         : " << mhs[i].nama;
        cout << "\nNIM          : " << mhs[i].nim;
        cout << "\nNilai Akhir  : " << mhs[i].akhir << endl;
    }

    return 0;
}

```
#### Output:
<img width="611" height="740" alt="image" src="https://github.com/user-attachments/assets/0e7bcd60-27a2-4241-9db2-12362cd59864" />


Kode di atas berfungsi untuk menyimpan dan menampilkan data beberapa mahasiswa menggunakan struktur (struct). Program meminta pengguna untuk menginput nama, NIM, serta nilai UTS, UAS, dan tugas. Setelah itu, nilai akhir dihitung dengan rumus 0.3*UTS + 0.4*UAS + 0.3*Tugas melalui fungsi khusus. Hasilnya, program menampilkan kembali seluruh data mahasiswa beserta nilai akhirnya, sehingga pengguna dapat melihat daftar nilai yang telah dihitung secara otomatis.


#### Full code Screenshot:
<img width="768" height="1011" alt="image" src="https://github.com/user-attachments/assets/66349eb0-b652-4e2a-a98f-a064045169a8" />


### 2. [Soal]
Code pelajaran.h
```C++
#ifndef PELAJARAN_H_INCLUDED
#define PELAJARAN_H_INCLUDED
#include <string>
using namespace std;

struct pelajaran {
    string namaMapel;
    string kodeMapel;
};

pelajaran create_pelajaran(string namapel, string kodepel);
void tampil_pelajaran(pelajaran p);

#endif
```
Code pelajaran.cpp
```C++
#include <iostream>
#include "pelajaran.h"
using namespace std;

pelajaran create_pelajaran(string namapel, string kodepel) {
    pelajaran p;
    p.namaMapel = namapel;
    p.kodeMapel = kodepel;
    return p;
}

void tampil_pelajaran(pelajaran pel) {
    cout << "Nama Mata Pelajaran : " << pel.namaMapel << endl;
    cout << "Kode Mata Pelajaran : " << pel.kodeMapel << endl;
}
```
Code main.cpp
```C++
#include <iostream>
#include "pelajaran.h"
using namespace std;

int main() {
    string namapel = "Struktur Data";
    string kodepel = "STD";

    pelajaran pel = create_pelajaran(namapel, kodepel);
    tampil_pelajaran(pel);

    return 0;
}
```
#### Output:
<img width="1166" height="197" alt="image" src="https://github.com/user-attachments/assets/e98d2b65-a016-49ef-8d2a-ab0bccb4d9d0" />


Kode di atas menerapkan konsep Abstract Data Type (ADT) untuk mendefinisikan tipe data pelajaran yang memiliki atribut namaMapel dan kodeMapel. Implementasi dibagi menjadi tiga bagian yaitu file header (pelajaran.h), file implementasi (pelajaran.cpp), dan file utama (main.cpp). Program utama membuat sebuah objek pelajaran melalui fungsi create_pelajaran, kemudian menampilkan hasilnya menggunakan prosedur tampil_pelajaran. Dengan pemisahan ini, program menjadi lebih terstruktur dan mudah digunakan ulang sesuai prinsip modularitas pada ADT.

#### Full code Screenshot:
<img width="920" height="530" alt="image" src="https://github.com/user-attachments/assets/66b95cf5-9a73-490a-b1e5-adb93112dd7d" />
<img width="918" height="544" alt="image" src="https://github.com/user-attachments/assets/ec95b7e4-8457-41a2-b040-f39adc8d04ac" />
<img width="935" height="499" alt="image" src="https://github.com/user-attachments/assets/d654697a-5a5a-4bdb-bc5b-c2eef767971e" />



### 3. [Soal]
```C++
#include <iostream>
using namespace std;

int cariMin(int a[], int n);
int cariMaks(int a[], int n);
void hitungRata(int a[], int n);

int main() {
    int arr[10] = {11,8,5,7,12,26,3,54,33,55};
    int pilih, n = 10;

    do {
        cout << "\n--- Menu Program Array ---\n";
        cout << "1. Tampilkan isi array\n";
        cout << "2. Cari nilai maksimum\n";
        cout << "3. Cari nilai minimum\n";
        cout << "4. Hitung nilai rata-rata\n";
        cout << "5. Keluar\n";
        cout << "Pilih: ";
        cin >> pilih;

        switch(pilih) {
            case 1:
                for(int i=0;i<n;i++)
                    cout << arr[i] << " ";
                cout << endl;
                break;
            case 2:
                cout << "Nilai maksimum: " << cariMaks(arr,n) << endl;
                break;
            case 3:
                cout << "Nilai minimum: " << cariMin(arr,n) << endl;
                break;
            case 4:
                hitungRata(arr,n);
                break;
            case 5:
                cout << "Terima kasih!\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while(pilih != 5);

    return 0;
}

int cariMin(int a[], int n){
    int min = a[0];
    for(int i=1;i<n;i++)
        if(a[i]<min) min = a[i];
    return min;
}

int cariMaks(int a[], int n){
    int maks = a[0];
    for(int i=1;i<n;i++)
        if(a[i]>maks) maks = a[i];
    return maks;
}

void hitungRata(int a[], int n){
    int total=0;
    for(int i=0;i<n;i++) total += a[i];
    cout << "Nilai rata-rata: " << (float)total/n << endl;
}
```
#### Output:
<img width="599" height="927" alt="Image" src="https://github.com/user-attachments/assets/3a1be501-56d9-45de-ac15-4a9260002600" />

Kode di atas berfungsi untuk melakukan berbagai operasi pada data array berisi sepuluh angka. Program menampilkan menu interaktif yang memungkinkan pengguna memilih beberapa opsi, yaitu menampilkan isi array, mencari nilai maksimum, mencari nilai minimum, dan menghitung nilai rata-rata. Fungsi `cariMaks()` digunakan untuk menentukan nilai terbesar dari elemen array, sedangkan `cariMin()` untuk mencari nilai terkecil. Sementara itu, fungsi `hitungRata()` menjumlahkan semua elemen array dan membaginya dengan jumlah data untuk mendapatkan rata-ratanya. Program akan terus berjalan menampilkan menu sampai pengguna memilih opsi keluar.


#### Full code Screenshot:
<img width="476" height="940" alt="Image" src="https://github.com/user-attachments/assets/78039e91-904a-4c18-8aad-069adf6f16ad" />


### 🧾 **Kesimpulan**

Ketiga program yang telah dibuat memiliki tujuan yang berbeda namun sama-sama melatih pemahaman konsep dasar pemrograman C++ terutama pada penerapan struktur data dan tipe data abstrak.
Program pertama digunakan untuk menyimpan dan menampilkan data mahasiswa menggunakan `struct`, serta menghitung nilai akhir melalui fungsi sederhana.
Program kedua menerapkan konsep *Abstract Data Type (ADT)* dengan memisahkan file header (`.h`), implementasi (`.cpp`), dan program utama (`main.cpp`) untuk tipe data `pelajaran`, sehingga melatih pemahaman modularitas program.
Sedangkan program ketiga menampilkan cara manipulasi data menggunakan array dua dimensi dan pointer, termasuk menukar nilai elemen dan variabel yang ditunjuk oleh pointer.
Secara keseluruhan, ketiga program ini membantu memahami penggunaan `struct`, fungsi, ADT, array 2D, dan pointer dalam penyusunan program C++ yang lebih terstruktur dan efisien.


## Referensi
[1] GeeksforGeeks. (2024, April 15). Structures in C++. Diakses dari https://www.geeksforgeeks.org/structures-in-cpp/
[2] EECS 280 Staff. (n.d.). Abstract Data Types in C++. University of Michigan. Diakses dari https://eecs280staff.github.io/notes/08_ADTs_in_C%2B%2B.html
[3] Studytonight. (2022, Maret 30). C++ Program For Swapping Two Number In Function Using Pointer. Diakses dari https://www.studytonight.com/cpp-programs/cpp-program-for-swapping-two-number-in-function-using-pointer








