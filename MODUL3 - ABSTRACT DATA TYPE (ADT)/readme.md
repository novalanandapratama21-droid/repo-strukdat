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
```C++
#include <iostream>
using namespace std;

int main(){
    int a, b, c, t;
    cout << "Masukkan tiga bilangan: ";
    cin >> a >> b >> c;
    cout<<"Sebelum: "<<a<<" "<<b<<" "<<c<<endl;
    t=a; a=b; b=c; c=t;
    cout<<"Sesudah: "<<a<<" "<<b<<" "<<c<<endl;
}
```
#### Output:
<img width="644" height="181" alt="Image" src="https://github.com/user-attachments/assets/c17cb710-1783-4a6e-8998-cc5c2e5c5634" />

Kode di atas berfungsi untuk menukar posisi tiga bilangan yang dimasukkan oleh pengguna. Program meminta input tiga angka melalui `cin`, lalu menampilkan nilai sebelum dan sesudah pertukaran menggunakan `cout`. Proses penukaran dilakukan dengan memanfaatkan variabel sementara `t`, sehingga nilai `a`, `b`, dan `c` berpindah posisi secara berurutan.

#### Full code Screenshot:
<img width="695" height="386" alt="Image" src="https://github.com/user-attachments/assets/c58a5552-8ba1-4182-b4ab-daa0afe40792" />

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

## Kesimpulan
Ketiga program yang telah dibuat memiliki tujuan yang berbeda namun sama-sama melatih pemahaman dasar pemrograman C++. Program pertama digunakan untuk melakukan operasi aritmatika pada matriks, yaitu penjumlahan, pengurangan, dan perkalian. Program kedua menunjukkan cara menukar posisi tiga bilangan menggunakan variabel sementara. Sedangkan program ketiga menampilkan penerapan array dengan fungsi tambahan untuk mencari nilai maksimum, minimum, dan rata-rata melalui menu interaktif. Secara keseluruhan, ketiga program ini membantu memahami penggunaan array, perulangan, fungsi, serta logika dasar dalam penyusunan program C++.

## Referensi
[1] GeeksforGeeks. (n.d.). Different Operations on Matrices in C++. Retrieved October 9, 2025, from https://www.geeksforgeeks.org/different-operation-matrices/
[2] GeeksforGeeks. (n.d.). Maximum and Minimum in an Array in C++. Retrieved October 9, 2025, from https://www.geeksforgeeks.org/dsa/maximum-and-minimum-in-an-array/
[3] GeeksforGeeks. (n.d.). Menu Driven Program in C++ to Perform Various Basic Operations on Array. Retrieved October 9, 2025, from https://www.geeksforgeeks.org/dsa/menu-driven-program-in-cpp-to-perform-various-basic-operations-on-array/









