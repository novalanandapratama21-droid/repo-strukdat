  # <h1 align="center">Laporan Praktikum Modul Pengenalan Bahasa C++ (1)</h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

Modul 2: Pengenalan Bahasa C++ (Bagian Kedua) membahas dasar logika dalam pemrograman C++. Di dalamnya dijelaskan cara membuat program yang bisa menerima input, memproses data, dan menampilkan hasil. Program C++ dimulai dengan #include <iostream> dan fungsi utama int main(). Perintah cout digunakan untuk menampilkan teks ke layar, sedangkan cin digunakan untuk membaca input dari pengguna. Variabel dipakai untuk menyimpan nilai, dan setiap variabel memiliki tipe data, seperti int untuk angka bulat, float untuk angka desimal, char untuk huruf, string untuk teks, dan bool untuk benar atau salah. Operator digunakan untuk menghitung atau membandingkan nilai, misalnya +, -, *, /, ==, <, > dan sebagainya. Percabangan seperti if dan switch digunakan agar program bisa mengambil keputusan berdasarkan kondisi tertentu. Perulangan seperti for, while, dan do-while digunakan agar perintah bisa dijalankan berulang kali. Secara singkat, modul ini mengajarkan dasar logika pemrograman dengan C++ agar program bisa berpikir dan bekerja sesuai perintah yang diberikan.
## Guided 

### 1. [Pengenalan Bahasa C++(Bagian Kedua]

```C++
#include <iostream>

using namespace std;

void tulis (int x){
    for (int i = 0; 1 < x; i++ ){
        cout << "Baris ke -: " << i+1 << endl;
    }
}
int main () {
    int jum;
    cout << "Jumlah baris kata: ";
    cin >> jum;
    tulis(jum);
    
    return 0;
}
```
Kode di atas berfungsi untuk menampilkan teks “Baris ke-” sesuai jumlah yang dimasukkan pengguna. Nilai input disimpan pada variabel `jum`, lalu dikirim ke fungsi `tulis()` yang menggunakan perulangan `for` untuk mencetak baris secara berurutan. Namun, ada kesalahan pada kondisi perulangan (`1 < x` seharusnya `i < x`), sehingga perlu diperbaiki agar program dapat berjalan dengan benar.

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
<img width="619" height="274" alt="Image" src="https://github.com/user-attachments/assets/f66d4767-7d4f-4bf5-bb40-44d833ffd3bb" />

Kode di atas berfungsi untuk menghitung penjumlahan, pengurangan, perkalian, dan pembagian dari dua angka yang dimasukkan pengguna. Program meminta input dua angka melalui `cin`, lalu menampilkan hasil operasi menggunakan `cout`. Jika angka kedua bernilai nol, program menampilkan pesan bahwa pembagian tidak dapat dilakukan.


#### Full code Screenshot:
<img width="897" height="694" alt="Image" src="https://github.com/user-attachments/assets/f07146c9-4157-4686-9264-b1c855fb45d2" />

### 2. [Soal]
```C++
#include <iostream>
using namespace std;

int main() {
    int angka;
    cout << "Masukkan bilangan (0-100): ";
    cin >> angka;

    string nilai[] = {"nol", "satu", "dua", "tiga", "empat", "lima",
                     "enam", "tujuh", "delapan", "sembilan"};

    if (angka < 10)
        cout << angka << " : " << nilai[angka];
    else if (angka == 10)
        cout << angka << " : sepuluh";
    else if (angka == 11)
        cout << angka << " : sebelas";
    else if (angka < 20)
        cout << angka << " : " << nilai[angka - 10] << " belas";
    else if (angka < 100) {
        int puluhan = angka / 10;
        int sisa = angka % 10;
        cout << angka << " : " << nilai[puluhan] << " puluh";
        if (sisa != 0)
            cout << " " << nilai[sisa];
    } else if (angka == 100)
        cout << angka << " : seratus";
    else
        cout << "Bilangan di luar jangkauan (0-100)";

    cout << endl;
    return 0;
}
```
#### Output:
<img width="636" height="492" alt="Image" src="https://github.com/user-attachments/assets/49a287ca-81fe-401b-bfc3-516c58894053" />

Kode di atas berfungsi mengubah angka 0–100 menjadi bentuk tulisan bahasa Indonesia. Program meminta input angka, lalu menggunakan `if-else` untuk menentukan hasilnya. Angka di bawah 10 diambil dari array `nilai`, sedangkan angka 10–19 dan 20–99 diproses dengan aturan “belas” dan “puluh”. Jika angka 100, ditampilkan “seratus”, dan jika di luar rentang, muncul pesan peringatan.

#### Full code Screenshot:
<img width="1381" height="985" alt="Image" src="https://github.com/user-attachments/assets/0dec2ecb-e37f-4b9d-a188-df118dabb74d" />

### 3. [Soal]
```C++
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Input: ";
    cin >> n;
    cout << "Output:\n";

    for (int i = n; i >= 1; i--) {
    
        for (int s = 0; s < (n - i) * 2; s++)
            cout << " ";


        for (int j = i; j >= 1; j--)
            cout << j << " ";

        cout << "* ";

        for (int j = 1; j <= i; j++)
            cout << j << " ";

        cout << endl;
    }

    return 0;
}
```
#### Output:
<img width="647" height="256" alt="Image" src="https://github.com/user-attachments/assets/7f9d038e-2fc9-4292-a0e0-25dc1ee6f0e2" />

Kode di atas digunakan untuk menampilkan pola angka berbentuk segitiga terbalik dengan simbol bintang (*) di tengahnya. Program meminta pengguna memasukkan nilai `n`, lalu menggunakan dua perulangan `for` bersarang untuk mencetak spasi dan angka secara teratur. Angka dicetak menurun di sisi kiri dan menaik di sisi kanan, sedangkan tanda bintang ditempatkan di tengah sebagai pemisah. Proses ini diulang hingga baris terakhir, sehingga terbentuk pola simetris dari angka dan bintang.


#### Full code Screenshot:
<img width="712" height="885" alt="Screenshot 2025-10-09 142944" src="https://github.com/user-attachments/assets/5a832f44-1969-47b1-8ca7-31780fea1dbf" />


## Kesimpulan
Kesimpulan dari ketiga program di atas adalah bahwa masing-masing memiliki fungsi dan logika yang berbeda, tapi sama-sama menggunakan dasar pemrograman C++. Program pertama digunakan untuk menghitung operasi aritmatika sederhana seperti penjumlahan, pengurangan, perkalian, dan pembagian. Program kedua menunjukkan penerapan struktur *if-else* untuk mengubah angka menjadi bentuk tulisan dalam bahasa Indonesia. Sedangkan program ketiga menerapkan konsep *looping bersarang* untuk menampilkan pola angka yang simetris dengan tanda bintang di tengahnya. Dari ketiga program tersebut bisa disimpulkan bahwa pemahaman terhadap input/output, percabangan, dan perulangan sangat penting karena menjadi dasar dalam menyusun logika program yang lebih kompleks.


## Referensi
[1] GeeksforGeeks. (2023, July 7). Basic Input/Output in C++. https://www.geeksforgeeks.org/basic-input-output-c/
[2] CodesCracker. (n.d.). C++ Program to Convert Number to Words. https://codescracker.com/cpp/program/cpp-program-convert-number-to-words.htm
[3] Modul 1. (2025). Code::Blocks IDE & Pengenalan Bahasa C++ (Bagian Pertama).

