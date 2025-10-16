# <h1 align="center">Laporan Praktikum Modul ABSTRACT DATA TYPE (ADT)</h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

Abstract Data Type (ADT) merupakan konsep dasar dalam pemrograman yang mendefinisikan suatu tipe data beserta operasi-operasi yang dapat dilakukan terhadapnya tanpa memperhatikan bagaimana data tersebut diimplementasikan. Dalam bahasa C++, ADT biasanya diwujudkan melalui penggunaan `struct` dan fungsi-fungsi pendukung yang dipisahkan ke dalam beberapa file, yaitu file header (`.h`) untuk mendefinisikan tipe dan deklarasi fungsi, file implementasi (`.cpp`) untuk merealisasikan fungsi, serta file utama (`main.cpp`) sebagai penguji ADT. Pemisahan ini bertujuan agar program lebih terstruktur, mudah dibaca, dan dapat digunakan ulang. Dengan memahami ADT, programmer dapat membangun program yang modular, efisien, dan sesuai dengan prinsip abstraksi data.

## Guided 

### 1. [ABSTRACT DATA TYPE (ADT)]
Code mahasiswa.h
```C++
#ifndef MAHASISWA_H_INCLUDED 
#define MAHASISWA_H_INCLUDED 

struct mahasiswa { 
    char nim[10]; 
    int nilai1, nilai2; 
};

void inputMhs(mahasiswa &m); 
float rata2(mahasiswa m); 

#endif
```
Code mahasiswa.cpp
```C++
#include <iostream>
#include "mahasiswa.h"
void inputMhs(mahasiswa &m){ 
    cout << "input nama = "; 
    cin >> (m).nim; 
    cout << "input nilai = "; 
    cin >> (m).nilai1; 
    cout << "input nilai2 = "; 
    cin >> (m).nilai2;
} 
 
float rata2(mahasiswa m){ 
  return float(m.nilai1+m.nilai2)/2; 
}
```
Code main.cpp
```C++
#include <iostream>
using namespace std;

struct mahasiswa{ 
    char nim[10]; 
    int nilai1,nilai2;
};

void inputMhs(mahasiswa &m); 
float rata2(mahasiswa m);

int main() { 
mahasiswa mhs; 
inputMhs(mhs); 
    cout << "rata-rata = " << rata2(mhs); 
return 0; 
}

void inputMhs(mahasiswa &m){ 
    cout << "input nama = "; 
    cin >> m.nim; 
    cout << "input nilai = "; 
    cin >> m.nilai1; 
    cout << "input nilai2 = ";
    cin >> m.nilai2; 
} 
float rata2(mahasiswa m){ 
return float(m.nilai1+m.nilai2)/2; 
}
```
Program ini dibuat untuk menerapkan konsep Abstract Data Type (ADT) sederhana menggunakan tiga file terpisah (main.cpp, mahasiswa.h, dan mahasiswa.cpp).
Program berfungsi untuk memasukkan data mahasiswa berupa NIM dan dua nilai, kemudian menghitung rata-rata dari kedua nilai tersebut menggunakan fungsi rata2().

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

void tampilArray(int A[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << A[i][j] << " ";
        }
        cout << endl;
    }
}

void tukarArray(int A[3][3], int B[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            int temp = A[i][j];
            A[i][j] = B[i][j];
            B[i][j] = temp;
        }
    }
}

void tukarPointer(int *x, int *y) {
    int temp = *x;
    *x = *y;
    *y = temp;
}

int main() {
    int A[3][3] = {{1,2,3},{4,5,6},{7,8,9}};
    int B[3][3] = {{9,8,7},{6,0,4},{3,2,1}};
    int a = 10, b = 20;
    int *pa = &a, *pb = &b;

    cout << "=== ARRAY SEBELUM DITUKAR ===" << endl;
    cout << "Array A:\n"; tampilArray(A);
    cout << "Array B:\n"; tampilArray(B);

    tukarArray(A, B);

    cout << "\n=== ARRAY SETELAH DITUKAR ===" << endl;
    cout << "Array A:\n"; tampilArray(A);
    cout << "Array B:\n"; tampilArray(B);

    cout << "\n=== NILAI POINTER ===" << endl;
    cout << "Sebelum tukar: a = " << a << ", b = " << b << endl;
    tukarPointer(pa, pb);
    cout << "Sesudah tukar: a = " << a << ", b = " << b << endl;

    return 0;
}

```
#### Output:
<img width="662" height="805" alt="image" src="https://github.com/user-attachments/assets/52423fb3-15e9-4268-a95e-a97728d01f24" />

Kode di atas berfungsi untuk menampilkan dan menukar isi dua buah array dua dimensi berukuran 3×3 serta menukar nilai dua variabel menggunakan pointer. Program dimulai dengan menampilkan isi awal dari array `A` dan `B`, kemudian seluruh elemen dari kedua array ditukar menggunakan prosedur `tukarArray()`. Setelah pertukaran, hasil isi array ditampilkan kembali untuk menunjukkan perubahannya. Selain itu, program juga menukar nilai dua variabel `a` dan `b` dengan prosedur `tukarPointer()` yang menggunakan konsep pointer untuk mengakses dan menukar nilai di memori. Secara keseluruhan, program ini memperlihatkan penerapan konsep fungsi, array dua dimensi, dan pointer dalam melakukan manipulasi data di C++.

#### Full code Screenshot:
<img width="595" height="923" alt="image" src="https://github.com/user-attachments/assets/70234abd-be2d-47f4-81a7-69d74fdf98bd" />



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








