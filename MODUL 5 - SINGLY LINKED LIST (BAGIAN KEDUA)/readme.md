  # <h1 align="center">Laporan Praktikum Modul Singly Linked List (Bagian Kedua)</h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

Modul ini membahas dasar-dasar struktur data Searching merupakan operasi dasar list dengan melakukan aktivitas pencarian terhadap node tertentu. Proses ini berjalan dengan mengunjungi setiap node dan berhenti setelah node yang dicari ketemu. Dengan melakukan operasi searching, operasi-operasi seperti insert after, delete after, dan update akan lebih mudah. Semua fungsi dasar di atas merupakan bagian dari ADT dari singgle linked list, dan aplikasi pada bahasa pemrograman Cp semua ADT tersebut tersimpan dalam file *.c dan file *.h.

## Guided 

### 1. [Singly Linked List (Bagian Kedua)]
*listBuah.h*
```C++
//Header guard digunakan untuk mencegah file header yg sama

#ifndef LISTBUAH_H
#define LISTBUAH_H
#define Nil NULL 

#include <iostream>
using namespace std;

// deklarasi isi data struct mahasiswa
struct buah{
    string nama;
    int jumlah;
    float harga;
};

typedef buah dataBuah; //memberikan nama alias dataMahasiswa untuk struct mahasiswa

typedef struct node *address; //mendefinisikan alias address sebagai pointer ke struct node

struct node{ //node untuk isi linked listnya, isi setiap node adalah data & pointer next
    dataBuah isidata;
    address next;
};

struct linkedlist{//ini linked listnya 
    address first;
};

//semua function &prosedur yg akan dipakai 
//materi modul 4
bool isEmpty(linkedlist List);
void createList(linkedlist &List);
address alokasi(string nama, int jumlah, float harga);
void dealokasi(address &node);
void printList(linkedlist List);
void insertFirst(linkedlist &List, address nodebaru);
void insertAfter(linkedlist &List, address nodebaru, address prev);
void insertLast(linkedlist &List, address nodebaru);
void delFirst(linkedlist &List);
void delLast(linkedlist &List);
void delAfter(linkedlist &list, address nodeHapus, address nodePrev);
int nbList(linkedlist List);
void deleteList(linkedlist &List);

//materi modul 5(part 1 - update)
void updateFirst(linkedlist List);
void updateLast(linkedlist List);
void updateAfter(linkedlist List, address prev);

//materi modul 5(part 2 - searching)
void FindNodeByData(linkedlist list, string data);
void FindNodeByAddress(linkedlist list, address node);
void FindNodeByRange(linkedlist list, float hargaAwal, float hargaAkhir);

#endif
```
*listBuah.cpp*
```C++
#include "listBuah.h"
#include <iostream>
using namespace std;

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
    List.first = Nil;
}

//pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, int jumlah, float harga) { 
    address nodeBaru = new node; 
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.jumlah = jumlah; 
    nodeBaru->isidata.harga = harga;
    nodeBaru->next = Nil;
    return nodeBaru;
}

//penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &node) {
    node->next = Nil;
    delete node;
}

//prosedur-prosedur untuk insert / menambahkan node baru kedalam list
void insertFirst(linkedlist &List, address nodeBaru) {
    nodeBaru->next = List.first; 
    List.first = nodeBaru;
}

void insertAfter(linkedlist &List, address nodeBaru, address Prev) {
    if (Prev != Nil) {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    } else {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

void insertLast(linkedlist &List, address nodeBaru) {
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
    address nodeHapus;
    if (isEmpty(List) == false) {
        nodeHapus = List.first;
        List.first = List.first->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
        cout << "Node pertama berhasil terhapus!" << endl;
    } else {
        cout << "List kosong!" << endl;
    }
}

void delLast(linkedlist &List){
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
        cout << "Node terakhir berhasil terhapus!" << endl;
    } else {
        cout << "list kosong" << endl;
    }
}

void delAfter(linkedlist &List, address nodeHapus, address nodePrev){
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else { //jika list tidak kosong
        if (nodePrev != Nil && nodePrev->next != Nil) { 
            nodeHapus = nodePrev->next;       
            nodePrev->next = nodeHapus->next;  
            nodeHapus->next = Nil;         
            dealokasi(nodeHapus);
            cout << "Node setelah node " << nodePrev->isidata.nama << " berhasil terhapus!" << endl;
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

//prosedur untuk menampilkan isi list
void printList(linkedlist List) {
    if (isEmpty(List)) {
        cout << "List kosong." << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu != Nil) { 
            cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

//function untuk menampilkan jumlah node didalam list
int nbList(linkedlist List) {
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
    address nodeBantu, nodeHapus;
    nodeBantu = List.first;
    while(nodeBantu != Nil){
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus); 
    }
    List.first = Nil; 
    cout << "List berhasil terhapus!" << endl;
}

/*----- MATERI PERTEMUAN 5 - SINGLY LINKED LIST (BAGIAN KEDUA) - PART 1 (UPDATE) -----*/
//prosedur-prosedur untuk melakukan update data node
void updateFirst(linkedlist List){ 
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else {
        cout << "Masukkan update data node pertama : " << endl;
        cout << "Nama buah : ";
        cin >> List.first->isidata.nama;
        cout << "Jumlah : ";
        cin >> List.first->isidata.jumlah;
        cout << "Harga : ";
        cin >> List.first->isidata.harga;
        cout << "Data Berhasil Diupdate!" << endl;
        cout << endl;
    }
}

void updateLast(linkedlist List){
    if (isEmpty(List) == true) {
        cout << "List Kosong!" << endl;
    } else {
        address nodeBantu = List.first; 
        while (nodeBantu->next != Nil) { //akan iterasi terus
            nodeBantu = nodeBantu->next; // bisa diganti nodeBantu=nodeAkhir
        }
        cout << "masukkan update data node terakhir : " << endl;
        cout << "Nama buah : ";
        cin >> nodeBantu->isidata.nama;
        cout << "Jumlah : ";
        cin >> nodeBantu->isidata.jumlah;
        cout << "Harga : ";
        cin >> nodeBantu->isidata.harga;
        cout << "Data Berhasil Diupdate!" << endl;
        cout << endl;
    }
}

void updateAfter(linkedlist List, address nodePrev){ //node diantara (bukan akhir atau awal) pointer mengarah ke nil
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else {
        if (nodePrev != Nil && nodePrev->next != Nil){ //next tidak mengarah ke nil
            address nodeBantu = nodePrev->next; //mengubah prosesnya
            cout << "masukkan update data node setelah node " << nodePrev->isidata.nama << " : " << endl;
            cout << "Nama buah : ";
            cin >> nodeBantu->isidata.nama;
            cout << "Jumlah : ";
            cin >> nodeBantu->isidata.jumlah;
            cout << "Harga : ";
            cin >> nodeBantu->isidata.harga;
            cout << "Data Berhasil Diupdate!" << endl;
            cout << endl;
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

/*----- MATERI PERTEMUAN 5 - SINGLY LINKED LIST (BAGIAN KEDUA) - PART 2 (SEARCHING) -----*/
//prosedur-prosedur untuk searching data
//prosedur untuk mencari node berdasarkan data
void FindNodeByData(linkedlist list, string data){
    if(isEmpty(list) == true){
        cout << "List kosong!" << endl;
    } else {
        address nodeBantu = list.first;
        int posisi = 0;
        bool found = false;
        while(nodeBantu != Nil){
            posisi++;
            if(nodeBantu->isidata.nama == data){
                cout << "Data " << data << " ditemukan pada posisi ke-" << posisi << "!" << endl;
                cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
                found = true;
                break;
            }
            nodeBantu = nodeBantu->next;
        }
        if(found == false){
            cout << "Node dengan data " << data << " tidak ditemukan!" << endl;
        }
    }
    cout << endl;
}

//prosedur untuk mencari node berdasarkan alamat node
void FindNodeByAddress(linkedlist list, address node) {
    if(isEmpty(list) == true) {
        cout << "List kosong!" << endl;
    } else {
        address nodeBantu = list.first;
        int posisi = 0;
        bool found = false;
        while (nodeBantu != Nil) {
            posisi++;
            if(nodeBantu == node) {
                cout << "Node ditemukan pada posisi ke-" << posisi << "!" << endl;
                cout << "Alamat node : " << nodeBantu << endl;
                cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
                found = true;
                break;
            }
            nodeBantu = nodeBantu->next;
        }
        if(found == false) {
            cout << "Node dengan alamat " << node << " tidak ditemukan dalam list!" << endl;
        }
    }
    cout << endl;
}

//prosedur untuk mencari node berdasarkan range data (range harga)
void FindNodeByRange(linkedlist list, float hargaAwal, float hargaAkhir) {
    if(isEmpty(list) == true) {
        cout << "List kosong!" << endl;
    } else {
        address nodeBantu = list.first;
        int posisi = 0;
        bool found = false;
        cout << "--- Buah dalam range harga " << hargaAwal << " - " << hargaAkhir << " ---" << endl;
        cout << "-------------------------------------------" << endl;
        while (nodeBantu != Nil) {
            posisi++;
            float harga = nodeBantu->isidata.harga;
            if(harga >= hargaAwal && harga <= hargaAkhir) {
                cout << "Data ditemukan pada posisi ke-" << posisi << " :" << endl;
                cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
                cout << "-------------------------------------------" << endl;
                found = true;
            }
            nodeBantu = nodeBantu->next;
        }
        if(found == false) {
            cout << "Tidak ada data buah dalam range harga tersebut!" << endl;
            cout << "-------------------------------------------" << endl;
        }
    }
    cout << endl;
}

```
*main.cpp*
```C++
#include "listBuah.h"

#include<iostream>
using namespace std;

int main(){
    linkedlist List;
    address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
    createList(List);

    dataBuah dtBuah;

    nodeA = alokasi("Jeruk", 100, 3000);
    nodeB = alokasi("Apel", 75, 4000);
    nodeC = alokasi("Pir", 87, 5000);
    nodeD = alokasi("Semangka", 43, 11500);
    nodeE = alokasi("Durian", 15, 31450);

    insertFirst(List, nodeA);
    insertLast(List, nodeB);
    insertAfter(List, nodeC, nodeA);
    insertAfter(List, nodeD, nodeC);
    insertLast(List, nodeE);

    cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
    printList(List);
    cout << "Jumlah node : " << nbList(List) << endl;
    cout << endl;

   updateFirst(List);
   updateLast(List);
   updateAfter(List, nodeD);

    cout << "--- ISI LIST SETELAH DILAKUKAN UPDATE ---" << endl;
    printList(List);
    cout << "Jumlah node : " << nbList(List) << endl;
    cout << endl;

    FindNodeByData(List, "Kelapa");
    FindNodeByAddress(List, nodeC);
    FindNodeByRange(List, 5000, 10000);

    delFirst(List);
    delLast(List);
    delAfter(List, nodeD, nodeC);

    cout << "--- ISI LIST SETELAH DILAKUKAN DELETE ---" << endl;
    printList(List);
    cout << "jumlah node : " << nbList(List) << endl;
    cout << endl;

    deleteList(List);
    cout << "--- ISI LIST SETELAH DILAKUKAN HAPUS LIST ---" << endl;
    printList(List);
    cout << "jumlah node : " << nbList(List) << endl;
    cout << endl;

    return 0;
}
```

