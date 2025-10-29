  # <h1 align="center">Laporan Praktikum Modul Singly Linked List (Bagian Kedua)</h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

Modul ini membahas dasar-dasar struktur data Searching merupakan operasi dasar list dengan melakukan aktivitas pencarian terhadap node tertentu. Proses ini berjalan dengan mengunjungi setiap node dan berhenti setelah node yang dicari ketemu. Dengan melakukan operasi searching, operasi-operasi seperti insert after, delete after, dan update akan lebih mudah. Semua fungsi dasar di atas merupakan bagian dari ADT dari singgle linked list, dan aplikasi pada bahasa pemrograman Cp semua ADT tersebut tersimpan dalam file *.c dan file *.h.

## Guided 

### 1. [Singly Linked List (Bagian Pertama)]
*list.h*
```C++
//
//
#ifndef LIST_H
#define LIST_H
#define Nil NULL

#include <iostream>
using namespace std;

//deklarasi isi data struct mahasiswa
struct mahasiswa{
    string nama;
    string nim;
    int umur;
};

typedef mahasiswa dataMahasiswa; //Membiarkan nama alias dataMahasiswa untuk struct mahasiswa

typedef struct node *address; //Mendefinisikan alias address sbg pointer ke struct node

struct node{
    dataMahasiswa isidata;
    address next;
};

struct linkedlist{ //ini linked list nya
    address first;
};

//semua function & prosedur yang akan dipakai
bool isEmpty(linkedlist List);
void createList(linkedlist &List);
address alokasi(string nama, string nim, int umur);
void dealokasi(address &node);
void printList(linkedlist List);
void insertFirst(linkedlist &List, address nodeBaru);
void insertAfter(linkedlist &List, address nodeBaru, address Prev);
void insertLast(linkedlist &List, address nodeBaru);

#endif
```
*list.cpp*
```C++
#include "list.h"
#include <iostream>
using namespace std;

//I.S = Initial State / kondisi awal
//F.S = Final State / kondisi akhir

//fungsi untuk cek apakah list kosong atau tidak
bool isEmpty(linkedlist List) {
    if(List.first == Nil){
        return true; 
    } else {
        return false;
    }
}

//pembuatan linked list kosong
void createList(linkedlist &List) {
    /* I.S. sembarang
       F.S. terbentuk list kosong */
    List.first = Nil;
}

//pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, string nim, int umur) { 
    /* I.S. sembarang
       F.S. mengembalikan alamat node baru dengan isidata = sesuai parameter dan next = Nil */
    address nodeBaru = new node; 
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim; 
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

//penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &node) {
    /* I.S. P terdefinisi
       F.S. memori yang digunakan node dikembalikan ke sistem */
    node->next = Nil;
    delete node;
}

//prosedur-prosedur untuk insert / menambahkan node baru kedalam list
void insertFirst(linkedlist &List, address nodeBaru) {
    /* I.S. sembarang, P sudah dialokasikan
       F.S. menempatkan elemen list (node) pada awal list */
    nodeBaru->next = List.first; 
    List.first = nodeBaru;
}

void insertAfter(linkedlist &List, address nodeBaru, address Prev) {
    /* I.S. sembarang, nodeBaru dan Prev alamat salah satu elemen list (node)
       F.S. menempatkan elemen (node) sesudah elemen node Prev */
    if (Prev != Nil) {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    } else {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

void insertLast(linkedlist &List, address nodeBaru) {
    /* I.S. sembarang, nodeBaru sudah dialokasikan
       F.S. menempatkan elemen nodeBaru pada akhir list */
    if (isEmpty(List)) {
        List.first = nodeBaru;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu->next != Nil) {
            nodeBantu = nodeBantu->next;
        }
        nodeBantu->next = nodeBaru;
    }
}

//prosedur-prosedur untuk delete / menghapus node yang ada didalam list
void delFirst(linkedlist &List){
    /* I.S. list tidak kosong
    F.S. node pertama di list terhapus*/
    address nodeHapus;
    if (isEmpty(List) == false) {
        nodeHapus = List.first;
        List.first = List.first->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
    } else {
        cout << "List kosong!" << endl;
    }
}

void delLast(linkedlist &List){
    /* I.S. list tidak kosong
    F.S. node terakhir di list terhapus */
    address nodeHapus, nodePrev;
    if(isEmpty(List) == false){
        nodeHapus = List.first;
        if(nodeHapus->next == Nil){
            List.first->next = Nil;
            dealokasi(nodeHapus);
        } else { 
            while(nodeHapus->next != Nil){
                nodePrev = nodeHapus; 
                nodeHapus = nodeHapus->next;
            }
            nodePrev->next = Nil; 
            dealokasi(nodeHapus);
        }
    } else {
        cout << "list kosong" << endl;
    }
}

void delAfter(linkedlist &List, address nodeHapus, address nodePrev){
    /* I.S. list tidak kosng, Prev alamat salah satu elemen list
    F.S. nodeBantu adalah alamat dari Prev→next, menghapus Prev→next dari list */
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else { //jika list tidak kosong
        if (nodePrev != Nil && nodePrev->next != Nil) { 
            nodeHapus = nodePrev->next;       
            nodePrev->next = nodeHapus->next;  
            nodeHapus->next = Nil;         
            dealokasi(nodeHapus);
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

//prosedur untuk menampilkan isi list
void printList(linkedlist List) {
    /* I.S. list mungkin kosong
       F.S. jika list tidak kosong menampilkan semua info yang ada pada list */
    if (isEmpty(List)) {
        cout << "List kosong." << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu != Nil) { 
            cout << "Nama : " << nodeBantu->isidata.nama << ", NIM : " << nodeBantu->isidata.nim << ", Usia : " << nodeBantu->isidata.umur << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

//function untuk menampilkan jumlah node didalam list
int nbList(linkedlist List) {
    /* I.S. list sudah ada
       F.S. menampilkan jumlah node didalam list*/
    int count = 0;
    address nodeBantu = List.first;
    while (nodeBantu != Nil) {
        count++;
        nodeBantu = nodeBantu->next; 
    }
    return count;
}

//prosedur untuk menghapus list (menghapus semua node didalam list)
void deleteList(linkedlist &List){
    /* I.S. list sudah ada
       F.S. menghapus semua node didalam list*/
    address nodeBantu, nodeHapus;
    nodeBantu = List.first;
    while(nodeBantu != Nil){
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus); 
    }
    List.first = Nil; 
    cout << "List sudah terhapus!" << endl;
}
```
*main.cpp*
```C++
#include "list.h"

#include<iostream>
using namespace std;

int main(){
    linkedlist List;
    address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
    createList(List);

    dataMahasiswa mhs;

    nodeA = alokasi("Dhimas", "2311102151", 20);
    nodeB = alokasi("Arvin", "2211110014", 21);
    nodeC = alokasi("Rizal", "2311110029", 20);
    nodeD = alokasi("Satrio", "2211102173", 21);
    nodeE = alokasi("Joshua", "2311102133", 21);

    insertFirst(List, nodeA);
    insertLast(List, nodeB);
    insertAfter(List, nodeC, nodeA);
    insertAfter(List, nodeD, nodeC);
    insertLast(List, nodeE);

    cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
    printList(List);

    return 0;
}
```

