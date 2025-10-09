 # <h1 align="center">Laporan Praktikum Modul Pengenalan Bahasa C++ (1)</h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

Modul ini membahas dasar-dasar pemrograman C++ dengan menggunakan Code::Blocks sebagai IDE. Code::Blocks digunakan untuk menulis, menjalankan, dan mengecek program agar lebih mudah dan teratur. Di dalam modul dijelaskan struktur dasar program C++, yang diawali dengan `#include <iostream>` dan fungsi utama `int main()`. Perintah `cout` digunakan untuk menampilkan output ke layar, sedangkan `cin` untuk menerima input dari pengguna. Modul ini juga menjelaskan tipe data seperti `int`, `float`, dan `string`, serta cara menggunakan variabel untuk menyimpan nilai. Selain itu, dibahas juga penggunaan operator aritmatika dan logika, struktur percabangan `if-else`, serta perulangan seperti `for` dan `while`. Secara keseluruhan, modul ini membantu memahami konsep dasar C++ yang penting untuk membuat program sederhana.

## Guided 

### 1. [Code Blocks Ide & Pengenalan Bahasa C++(Bagian Pertama]

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

Kode di atas berfungsi untuk menampilkan teks “Baris ke-” sesuai jumlah yang dimasukkan pengguna. Nilai input disimpan pada variabel `jum`, lalu dikirim ke fungsi `tulis()` yang menggunakan perulangan `for` untuk mencetak baris secara berurutan. Namun, ada kesalahan pada kondisi perulangan (`1 < x` seharusnya `i < x`), sehingga perlu diperbaiki agar program dapat berjalan dengan benar.

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
<img width="897" height="694" alt="Image" src="https://github.com/user-attachments/assets/f07146c9-4157-4686-9264-b1c855fb45d2" />

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
<img width="636" height="492" alt="Image" src="https://github.com/user-attachments/assets/49a287ca-81fe-401b-bfc3-516c58894053" />

Kode di atas berfungsi mengubah angka 0–100 menjadi bentuk tulisan bahasa Indonesia. Program meminta input angka, lalu menggunakan `if-else` untuk menentukan hasilnya. Angka di bawah 10 diambil dari array `nilai`, sedangkan angka 10–19 dan 20–99 diproses dengan aturan “belas” dan “puluh”. Jika angka 100, ditampilkan “seratus”, dan jika di luar rentang, muncul pesan peringatan.

#### Full code Screenshot:
<img width="1381" height="985" alt="Image" src="https://github.com/user-attachments/assets/0dec2ecb-e37f-4b9d-a188-df118dabb74d" />

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
<img width="647" height="256" alt="Image" src="https://github.com/user-attachments/assets/7f9d038e-2fc9-4292-a0e0-25dc1ee6f0e2" />

Kode di atas digunakan untuk menampilkan pola angka berbentuk segitiga terbalik dengan simbol bintang (*) di tengahnya. Program meminta pengguna memasukkan nilai `n`, lalu menggunakan dua perulangan `for` bersarang untuk mencetak spasi dan angka secara teratur. Angka dicetak menurun di sisi kiri dan menaik di sisi kanan, sedangkan tanda bintang ditempatkan di tengah sebagai pemisah. Proses ini diulang hingga baris terakhir, sehingga terbentuk pola simetris dari angka dan bintang.


#### Full code Screenshot:
<img width="712" height="885" alt="Screenshot 2025-10-09 142944" src="https://github.com/user-attachments/assets/5a832f44-1969-47b1-8ca7-31780fea1dbf" />


## Kesimpulan
Kesimpulan dari ketiga program di atas adalah bahwa masing-masing memiliki fungsi dan logika yang berbeda, tapi sama-sama menggunakan dasar pemrograman C++. Program pertama digunakan untuk menghitung operasi aritmatika sederhana seperti penjumlahan, pengurangan, perkalian, dan pembagian. Program kedua menunjukkan penerapan struktur *if-else* untuk mengubah angka menjadi bentuk tulisan dalam bahasa Indonesia. Sedangkan program ketiga menerapkan konsep *looping bersarang* untuk menampilkan pola angka yang simetris dengan tanda bintang di tengahnya. Dari ketiga program tersebut bisa disimpulkan bahwa pemahaman terhadap input/output, percabangan, dan perulangan sangat penting karena menjadi dasar dalam menyusun logika program yang lebih kompleks.


## Referensi
[1] Modul 1
[2] Tutorialspoint
[3] GeeksforGeeks
