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

Kode di atas digunakan untuk memberikan output-an hasil penjumlahan, pengurangan, perkalian, dan pembagian dari dua bilangan yang di input pengguna

#### Full code Screenshot:
![240309_10h21m35s_screenshot](https://github.com/suxeno/Struktur-Data-Assignment/assets/111122086/41e9641c-ad4e-4e50-9ca4-a0215e336b04)

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

Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function cout untuk mengeksekusi nya.

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

Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function cout untuk mengeksekusi nya.

#### Full code Screenshot:
![240309_10h21m35s_screenshot](https://github.com/suxeno/Struktur-Data-Assignment/assets/111122086/41e9641c-ad4e-4e50-9ca4-a0215e336b04)


## Kesimpulan
Ringkasan dan interpretasi pandangan kalia dari hasil praktikum dan pembelajaran yang didapat[1].

## Referensi
[1] I. Holm, Narrator, and J. Fullerton-Smith, Producer, How to Build a Human [DVD]. London: BBC; 2002.
