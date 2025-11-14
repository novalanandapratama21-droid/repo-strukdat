# <h1 align="center">Laporan Praktikum Modul Doubly Linked List (Bagian Pertama)</h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

Doubly Linked list adalah linked list yang masing – masing elemen nya memiliki 2 successor, yaitu successor yang menunjuk pada elemen sebelumnya (prev) dan successor yang menunjuk pada elemen sesudahnya (next). Doubly linked list juga menggunakan dua buah successor utama yang terdapat pada list, yaitu first (successor yang menunjuk elemen pertama) dan last (susesor yang menunjuk elemen terakhir list).
Komponen-komponen dalam Doubly linked list:
1. First : pointer pada list yang menunjuk pada elemen pertama list.
2. Last : pointer pada list yang menunjuk pada elemen terakhir list.
3. Next : pointer pada elemen sebagai successor yang menunjuk pada elemen didepannya.
4. Prev : pointer pada elemen sebagai successor yang menunjuk pada elemen dibelakangnya.
## Guided 

### 1. [Doubly Linked List (Bagian Pertama)]
*stack.h*
```C++
#ifndef STACK_TABLE
#define STACK_TABLE

#include <iostream>
using namespace std;

//ubah kapasitas sesuai kebutuhan
const int MAX = 10;

struct stackTable{
    int data[MAX];
    int top; // -1 = kosong

};

bool isEmpty(stackTable s);
bool isFull(stackTable s);
void createStack(stackTable &s);

void push(stackTable &s, int angka);
void pop(stackTable &s);
void update(stackTable &s, int posisi);
void view(stackTable s);
void searchData(stackTable s, int data);

#endif
```
*stack.cpp*
```C++
#include "stack.h"
#include <iostream>

using namespace std;

bool isEmpty(stackTable s) {
    return s.top == -1;
}

bool isFull(stackTable s){
    return s.top == MAX -1;
}

void createStack(stackTable &s) {
    s.top = -1;
}

void push(stackTable &s, int angka){
    if(isFull(s)){
        cout << "Stack Penuh!" << endl;
    } else {
        s.top++;
        s.data[s.top] = angka;
        cout << "Data " << angka << " berhasil ditambahkan kedalam stack!" << endl;
    }
}

void pop(stackTable &s){
    if(isEmpty(s)){
        cout << "Stack kosong!" << endl;
    } else {
        int val = s.data[s.top];
        s.top--;
        cout << "Data " << val << " Berhasil dihapus dari stack!" << endl;
    }
}

void update(stackTable &s, int posisi){
    if(isEmpty(s)){
        cout << "Stack kosong!" << endl;
        return;
    }
    if(posisi <= 0){
        cout << "Posisi tidak valid!" << endl;
        return;
    }

    //index = top - (posisi -1)
    int idx = s.top - (posisi -1);
    if(idx < 0 || idx > s.top){
        cout << "Posisi " << posisi << " Tidak valid!" << endl;
        return;
    }

    cout << "Update data posisi ke-" << posisi << endl;
    cout << "Masukkan angka: ";
    cin >> s.data[idx];
    cout << "Data berhasil diupdate!" << endl;
    cout << endl;
}

void view(stackTable s){
    if(isEmpty(s)){
        cout << "Stack Kosong!" << endl;
    } else {
        for(int i = s.top; i >= 0; --i){
            cout << s.data[i] << " ";
        }
    }
    cout << endl;
}

void searchData(stackTable s, int data){
    if(isEmpty(s)){
        cout << "Stack Kosong!" << endl;
        return;
    }
    cout << "Mencari data" << data << "..." << endl;
    int posisi = 1;
    bool found = false;

    for(int i = s.top; i >= 0; --i){
        if(s.data[i] == data){
            cout << "Data " << data << " ditemukan pada posisi ke-" << posisi << endl;
            cout << endl;
            found = true;
            break;
        }
        posisi++;
    }

    if(!found){
        cout << "Data " << data << " tidak ditemukan didalam stack!" << endl;
        cout << endl;
    }
}
```
*main.cpp*
```C++
#include "stack.h"
#include <iostream>

using namespace std;

int main(){
    stackTable s;
    createStack(s);

    push(s, 1);
    push(s, 2);
    push(s, 3);
    push(s, 4);
    push(s, 5);
    cout << endl;

    cout << "--- Stack setelah push ---" << endl;
    view(s);
    cout << endl;

    pop(s);
    pop(s);
    cout << endl;

    cout << "--- Stack setelah pop 2 kali ---" << endl;
    view(s);
    cout << endl;

    //Posisi dihitung dari TOP(1-based)
    update(s, 2);
    update(s, 1);
    update(s, 4);
    cout << endl;

    cout << "--- Stack setelah update ---" << endl;
    view(s);
    cout << endl;

    searchData(s, 4);
    searchData(s, 9);

    return 0;
}
```

Program ini mengimplementasikan struktur data Stack menggunakan array dengan kapasitas tetap. Stack disimpan dalam struct stackTable yang memiliki array data dan variabel top sebagai penanda elemen teratas. Fungsi dasar seperti push dan pop digunakan untuk menambah dan menghapus elemen sesuai prinsip LIFO, sedangkan isEmpty dan isFull memeriksa kondisi stack. Fungsi update memungkinkan perubahan nilai pada posisi tertentu yang dihitung dari bagian atas stack, view menampilkan seluruh isi stack dari atas ke bawah, dan searchData melakukan pencarian elemen mulai dari top. Dalam fungsi main, beberapa data dimasukkan, dihapus, diperbarui, dan dicari sehingga menunjukkan bagaimana operasi-operasi stack bekerja secara keseluruhan.

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

