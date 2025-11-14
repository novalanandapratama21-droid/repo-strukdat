# <h1 align="center">Laporan Praktikum Modul Doubly Linked List (Bagian Kedua)</h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

Doubly Linked list adalah linked list yang masing – masing elemen nya memiliki 2 successor, yaitu successor yang menunjuk pada elemen sebelumnya (prev) dan successor yang menunjuk pada elemen sesudahnya (next). Doubly linked list juga menggunakan dua buah successor utama yang terdapat pada list, yaitu first (successor yang menunjuk elemen pertama) dan last (susesor yang menunjuk elemen terakhir list).
Komponen-komponen dalam Doubly linked list:
1. First : pointer pada list yang menunjuk pada elemen pertama list.
2. Last : pointer pada list yang menunjuk pada elemen terakhir list.
3. Next : pointer pada elemen sebagai successor yang menunjuk pada elemen didepannya.
4. Prev : pointer pada elemen sebagai successor yang menunjuk pada elemen dibelakangnya.
## Guided 

### 1. [Doubly Linked List (Bagian Kedua)]
```C++
#include <iostream>
#define Nil NULL
using namespace std;

typedef int infotype; // Definisikan tipe data infotype sebagai integer untuk menyimpan informasi elemen
typedef struct elmlist *address; // Definisikan tipe address sebagai pointer ke struct elmlist

struct elmlist {
    infotype info; // Deklarasikan field info untuk menyimpan data elemen
    address next;
    address prev;
};

struct List { 
    address first; 
    address last; 
}; 

void insertFirst(List &L, address P) { 
    P->next = L.first; // Set pointer next dari P ke elemen pertama saat ini
    P->prev = Nil; // Set pointer prev dari P ke Nil karena menjadi elemen pertama
    if (L.first != Nil) L.first->prev = P; // Jika list tidak kosong, set prev elemen pertama lama ke P
    else L.last = P; // Jika list kosong, set last juga ke P
    L.first = P; // Update first list menjadi P
} 

void insertLast(List &L, address P) { 
    P->prev = L.last; // Set pointer prev dari P ke elemen terakhir saat ini
    P->next = Nil; // Set pointer next dari P ke Nil karena menjadi elemen terakhir
    if (L.last != Nil) L.last->next = P; // Jika list tidak kosong, set next elemen terakhir lama ke P
    else L.first = P; // Jika list kosong, set first juga ke P
    L.last = P; // Update last list menjadi P
} 

void insertAfter(List &L, address P, address R) { // Definisikan fungsi insertAfter untuk menyisipkan elemen setelah R
    P->next = R->next; // Set pointer next dari P ke elemen setelah R
    P->prev = R; // Set pointer prev dari P ke R
    if (R->next != Nil) R->next->prev = P; // Jika ada elemen setelah R, set prev elemen tersebut ke P
    else L.last = P; // Jika R adalah terakhir, update last menjadi P
    R->next = P; // Set next dari R ke P
}

address alokasi(infotype x) { // Definisikan fungsi alokasi untuk membuat elemen baru
    address P = new elmlist; // Alokasikan memori baru untuk elemen
    P->info = x; // Set info elemen dengan nilai x
    P->next = Nil; // Set next elemen ke Nil
    P->prev = Nil; // Set prev elemen ke Nil
    return P; 
} 

void printInfo(List L) { // Definisikan fungsi printInfo untuk mencetak isi list
    address P = L.first; // Set P ke elemen pertama list
    while (P != Nil) { // Loop selama P tidak Nil
        cout << P->info << " "; // Cetak info dari P 
        P = P->next; // Pindah ke elemen berikutnya
    } 
    cout << endl; 
}

int main() { 
    List L; 
    L.first = Nil; 
    L.last = Nil;
    address P1 = alokasi(1); 
    insertFirst(L, P1); 
    address P2 = alokasi(2); 
    insertLast(L, P2); 
    address P3 = alokasi(3); 
    insertAfter(L, P3, P1); 
    printInfo(L); 
    return 0; 
}
```