Kode ini berfungsi untuk mengelola data mahasiswa menggunakan singly linked list dalam C++. Struktur node menyimpan nama, NIM, dan umur, sedangkan linkedlist menyimpan pointer ke elemen pertama. Fungsi-fungsi di list.cpp digunakan untuk membuat list, menambah atau menghapus node, menampilkan isi list, serta menghitung jumlah elemen. Pada main.cpp, beberapa data mahasiswa dibuat dan dimasukkan ke dalam list menggunakan fungsi insertFirst, insertAfter, dan insertLast, lalu ditampilkan dengan printList. Program ini menunjukkan cara penyimpanan data dinamis yang fleksibel dengan konsep linked list.

## Unguided 

### 1. [Soal]
*Singlylist.h*
```C++
#ifndef SINGLYLIST_H_INCLUDED
#define SINGLYLIST_H_INCLUDED

#include <iostream>
using namespace std;

#define Nil NULL
typedef int infotype;
typedef struct elmList *address;

struct elmList {
    infotype info;
    address next;
};

struct List {
    address first;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void insertFirst(List &L, address P);
void printInfo(List L);

#endif
```
*Singlylist.cpp*
```C++
#include "Singlylist.h"

void createList(List &L) {
    L.first = Nil;
}

address alokasi(infotype x) {
    address P = new elmList;
    P->info = x;
    P->next = Nil;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = Nil;
}

void insertFirst(List &L, address P) {
    P->next = L.first;
    L.first = P;
}

void printInfo(List L) {
    address P = L.first;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}
```
*main.cpp*
```C++
#include "Singlylist.h"

int main() {
    List L;
    address P1, P2, P3, P4, P5= Nil;
    createList(L);

    P1 = alokasi(2);
    insertFirst(L, P1);

    P2 = alokasi(0);
    insertFirst(L, P2);

    P3 = alokasi(8);
    insertFirst(L, P3);

    P4 = alokasi(12);
    insertFirst(L, P4);

    P5 = alokasi(9);
    insertFirst(L, P5);

    printInfo(L);

    return 0;
}
```
#### Output:
<img width="726" height="128" alt="image" src="https://github.com/user-attachments/assets/9727cd84-919c-4108-9384-1874886e4068" />


