  # <h1 align="center">Laporan Praktikum Modul Pengenalan Bahasa C++ (1)</h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

Modul 2: Pengenalan Bahasa C++ (Bagian Kedua) membahas dasar logika dalam pemrograman C++. Di dalamnya dijelaskan cara membuat program yang bisa menerima input, memproses data, dan menampilkan hasil. Program C++ dimulai dengan #include <iostream> dan fungsi utama int main(). Perintah cout digunakan untuk menampilkan teks ke layar, sedangkan cin digunakan untuk membaca input dari pengguna. Variabel dipakai untuk menyimpan nilai, dan setiap variabel memiliki tipe data, seperti int untuk angka bulat, float untuk angka desimal, char untuk huruf, string untuk teks, dan bool untuk benar atau salah. Operator digunakan untuk menghitung atau membandingkan nilai, misalnya +, -, *, /, ==, <, > dan sebagainya. Percabangan seperti if dan switch digunakan agar program bisa mengambil keputusan berdasarkan kondisi tertentu. Perulangan seperti for, while, dan do-while digunakan agar perintah bisa dijalankan berulang kali. Secara singkat, modul ini mengajarkan dasar logika pemrograman dengan C++ agar program bisa berpikir dan bekerja sesuai perintah yang diberikan.
## Guided 

### 1. [Pengenalan Bahasa C++(Bagian Kedua]

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

int main() {
    int A[3][3], B[3][3], C[3][3];
    cout << "Masukkan matriks A:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cin >> A[i][j];
        }
    }
    cout << "Masukkan matriks B:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cin >> B[i][j];
        }
    }
    cout << "Penjumlahan:" << endl;
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            C[i][j]=A[i][j]+B[i][j];
            cout<<C[i][j]<<" ";
        }
        cout<<endl;
    }
    cout << "Pengurangan:" << endl;
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            C[i][j]=A[i][j]-B[i][j];
            cout<<C[i][j]<<" ";
        }
        cout<<endl;
    }
    cout << "Perkalian:" << endl;
    for(int i=0;i<3;i++){   
        for(int j=0;j<3;j++){
            C[i][j]=0;
            for(int k=0;k<3;k++){
                C[i][j]+=A[i][k]*B[k][j];
            }
            cout<<C[i][j]<<" ";
        }
        cout<<endl;
    }
}

```
#### Output:
<img width="643" height="943" alt="Image" src="https://github.com/user-attachments/assets/cae7fee4-c6cf-4e12-a597-f997107a2244" />

Kode di atas berfungsi untuk melakukan operasi penjumlahan, pengurangan, dan perkalian antara dua matriks berukuran 3x3. Program meminta pengguna untuk memasukkan nilai elemen-elemen matriks A dan B menggunakan `cin`, lalu hasilnya disimpan ke dalam matriks C. Setelah itu, program menampilkan hasil penjumlahan, pengurangan, dan perkalian kedua matriks menggunakan `cout` dengan perulangan bersarang untuk mengakses setiap elemen matriks satu per satu.


#### Full code Screenshot:
<img width="1394" height="996" alt="Image" src="https://github.com/user-attachments/assets/52fb48bc-3dec-4091-9901-0b9a53896ffd" />

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