Program ini membuat struktur Doubly Linked List sederhana yang dapat menambah elemen di depan, di belakang, dan di tengah list. Setiap node memiliki dua pointer, yaitu next dan prev, sehingga hubungan antar-elemen bisa diakses dua arah. Fungsi insertFirst, insertLast, dan insertAfter digunakan untuk menempatkan node baru sesuai posisinya dengan mengatur ulang pointer secara benar agar struktur list tetap konsisten. Fungsi alokasi membuat node baru, sementara printInfo menampilkan seluruh isi list dari elemen pertama hingga terakhir. Pada bagian main, elemen 1 ditambahkan ke depan, elemen 2 ke belakang, dan elemen 3 disisipkan setelah elemen pertama, sehingga list akhirnya berisi 1 3 2.

## Unguided 

### 1. [Soal]
*Doublylist.h*
```C++
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H
#include <iostream>
using namespace std;

#define Nil NULL

struct kendaraan {
    string nopol;
    string warna;
    int thnBuat;
};

typedef kendaraan infotype;

struct ElmList;
typedef ElmList* address;

struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);

#endif
```
*Doublylist.cpp*
```C++
#include "Doublylist.h"

void createList(List &L){
    L.First = Nil;
    L.Last = Nil;
}

address alokasi(infotype x){
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    P->prev = Nil;
    return P;
}

void dealokasi(address &P){
    delete P;
    P = Nil;
}

void insertLast(List &L, address P){
    if(L.First == Nil){
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;
        L.Last->next = P;
        L.Last = P;
    }
}

void printInfo(List L){
    address P = L.First;
    while(P != Nil){
        cout << "no polisi : " << P->info.nopol << endl;
        cout << "warna     : " << P->info.warna << endl;
        cout << "tahun     : " << P->info.thnBuat << endl;
        cout << endl;
        P = P->next;
    }
}
```
*main.cpp*
```C++
#include <iostream>
#include "Doublylist.h"

using namespace std;

int main(){
    List L;
    createList(L);

    int n = 3;
    for(int i = 0; i < n; i++){
        infotype x;
        cout << "masukkan nomor polisi : ";
        cin >> x.nopol;

        address Q = L.First;
        bool found = false;
        while(Q != Nil){
            if(Q->info.nopol == x.nopol){
                found = true;
            }
            Q = Q->next;
        }

        if(found){
            cout << "nomor polisi sudah terdaftar" << endl;
            i--;
            continue;
        }

        cout << "masukkan warna kendaraan: ";
        cin >> x.warna;
        cout << "masukkan tahun kendaraan: ";
        cin >> x.thnBuat;

        address P = alokasi(x);
        insertLast(L, P);
    }

    cout << "\nDATA LIST 1\n\n";
    printInfo(L);
}
```
#### Output:
<img width="736" height="542" alt="image" src="https://github.com/user-attachments/assets/915ba0ca-34f6-4713-b777-bb0a6ed94bec" />

Kode pada soal pertama berfungsi untuk membangun sebuah ADT Doubly Linked List yang mampu menyimpan data kendaraan secara dinamis. Struktur data dibuat berdasarkan modul, yaitu node yang memiliki info, next, dan prev, serta list yang memiliki First dan Last sebagai penanda elemen awal dan akhir. Fungsi‐fungsi seperti createList, alokasi, dan dealokasi memastikan list dapat dibentuk dan node dapat dibuat atau dibuang dari memori. Selain itu, insertLast digunakan untuk menambahkan data baru ke ujung list sambil menjaga konsistensi pointer prev dan next, sedangkan printInfo menampilkan seluruh isi list secara berurutan dari depan ke belakang. Secara keseluruhan, kode ini berfungsi sebagai implementasi dasar Doubly Linked List yang mampu menambah dan menampilkan data kendaraan secara terstruktur.