Kode ini membuat dan menampilkan singly linked list dalam bahasa C++. Setiap node berisi data dan pointer ke node berikutnya, sedangkan struktur List menyimpan pointer ke node pertama. Fungsi createList menginisialisasi list, alokasi membuat node baru, insertFirst menambah node di awal, dan printInfo menampilkan isi list. Pada fungsi main, beberapa node dengan nilai berbeda ditambahkan, lalu seluruh isi list ditampilkan secara berurutan.

#### Full code Screenshot:
<img width="631" height="711" alt="image" src="https://github.com/user-attachments/assets/0603ffd9-626a-4a83-a373-afb042e26f77" />
<img width="565" height="840" alt="image" src="https://github.com/user-attachments/assets/95b86ae0-af63-4819-9873-cc345a7a87ba" />
<img width="470" height="724" alt="image" src="https://github.com/user-attachments/assets/f6527e62-c20b-4839-8950-ac99ae6dcc0c" />




### 2. [Soal]
*Singlylist.h*
```C++
#ifndef SINGLYLIST_H_INCLUDED
#define SINGLYLIST_H_INCLUDED

#include <iostream>
using namespace std;

#define Nil NULL
typedef int infotype;
typedef struct elmList *address;

struct elmList {
    infotype info;
    address next;
};

struct List {
    address first;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void insertFirst(List &L, address P);
void printInfo(List L);

void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);
int nbElmt(List L);
void deleteList(List &L);

#endif
```
*Singlylist.cpp*
```C++
#include "Singlylist.h"

void createList(List &L) {
    L.first = Nil;
}

address alokasi(infotype x) {
    address P = new elmList;
    P->info = x;
    P->next = Nil;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = Nil;
}

void insertFirst(List &L, address P) {
    P->next = L.first;
    L.first = P;
}

void printInfo(List L) {
    address P = L.first;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

void deleteFirst(List &L, address &P) {
    if (L.first != Nil) {
        P = L.first;
        L.first = P->next;
        P->next = Nil;
    }
}

void deleteLast(List &L, address &P) {
    address Q = L.first;
    if (Q == Nil) {
        P = Nil;
    } else if (Q->next == Nil) {
        P = Q;
        L.first = Nil;
    } else {
        while (Q->next->next != Nil) {
            Q = Q->next;
        }
        P = Q->next;
        Q->next = Nil;
    }
}

void deleteAfter(List &L, address Prec, address &P) {
    if (Prec != Nil && Prec->next != Nil) {
        P = Prec->next;
        Prec->next = P->next;
        P->next = Nil;
    }
}

int nbElmt(List L) {
    int count = 0;
    address P = L.first;
    while (P != Nil) {
        count++;
        P = P->next;
    }
    return count;
}

void deleteList(List &L) {
    address P;
    while (L.first != Nil) {
        deleteFirst(L, P);
        dealokasi(P);
    }
}
```
*main.cpp*
```C++
#include "Singlylist.h"

int main() {
    List L;
    address P, Q;

    createList(L);

    insertFirst(L, alokasi(2));
    insertFirst(L, alokasi(0));
    insertFirst(L, alokasi(8));
    insertFirst(L, alokasi(12));
    insertFirst(L, alokasi(9));
    
    deleteFirst(L, P);
    dealokasi(P);

    deleteLast(L, P);
    dealokasi(P);

    Q = L.first;
    deleteAfter(L, Q, P);
    dealokasi(P);

    printInfo(L);

    cout << "Jumlah node: " << nbElmt(L) << endl;

    deleteList(L);
    cout << "- List Berhasil Terhapus -" << endl;
    cout << "Jumlah node: " << nbElmt(L) << endl;

    return 0;
}
```
#### Output:
<img width="1018" height="219" alt="image" src="https://github.com/user-attachments/assets/9063df15-dc46-42f3-b718-a0ed2a486635" />