Kode ini berfungsi untuk mengelola data buah menggunakan singly linked list dalam C++. Struktur `buah` menyimpan nama, jumlah, dan harga, sedangkan `linkedlist` menyimpan pointer ke elemen pertama. Fungsi-fungsi dalam `listBuah.cpp` digunakan untuk membuat list, menambah, menghapus, memperbarui, dan mencari data buah. Pada `main.cpp`, beberapa data buah ditambahkan menggunakan fungsi insert, lalu dilakukan operasi update, pencarian, dan penghapusan. Program ini menunjukkan cara pengelolaan data dinamis secara fleksibel menggunakan konsep linked list.

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




### 3. [Soal]
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
address findElm(List L, infotype x);
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

address findElm(List L, infotype x) {
    address P = L.first;
    while (P != Nil && P->info != x) {
        P = P->next;
    }
    return P;
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

    address cari = findElm(L, 8);
       if (cari != Nil) {
            cout << "Elemen info ditemukan : " << cari->info << endl;
        } else {
            cout << "Elemen dengan info 8 tidak ditemukan." << endl;
    }
    return 0;
}
```
#### Output:
<img width="737" height="163" alt="image" src="https://github.com/user-attachments/assets/30bf8bb7-4a91-4353-8f44-11cb0c21f7d1" />

Program ini menambahkan fungsi totalInfo() untuk menghitung jumlah seluruh nilai info pada setiap node di dalam linked list. Prosesnya dilakukan dengan menelusuri seluruh elemen dan menjumlahkan nilainya satu per satu. Hasil akhir perhitungan dari data 9 + 12 + 8 + 0 + 2 menghasilkan total 31. Fungsi ini menunjukkan penerapan perulangan dalam pengolahan data dinamis menggunakan pointer.

#### Full code Screenshot:
<img width="510" height="586" alt="image" src="https://github.com/user-attachments/assets/f50e4f59-314b-44b5-9be1-be73e4fcfcc5" />
<img width="603" height="806" alt="image" src="https://github.com/user-attachments/assets/8d406e73-facb-4111-a8ee-6167060d2151" />
<img width="653" height="672" alt="image" src="https://github.com/user-attachments/assets/cbd4209f-ffea-4f6a-9d8b-ee38f310be84" />

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
address findElm(List L, infotype x);
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

address findElm(List L, infotype x) {
    address P = L.first;
    while (P != Nil && P->info != x) {
        P = P->next;
    }
    return P;
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

    address cari = findElm(L, 8);
       if (cari != Nil) {
            cout << "Elemen info ditemukan : " << cari->info << endl;
        } else {
            cout << "Elemen dengan info 8 tidak ditemukan." << endl;
    }
    return 0;
}
```
#### Output:
<img width="715" height="157" alt="Screenshot 2025-10-29 195147" src="https://github.com/user-attachments/assets/f808d174-7ab1-4571-a4bc-a257a49c18b2" />

