# <h1 align="center">Laporan Praktikum Modul Multilinkedlist </h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori
Tree adalah struktur data non-linear yang terdiri dari node-node yang tersusun secara hierarki. Binary Tree merupakan tree yang setiap node-nya memiliki maksimal dua child, yaitu left dan right. Binary Search Tree (BST) adalah binary tree terurut dengan aturan bahwa node pada subtree kiri bernilai lebih kecil dari parent, sedangkan node pada subtree kanan bernilai lebih besar. Dengan aturan ini, proses pencarian dan penyisipan data dapat dilakukan secara efisien menggunakan metode rekursif.
## Guided 

### 1. [Multilinkedlist]
```C++
/* buat dahulu elemen yang akan disisipkan */ 
address_anak alokasiAnak(infotypeanak X){
    address_anak P = alokasi(X); 
    P→next = Nil; 
    P→prev = Nil; 
    return P; 
} 
/* mencari apakah ada elemen pegawai dengan info X */ 
address findElm(listinduk L, infotypeinduk X){ 
    address cariInduk = L.first; 
    do{ 
        if(cariInduk.info == X){ 
            return cariInduk; 
        }else{ 
            cariInduk = cariInduk→next; 
}  
    }while(cariInduk.info != X || cariInduk != L→last) 
} 
/* menyisipkan anak pada akhir list anak */ 
void insertLastAnak(listanak &Lanak, address_anak P){ 
    address_anak ! = head(&Lanak); 
    do{ 
        Q = Q→next; 
    }while(next(&Lanak)!=Nil) 
    Q→next = P; 
    P→prev = Q; 
    P→next = Nil; 
}
```
*multilist.h*
```C++
/* contoh ADT list berkait dengan representasi fisik pointer*/ 
/* representasi address dengan pointer*/ 
 
/* info tipe adalah integer */ 
#ifndef MULTILIST_H_INCLUDED 
#define MULTILIST_H_INCLUDED 
#define Nil NULL 
 
typedef int infotypeanak; 
typedef int infotypeinduk; 
typedef struct elemen_list_induk *address; 
typedef struct elemen_list_anak *address_anak; 
/* define list : */ 
 
/* list kosong jika L.first=Nil 
setiap elemen address P dapat diacu P→info atau P→next 
elemen terakhir list jika addressnya last, maka L.last = Nil */ 
struct elemen_list_anak{ 
/* struct ini untuk menyimpan elemen anak dan pointer penunjuk 
   elemen tetangganya */ 
     infotypeanak info; 
     address_anak next; 
     address_anak prev; 
}; 
 
struct listanak { 
/* struct ini digunakan untuk menyimpan list anak itu sendiri */ 
   address_anak first; 
   address_anak last; 
}; 
 
struct elemen_list_induk{ 
/* struct ini untuk menyimpan elemen induk dan pointer penunjuk 
   elemen tetangganya */
      infotypeanak info; 
      listanak lanak;
      address next; 
      address prev; 
}; 
struct listinduk { 
/* struct ini digunakan untuk menyimpan list induk itu sendiri */ 
  address first;
  address last;
}; 
 
/********* pengecekan apakah list kosong ***********/ 
boolean ListEmpty(listinduk L); 
/*mengembalikan nilai true jika list induk kosong*/ 
boolean ListEmptyAnak(listanak L); 
/*mengembalikan nilai true jika list anak kosong*/ 
 
/********* pembuatan list kosong *********/ 
void CreateList(listinduk &L); 
/* I.S. sembarang 
   F.S. terbentuk list induk kosong*/ 
void CreateListAnak(listanak &L); 
/* I.S. sembarang 
   F.S. terbentuk list anak kosong*/ 
    
/********* manajemen memori *********/ 
address alokasi(infotypeinduk P); 
/* mengirimkan address dari alokasi sebuah elemen induk 
   jika alokasi berhasil, maka nilai address tidak Nil dan jika gagal 
   nilai address Nil */ 
    
address_anak alokasiAnak(infotypeanak P); 
/* mengirimkan address dari alokasi sebuah elemen anak 
   jika alokasi berhasil, maka nilai address tidak Nil dan jika gagal 
   nilai address_anak Nil */ 
    
void dealokasi(address P); 
/* I.S. P terdefinisi 
   F.S. memori yang digunakan P dikembalikan ke sistem */ 
 
void dealokasiAnak(address_anak P); 
/* I.S. P terdefinisi 
   F.S. memori yang digunakan P dikembalikan ke sistem */    
/********* pencarian sebuah elemen list *********/ 
address findElm(listinduk L, infotypeinduk X); 
/* mencari apakah ada elemen list dengan P→info = X 
   jika ada, mengembalikan address elemen tab tsb, dan Nil jika sebaliknya 
*/ 
address_anak findElm(listanak Lanak, infotypeanak X); 
/* mencari apakah ada elemen list dengan P→info = X 
   jika ada, mengembalikan address elemen tab tsb, dan Nil jika sebaliknya 
*/ 
boolean fFindElm(listinduk L, address P); 
/* mencari apakah ada elemen list dengan alamat P 
   mengembalikan true jika ada dan false jika tidak ada */ 
boolean fFindElmanak(listanak Lanak, address_anak P); 
/* mencari apakah ada elemen list dengan alamat P 
   mengembalikan true jika ada dan false jika tidak ada */ 
 
address findBefore(listinduk L, address P); 
/* mengembalikan address elemen sebelum P 
   jika P berada pada awal list, maka mengembalikan nilai Nil */ 
address_anak findBeforeAnak(listanak Lanak, infotypeinduk X, address_anak 
P); 
/* mengembalikan address elemen sebelum P dimana P→info = X 
   jika P berada pada awal list, maka mengembalikan nilai Nil */ 
    
/********* penambahan elemen **********/ 
void insertFirst(listinduk &L, address P); 
/* I.S. sembarang, P sudah dialokasikan 
   F.S. menempatkan elemen beralamat P pada awal list */ 
    
void insertAfter(listinduk &L, address P, address Prec); 
/* I.S. sembarang, P dan Prec alamt salah satu elemen list 
   F.S. menempatkan elemen beralamat P sesudah elemen beralamat Prec */
void insertLast(listinduk &L, address P); 
/* I.S. sembarang, P sudah dialokasikan 
   F.S. menempatkan elemen beralamat P pada akhir list */ 
    
void insertFirstAnak(listanak &L, address_anak P); 
/* I.S. sembarang, P sudah dialokasikan 
   F.S. menempatkan elemen beralamat P pada awal list */ 
    
void insertAfterAnak(listanak &L, address_anak P, address_anak Prec); 
/* I.S. sembarang, P dan Prec alamt salah satu elemen list 
   F.S. menempatkan elemen beralamat P sesudah elemen beralamat Prec */ 
 
void insertLastAnak(listanak &L, address_anak P); 
/* I.S. sembarang, P sudah dialokasikan 
   F.S. menempatkan elemen beralamat P pada akhir list */ 
    
/********* penghapusan sebuah elemen *********/ 
void delFirst(listinduk &L, address &P); 
/* I.S. list tidak kosong 
   F.S. adalah alamat dari alamat elemen pertama list 
   sebelum elemen pertama list dihapus 
   elemen pertama list hilang dan list mungkin menjadi kosong 
   first elemen yang baru adalah successor first elemen yang lama */ 
void delLast(listinduk &L, address &P); 
/* I.S. list tidak kosong 
   F.S. adalah alamat dari alamat elemen terakhir list 
   sebelum elemen terakhir list dihapus 
   elemen terakhir list hilang dan list mungkin menjadi kosong 
   last elemen yang baru adalah successor last elemen yang lama */ 
 
void delAfter(listinduk &L, address &P, address Prec); 
/* I.S. list tidak kosng, Prec alamat salah satu elemen list 
   F.S. P adalah alamatdari Prec→next, menghapus Prec→next dari list */ 
void delP (listinduk &L, infotypeinduk X); 
/* I.S. sembarang 
   F.S. jika ada elemen list dengan alamat P, dimana P→info = X,  
        maka P dihapus dan P di-dealokasi,  
        jika tidak ada maka list tetap list mungkin akan menjadi kosong  
        karena penghapusan */ 
   
void delFirstAnak(listanak &L, address_anak &P); 
/* I.S. list tidak kosong 
   F.S. adalah alamat dari alamat elemen pertama list 
   sebelum elemen pertama list dihapus 
   elemen pertama list hilang dan list mungkin menjadi kosong 
   first elemen yang baru adalah successor first elemen yang lama */ 
void delLastAnak(listanak &L, address_anak &P); 
/* I.S. list tidak kosong 
   F.S. adalah alamat dari alamat elemen terakhir list 
   sebelum elemen terakhir list dihapus 
   elemen terakhir list hilang dan list mungkin menjadi kosong 
   last elemen yang baru adalah successor last elemen yang lama */ 
 
void delAfterAnak(listanak &L, address_anak &P, address_anak Prec); 
/* I.S. list tidak kosng, Prec alamat salah satu elemen list 
   F.S. P adalah alamatdari Prec→next, menghapus Prec→next dari list */ 
void delPAnak (listanak &L, infotypeanak X); 
/* I.S. sembarang 
   F.S. jika ada elemen list dengan alamat P, dimana P→info = X,  
        maka P dihapus dan P di-dealokasi,  
        jika tidak ada maka list tetap list mungkin akan menjadi kosong  
        karena penghapusan */ 
/********** proses semau elemen list *********/ 
void printInfo(list L); 
/* I.S. list mungkin kosong 
   F.S. jika list tidak kosong menampilkan semua info yang ada pada list 
*/ 

int nbList(list L); 
/* mengembalikan jumlah elemen pada list */ 
 
void printInfoAnak(listanak Lanak); 
/* I.S. list mungkin kosong 
   F.S. jika list tidak kosong menampilkan semua info yang ada pada list 
*/ 
 
int nbListAnak(listanak Lanak); 
/* mengembalikan jumlah elemen pada list anak */ 
 
/********** proses terhadap list **********/ 
void delAll(listinduk &L); 
/* menghapus semua elemen list dan semua elemen di-dealokasi */ 
#endif
```
Kode tersebut merupakan bagian dari implementasi Multi Linked List yang terdiri dari list induk dan list anak. Fungsi alokasiAnak digunakan untuk mengalokasikan memori elemen anak dan menginisialisasi pointer next dan prev agar belum terhubung dengan elemen lain. Fungsi findElm berfungsi mencari elemen induk berdasarkan nilai info dengan melakukan penelusuran dari elemen pertama hingga akhir list. Prosedur insertLastAnak digunakan untuk menambahkan elemen anak pada posisi terakhir list anak milik suatu induk, sehingga hubungan antar elemen anak tetap terjaga dengan benar.