Kode ini berfungsi untuk membuat, menampilkan, dan menghapus elemen pada singly linked list dalam bahasa C++. Setiap node berisi data dan pointer ke node berikutnya, sedangkan struktur List menyimpan pointer ke node pertama. Program menyediakan fungsi untuk membuat list, menambah dan menghapus node, menghitung jumlah elemen, serta menghapus seluruh list. Pada fungsi main, beberapa node ditambahkan lalu dihapus sebagian, kemudian ditampilkan hasil akhir beserta jumlah node sebelum dan sesudah list dihapus.

#### Full code Screenshot:
<img width="631" height="828" alt="image" src="https://github.com/user-attachments/assets/5424e6b2-6ce8-4c32-b61c-45257159a86a" />
<img width="504" height="856" alt="image" src="https://github.com/user-attachments/assets/2f831c42-94ea-481e-b5c2-e0cd7b43a632" />
<img width="532" height="906" alt="image" src="https://github.com/user-attachments/assets/833db2f4-3f8a-499f-b261-c6ce60c214fd" />
<img width="525" height="741" alt="image" src="https://github.com/user-attachments/assets/4b4abf36-2d9e-4ce5-840b-8a707b36d9d1" />

## Kesimpulan
Kesimpulan dari kedua program di atas adalah bahwa keduanya menerapkan konsep struktur data dinamis menggunakan singly linked list dalam bahasa C++. Program pertama menekankan pada pembuatan dan penambahan elemen ke dalam list, sedangkan program kedua menambahkan fitur penghapusan elemen serta perhitungan jumlah node. Dari kedua program tersebut dapat disimpulkan bahwa linked list memungkinkan pengelolaan data yang lebih fleksibel dibanding array, karena elemen dapat ditambah atau dihapus tanpa perlu menggeser data lain. Pemahaman tentang pointer dan alokasi memori menjadi hal penting untuk menghindari kesalahan saat mengelola struktur data dinamis seperti ini.


## Referensi
[1] GeeksforGeeks. (n.d.). C++ Program for Deleting a Node in a Linked List. Diakses pada 23 Oktober 2025, dari https://www.geeksforgeeks.org/cpp/cpp-program-for-deleting-a-node-in-a-linked-list/
[2] W3Schools. (n.d.). DSA Linked Lists. Diakses pada 23 Oktober 2025, dari https://www.w3schools.com/dsa/dsa_theory_linkedlists.php