Program ini menambahkan fungsi findElm() yang digunakan untuk mencari node berdasarkan nilai tertentu pada linked list. Fungsi ini menelusuri setiap node dari awal hingga akhir untuk menemukan elemen dengan nilai yang dicari, misalnya 8. Jika ditemukan, program akan menampilkan alamat dan nilai elemen tersebut. Konsep ini menunjukkan bagaimana operasi sequential search diterapkan pada struktur data dinamis seperti linked list.

#### Full code Screenshot:

## Kesimpulan
Kesimpulan dari ketiga program di atas adalah bahwa semuanya menerapkan konsep struktur data dinamis menggunakan **singly linked list** dalam bahasa C++. Program pertama berfokus pada pembuatan dan penambahan elemen ke dalam list, program kedua menambahkan fitur pencarian elemen serta perhitungan total nilai, sedangkan program ketiga mengembangkan fungsi-fungsi seperti pembaruan dan pencarian data berdasarkan kriteria tertentu. Dari ketiganya dapat disimpulkan bahwa linked list memungkinkan pengelolaan data secara fleksibel tanpa batasan ukuran seperti array, karena elemen dapat ditambah atau diubah dengan mudah. Pemahaman terhadap pointer dan manajemen memori sangat penting agar proses manipulasi data dalam struktur dinamis ini berjalan dengan benar dan efisien.

## Referensi
[1] GeeksforGeeks. (n.d.). C++ Program for Deleting a Node in a Linked List. Diakses pada 23 Oktober 2025, dari https://www.geeksforgeeks.org/cpp/cpp-program-for-deleting-a-node-in-a-linked-list/
[2] GeeksforGeeks. (n.d.). C++ Program For Searching An Element In A Linked List. Retrieved from https://www.geeksforgeeks.org/cpp-program-for-searching-an-element-in-a-linked-list/
[3] GeeksforGeeks. (n.d.). Sum of the nodes of a Singly Linked List. Retrieved from https://www.geeksforgeeks.org/dsa/sum-of-the-nodes-of-a-singly-linked-list/