## Unguided 

### 1. [Soal]
*circularist.h*
```C++
#ifndef CIRCULARLIST_H
#define CIRCULARLIST_H

#include <iostream>
#include <string>
using namespace std;

#define Nil NULL

typedef struct mahasiswa {
    string nama;
    string nim;
    char jenis_kelamin;
    float ipk;
} infotype;

typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
    address prev;
};

struct List {
    address first;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);

void insertFirst(List &L, address P);
void insertLast(List &L, address P);
void insertAfter(List &L, address Prec, address P);

void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);

address findElm(List L, infotype x);
void printInfo(List L);

#endif
```
*circularlist.cpp*
```C++
#include "circularlist.h"

void createList(List &L) {
    L.first = Nil;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = P;
    P->prev = P;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = Nil;
}

void insertFirst(List &L, address P) {
    if (L.first == Nil) {
        L.first = P;
    } else {
        address last = L.first->prev;
        P->next = L.first;
        P->prev = last;
        last->next = P;
        L.first->prev = P;
        L.first = P;
    }
}

void insertLast(List &L, address P) {
    if (L.first == Nil) {
        L.first = P;
    } else {
        address last = L.first->prev;
        P->next = L.first;
        P->prev = last;
        last->next = P;
        L.first->prev = P;
    }
}

void insertAfter(List &L, address Prec, address P) {
    P->next = Prec->next;
    P->prev = Prec;
    Prec->next->prev = P;
    Prec->next = P;
}

void deleteFirst(List &L, address &P) {
    if (L.first != Nil) {
        P = L.first;
        if (P->next == P) {
            L.first = Nil;
        } else {
            address last = P->prev;
            L.first = P->next;
            last->next = L.first;
            L.first->prev = last;
        }
        P->next = P->prev = Nil;
    }
}

void deleteLast(List &L, address &P) {
    if (L.first != Nil) {
        address last = L.first->prev;
        P = last;
        if (last == L.first) {
            L.first = Nil;
        } else {
            last->prev->next = L.first;
            L.first->prev = last->prev;
        }
        P->next = P->prev = Nil;
    }
}

void deleteAfter(List &L, address Prec, address &P) {
    P = Prec->next;
    Prec->next = P->next;
    P->next->prev = Prec;
    P->next = P->prev = Nil;
}

address findElm(List L, infotype x) {
    if (L.first == Nil) return Nil;
    address P = L.first;
    do {
        if (P->info.nim == x.nim)
            return P;
        P = P->next;
    } while (P != L.first);
    return Nil;
}

void printInfo(List L) {
    if (L.first != Nil) {
        address P = L.first;
        do {
            cout << "Nama : " << P->info.nama << endl;
            cout << "NIM  : " << P->info.nim << endl;
            cout << "L/P  : " << P->info.jenis_kelamin << endl;
            cout << "IPK  : " << P->info.ipk << endl << endl;
            P = P->next;
        } while (P != L.first);
    }
}
```
*main.cpp*
```C++
#include "circularlist.h"

address createData(string nama, string nim, char jenis_kelamin, float ipk) {
    infotype x;
    address P;

    x.nama = nama;
    x.nim = nim;
    x.jenis_kelamin = jenis_kelamin;
    x.ipk = ipk;

    P = alokasi(x);
    return P;
}

int main() {
    List L;
    address P1 = Nil;
    address P2 = Nil;
    infotype x;

    createList(L);

    cout << "coba insert first, last, dan after" << endl;

    P1 = createData("Danu", "04", 'l', 4.0);
    insertFirst(L, P1);

    P1 = createData("Fahmi", "06", 'l', 3.45);
    insertLast(L, P1);

    P1 = createData("Bobi", "02", 'l', 3.71);
    insertFirst(L, P1);

    P1 = createData("Ali", "01", 'l', 3.3);
    insertFirst(L, P1);

    P1 = createData("Gita", "07", 'p', 3.75);
    insertLast(L, P1);

    x.nim = "07";
    P1 = findElm(L, x);
    P2 = createData("Cindi", "03", 'p', 3.5);
    insertAfter(L, P1, P2);

    x.nim = "04";
    P1 = findElm(L, x);
    P2 = createData("Eli", "05", 'p', 3.4);
    insertAfter(L, P1, P2);

    P2 = createData("Hilmi", "08", 'p', 3.3);
    insertLast(L, P2);

    printInfo(L);
    return 0;
}
```
#### Output:
<img width="718" height="855" alt="image" src="https://github.com/user-attachments/assets/2273a7a4-2bb7-41f8-a746-709c662588dd" />