#### Full code Screenshot:
<img width="611" height="842" alt="image" src="https://github.com/user-attachments/assets/de6965e3-9c50-4e69-83ac-b15943a4c71e" />
<img width="643" height="889" alt="image" src="https://github.com/user-attachments/assets/e03bab96-f48a-4ab4-bce0-75987c0729b3" />
<img width="618" height="908" alt="image" src="https://github.com/user-attachments/assets/aee0e073-5862-4c29-aa91-d9c76aad1f66" />

### 2. [Soal]
*Doublylist.h*
```C++
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H
#include <iostream>
using namespace std;

#define Nil NULL

struct kendaraan {
    string nopol;
    string warna;
    int thnBuat;
};

typedef kendaraan infotype;

struct ElmList;
typedef ElmList* address;

struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);
address findElm(List L, string key);

#endif
```
*Doublylist.cpp*
```C++
#include "Doublylist.h"

void createList(List &L){
    L.First = Nil;
    L.Last = Nil;
}

address alokasi(infotype x){
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    P->prev = Nil;
    return P;
}

void dealokasi(address &P){
    delete P;
    P = Nil;
}

void insertLast(List &L, address P){
    if(L.First == Nil){
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;
        L.Last->next = P;
        L.Last = P;
    }
}

void printInfo(List L){
    address P = L.First;
    while(P != Nil){
        cout << "no polisi : " << P->info.nopol << endl;
        cout << "warna     : " << P->info.warna << endl;
        cout << "tahun     : " << P->info.thnBuat << endl;
        cout << endl;
        P = P->next;
    }
}

address findElm(List L, string key){
    address P = L.First;
    while(P != Nil){
        if(P->info.nopol == key){
            return P;    
        }
        P = P->next;
    }
    return Nil;
}
```
*main.cpp*
```C++
#include <iostream>
#include "Doublylist.h"

using namespace std;

int main(){
    List L;
    createList(L);

    int n = 3;
    for(int i = 0; i < n; i++){
        infotype x;
        cout << "masukkan nomor polisi : ";
        cin >> x.nopol;

        address Q = L.First;
        bool found = false;
        while(Q != Nil){
            if(Q->info.nopol == x.nopol){
                found = true;
            }
            Q = Q->next;
        }

        if(found){
            cout << "nomor polisi sudah terdaftar" << endl;
            i--;
            continue;
        }

        cout << "masukkan warna kendaraan: ";
        cin >> x.warna;
        cout << "masukkan tahun kendaraan: ";
        cin >> x.thnBuat;

        address P = alokasi(x);
        insertLast(L, P);
    }
    
    cout << "\nDATA LIST 1\n\n";
    printInfo(L);

    string cari;
        cout << "Masukkan Nomor Polisi yang dicari : ";
        cin >> cari;

    address H = findElm(L, cari);

        if(H != Nil){
            cout << "\nData ditemukan:\n";
            cout << "Nomor Polisi : " << H->info.nopol << endl;
            cout << "Warna        : " << H->info.warna << endl;
            cout << "Tahun        : " << H->info.thnBuat << endl;
        } else {
            cout << "Data tidak ditemukan." << endl;
        } 
}
```
#### Output:
<img width="737" height="699" alt="image" src="https://github.com/user-attachments/assets/1d66c0c5-27b0-405c-aa74-52d9c842137d" />

Kode pada soal kedua berfungsi untuk mencari elemen tertentu di dalam Doubly Linked List berdasarkan nomor polisi menggunakan fungsi findElm. Proses pencarian dilakukan dengan menelusuri node satu per satu dari pointer First menggunakan pointer next hingga menemukan node dengan nilai nopol yang sesuai. Jika data ditemukan, alamat node tersebut dikembalikan sehingga dapat digunakan pada proses lain, seperti menampilkan detail data atau untuk keperluan delete. Jika tidak ditemukan, fungsi mengembalikan Nil sebagai tanda bahwa data tidak ada dalam list. Cara kerja ini sesuai teori modul di mana pencarian pada Doubly Linked List dilakukan secara linear namun tetap efisien karena setiap node memiliki akses pointer yang jelas.

