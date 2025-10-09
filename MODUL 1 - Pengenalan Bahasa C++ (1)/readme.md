# <h1 align="center">Laporan Praktikum Modul Pengenalan Bahasa C++ (1)</h1>
<p align="center">Arvinanto Bahtiar</p>

## Dasar Teori

Berikan penjelasan teori terkait materi modul ini dengan bahasa anda sendiri serta susunan yang terstruktur per topiknya.

## Guided 

### 1. [Nama Topik]

```C++
#include <iostream>
using namespace std;

int main() {
    cout << "ini adalah file code guided praktikan" << endl;
    return 0;
}
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function cout untuk mengeksekusi nya.

## Unguided 

### 1. [Soal]

#include <iostream>

using namespace std;

int main() {
    float a, b;

    cout << "Masukan Angka Pertama: ";
    cin >> a;
    cout << "Masukan Angka Kedua: ";
    cin >> b;
    cout << "Hasil Penjumlahan: " << a + b << endl;
    cout << "Hasil Pengurangan: " << a - b << endl;
    cout << "Hasil Perkalian: " << a * b << endl;

    if (b != 0)
        cout << "Hasil pembagian: " << a / b << endl;
    else
        cout << "Pembagian tidak dapat dilakukan (b = 0)" << endl;

    return 0;
}
#### Output:
<img width="619" height="274" alt="Image" src="https://github.com/user-attachments/assets/f66d4767-7d4f-4bf5-bb40-44d833ffd3bb" />

Kode di atas berfungsi untuk menghitung penjumlahan, pengurangan, perkalian, dan pembagian dari dua angka yang dimasukkan pengguna. Program meminta input dua angka melalui `cin`, lalu menampilkan hasil operasi menggunakan `cout`. Jika angka kedua bernilai nol, program menampilkan pesan bahwa pembagian tidak dapat dilakukan.


#### Full code Screenshot:
<img width="1403" height="1079" alt="Image" src="https://github.com/user-attachments/assets/f4680476-3563-4d3c-ba7c-30357c402b15" />

### 2. [Soal]

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

#### Output:
![240302_00h00m06s_screenshot](https://github.com/suxeno/Struktur-Data-Assignment/assets/111122086/6d1727a8-fb77-4ecf-81ff-5de9386686b7)

Kode di atas berfungsi mengubah angka 0–100 menjadi bentuk tulisan bahasa Indonesia. Program meminta input angka, lalu menggunakan `if-else` untuk menentukan hasilnya. Angka di bawah 10 diambil dari array `nilai`, sedangkan angka 10–19 dan 20–99 diproses dengan aturan “belas” dan “puluh”. Jika angka 100, ditampilkan “seratus”, dan jika di luar rentang, muncul pesan peringatan.

#### Full code Screenshot:
![240309_10h21m35s_screenshot](https://github.com/suxeno/Struktur-Data-Assignment/assets/111122086/41e9641c-ad4e-4e50-9ca4-a0215e336b04)

### 3. [Soal]

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
#### Output:
![240302_00h00m06s_screenshot](https://github.com/suxeno/Struktur-Data-Assignment/assets/111122086/6d1727a8-fb77-4ecf-81ff-5de9386686b7)

Kode di atas digunakan untuk menampilkan pola angka berbentuk segitiga terbalik dengan simbol bintang (*) di tengahnya. Program meminta pengguna memasukkan nilai `n`, lalu menggunakan dua perulangan `for` bersarang untuk mencetak spasi dan angka secara teratur. Angka dicetak menurun di sisi kiri dan menaik di sisi kanan, sedangkan tanda bintang ditempatkan di tengah sebagai pemisah. Proses ini diulang hingga baris terakhir, sehingga terbentuk pola simetris dari angka dan bintang.


#### Full code Screenshot:
![240309_10h21m35s_screenshot](https://github.com/suxeno/Struktur-Data-Assignment/assets/111122086/41e9641c-ad4e-4e50-9ca4-a0215e336b04)


## Kesimpulan
Kesimpulan dari ketiga program di atas adalah bahwa masing-masing memiliki fungsi dan logika yang berbeda, tapi sama-sama menggunakan dasar pemrograman C++. Program pertama digunakan untuk menghitung operasi aritmatika sederhana seperti penjumlahan, pengurangan, perkalian, dan pembagian. Program kedua menunjukkan penerapan struktur *if-else* untuk mengubah angka menjadi bentuk tulisan dalam bahasa Indonesia. Sedangkan program ketiga menerapkan konsep *looping bersarang* untuk menampilkan pola angka yang simetris dengan tanda bintang di tengahnya. Dari ketiga program tersebut bisa disimpulkan bahwa pemahaman terhadap input/output, percabangan, dan perulangan sangat penting karena menjadi dasar dalam menyusun logika program yang lebih kompleks.


## Referensi
[1] Modul 1
[2] Tutorialspoint
[3] GeeksforGeeks