Program mengimplementasikan ADT Circular Doubly Linked List untuk menyimpan data mahasiswa yang terdiri dari nama, NIM, jenis kelamin, dan IPK. Operasi yang digunakan meliputi pembuatan list, alokasi memori, penyisipan data di awal, akhir, dan setelah node tertentu, pencarian data berdasarkan NIM, serta penampilan seluruh isi list. Program diuji menggunakan beberapa data mahasiswa dan menghasilkan urutan data sesuai dengan ilustrasi pada modul.

#### Full code Screenshot:
<img width="536" height="941" alt="image" src="https://github.com/user-attachments/assets/70f30b5e-3ff3-4cb5-a5fd-11deefbe636e" />
<img width="519" height="921" alt="image" src="https://github.com/user-attachments/assets/9374af0c-c498-4dc3-89dc-358a4ad97082" />
<img width="592" height="873" alt="image" src="https://github.com/user-attachments/assets/e29b1fdb-03d9-4cad-9dab-63f0c5957193" />
<img width="624" height="497" alt="image" src="https://github.com/user-attachments/assets/f7e20407-4b56-4405-8015-bee0ebed6d77" />
<img width="555" height="875" alt="image" src="https://github.com/user-attachments/assets/e6ccdf4c-0fee-4524-8f10-682103fbe4f1" />

## Kesimpulan
Berdasarkan hasil pengujian, implementasi Circular Doubly Linked List telah berjalan dengan baik. Seluruh fungsi dapat dijalankan sesuai tujuan, dan struktur circular berhasil menjaga keterhubungan antar node sehingga data dapat diakses secara berurutan tanpa kesalahan.

## Referensi
[1] Modul Struktur Data: Multi Linked List. Fakultas Informatika.
[2] GeeksforGeeks. (2023). Circular Doubly Linked List. https://www.geeksforgeeks.org/circular-doubly-linked-list/