#### Full code Screenshot:
<img width="617" height="832" alt="image" src="https://github.com/user-attachments/assets/b0d5d133-01a2-456e-a711-657d9d0d7ba7" />
<img width="525" height="915" alt="image" src="https://github.com/user-attachments/assets/23bf2b66-934b-42d0-a412-4edb03c388d3" />
<img width="568" height="832" alt="image" src="https://github.com/user-attachments/assets/a9e25c92-8f19-4b42-aed5-c1bebe2c06fe" />

### 3. [Soal]
*Doublylist.h*
```C++
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H
#include <iostream>
using namespace std;

#define Nil NULL

struct kendaraan {
    string nopol;
    string warna;
    int thnBuat;
};

typedef kendaraan infotype;

struct ElmList;
typedef ElmList* address;

struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address First;
    address Last;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);
address findElm(List L, string key);
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(address Prec, address &P);

#endif
```
*Doublylist.cpp*
```C++
#include "Doublylist.h"

void createList(List &L){
    L.First = Nil;
    L.Last = Nil;
}

address alokasi(infotype x){
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    P->prev = Nil;
    return P;
}

void dealokasi(address &P){
    delete P;
    P = Nil;
}

void insertLast(List &L, address P){
    if(L.First == Nil){
        L.First = P;
        L.Last = P;
    } else {
        P->prev = L.Last;
        L.Last->next = P;
        L.Last = P;
    }
}

void printInfo(List L){
    address P = L.First;
    while(P != Nil){
        cout << "no polisi : " << P->info.nopol << endl;
        cout << "warna     : " << P->info.warna << endl;
        cout << "tahun     : " << P->info.thnBuat << endl;
        cout << endl;
        P = P->next;
    }
}

address findElm(List L, string key){
    address P = L.First;
    while(P != Nil){
        if(P->info.nopol == key){
            return P;    
        }
        P = P->next;
    }
    return Nil;
}

void deleteFirst(List &L, address &P){
    P = L.First;
    if(L.First == L.Last){
        L.First = Nil;
        L.Last = Nil;
    } else {
        L.First = P->next;
        L.First->prev = Nil;
        P->next = Nil;
    }
}

void deleteLast(List &L, address &P){
    P = L.Last;
    if(L.First == L.Last){
        L.First = Nil;
        L.Last = Nil;
    } else {
        L.Last = P->prev;
        L.Last->next = Nil;
        P->prev = Nil;
    }
}

void deleteAfter(address Prec, address &P){
    P = Prec->next;
    Prec->next = P->next;

    if(P->next != Nil){
        P->next->prev = Prec;
    }

    P->next = Nil;
    P->prev = Nil;
}
```
*main.cpp*
```C++
#include <iostream>
#include "Doublylist.h"

using namespace std;

int main(){
    List L;
    createList(L);

    int n = 3;
    for(int i = 0; i < n; i++){
        infotype x;
        cout << "masukkan nomor polisi : ";
        cin >> x.nopol;

        address Q = L.First;
        bool found = false;
        while(Q != Nil){
            if(Q->info.nopol == x.nopol){
                found = true;
            }
            Q = Q->next;
        }

        if(found){
            cout << "nomor polisi sudah terdaftar" << endl;
            i--;
            continue;
        }

        cout << "masukkan warna kendaraan: ";
        cin >> x.warna;
        cout << "masukkan tahun kendaraan: ";
        cin >> x.thnBuat;

        address P = alokasi(x);
        insertLast(L, P);
    }
    
    cout << "\nDATA LIST 1\n\n";
    printInfo(L);

    string cari;
    cout << "Masukkan Nomor Polisi yang dicari : ";
    cin >> cari;

    address H = findElm(L, cari);

    if(H != Nil){
        cout << "\nData ditemukan:\n";
        cout << "Nomor Polisi : " << H->info.nopol << endl;
        cout << "Warna        : " << H->info.warna << endl;
        cout << "Tahun        : " << H->info.thnBuat << endl;
    } else {
        cout << "Data tidak ditemukan." << endl;
    }

    string del;
    cout << "\nMasukkan nomor polisi yang ingin dihapus: ";
    cin >> del;

    address X = findElm(L, del);

    if(X != Nil){
        address P;

        if(X == L.First){
            deleteFirst(L, P);
        }
        else if(X == L.Last){
            deleteLast(L, P);
        }
        else {
            deleteAfter(X->prev, P);
        }

        dealokasi(P);
        cout << "Data berhasil dihapus.\n";
    }
    else {
        cout << "Data tidak ditemukan.\n";
    }

    cout << "\nDATA LIST SETELAH DELETE:\n\n";
    printInfo(L);

    return 0;
}
```
#### Output:
<img width="728" height="941" alt="image" src="https://github.com/user-attachments/assets/9cbd3496-22aa-4694-8a32-295fa139b5d5" />

Kode pada soal ketiga berfungsi untuk menghapus elemen dari Doubly Linked List berdasarkan nomor polisi dengan menentukan jenis penghapusan yang tepat: deleteFirst, deleteLast, atau deleteAfter. Setelah data yang akan dihapus ditemukan melalui findElm, program mengecek posisi node tersebut dalam list. Jika node berada di awal, digunakan deleteFirst; jika di akhir, dipakai deleteLast; dan jika berada di tengah, digunakan deleteAfter dengan memberikan node sebelumnya sebagai parameter. Masing-masing prosedur mengatur ulang pointer next dan prev agar hubungan antar-node tetap valid dan tidak ada pointer yang menggantung. Dengan demikian, kode ini berfungsi menjaga struktur list tetap stabil setelah proses penghapusan, sesuai dengan konsep operasi delete pada Doubly Linked List dalam modul.

#### Full code Screenshot:
<img width="612" height="874" alt="image" src="https://github.com/user-attachments/assets/e9753c2d-120d-4145-8f0b-35d095029509" />
<img width="645" height="874" alt="image" src="https://github.com/user-attachments/assets/123d64b0-7f24-4b43-9179-351386cb18b6" />
<img width="657" height="1004" alt="image" src="https://github.com/user-attachments/assets/b0e0b2e1-1c82-488a-9091-e2423d56742e" />
<img width="683" height="961" alt="image" src="https://github.com/user-attachments/assets/1f485324-45b1-448d-a9ad-7d4ab52a2ef9" />
<img width="639" height="856" alt="image" src="https://github.com/user-attachments/assets/a8e76ff6-67a3-46d0-8e07-806483a1bde7" />


## Kesimpulan
Kesimpulan dari ketiga program di atas dapat disimpulkan bahwa Doubly Linked List merupakan struktur data yang fleksibel karena setiap node memiliki pointer next dan prev, sehingga proses penambahan, pencarian, dan penghapusan data dapat dilakukan dengan mudah. Pada soal 1, program berhasil membangun ADT lengkap untuk menyimpan data kendaraan dan menampilkan seluruh isi list. Pada soal 2, fungsi findElm digunakan untuk menelusuri list dan menemukan elemen berdasarkan nomor polisi. Pada soal 3, proses delete dapat dilakukan sesuai posisi node dalam list—baik di awal, akhir, maupun tengah—dengan menjaga konsistensi pointer agar struktur list tetap valid. Secara keseluruhan, implementasi ini menunjukkan bagaimana Doubly Linked List bekerja dalam mengelola data secara dinamis dan efisien.

## Referensi
[1] Linked List — Doubly Linked List. (2024). GeeksforGeeks. https://www.geeksforgeeks.org/doubly-linked-list/
[2] Programiz. (2023). Doubly Linked List Data Structure. https://www.programiz.com/dsa/doubly-linked-list
[3] W3Schools. (2023). C++ Pointers and Structs. https://www.w3schools.com/cpp/cpp_structs.asp

