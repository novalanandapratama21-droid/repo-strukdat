*Soal 1*

*SLLInventory.h*
```C++
#ifndef SLLInventory_H
#define SLLInventory_H
#define Nil NULL

#include <iostream>
using namespace std;

struct product{
    string Nama;
    string SKU;
    int Jumlah;
    float HargaSatuan;
    float DiskonPersen;
};

typedef product dataProduct;

typedef struct node *address;

struct node{
    dataProduct info;
    address next;
};

struct List{
    address head;
};

bool isEmpty(List list );
void createList(List &L);
address allocate(product P);
void deallocate(address addr);
void insertFirst(List &L, address P);
void insertLast(List &L, address P);
void insertAfter(List &L, address Prec, address P);
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);
void updateAtPosition(List &L, int position);
void viewList(List L);
void searchByPriceRange(List L, float minPrice, float maxPrice);
void hargaAkhir(List L, float &totalHarga);
#endif
```
*list.cpp*
```C++
#include "SLLInventory.h"
#include <iostream>
using namespace std;
bool isEmpty(List list ) {
    return list.head == Nil;
}
void createList(List &L) {
    L.head = Nil;
}
address allocate(product P) {
    address addr = new node;
    addr->info = P;
    addr->next = Nil;
    return addr;
}
void deallocate(address addr) {
    delete addr;
}
void insertFirst(List &L, address P) {
    P->next = L.head;
    L.head = P;
}
void insertLast(List &L, address P) {
    if (isEmpty(L)) {
        L.head = P;
    } else {
        address temp = L.head;
        while (temp->next != Nil) {
            temp = temp->next;
        }
        temp->next = P;
    }
}
void insertAfter(List &L, address Prec, address P) {
    if (Prec != Nil) {
        P->next = Prec->next;
        Prec->next = P;
    }
}

void deleteFirst(List &L, address &P) {
    if (L.head != Nil) {
        P = L.head;
        L.head = P->next;
        P->next = Nil;
    
    }
}
void deleteLast(List &L, address &P) {
    if (L.head == Nil) {
        P = Nil;
    } else if (L.head->next == Nil) {
        P = L.head;
        L.head = Nil;
    } else {
        address temp = L.head;
        while (temp->next->next != Nil) {
            temp = temp->next;
        }
        P = temp->next;
        temp->next = Nil;
    }  
}
void deleteAfter(List &L, address Prec, address &P) {
    if (Prec != Nil && Prec->next != Nil) {
        P = Prec->next;
        Prec->next = P->next;
        P->next = Nil;
    }
}

void viewList(List L) {
    address temp = L.head;
    while (temp != Nil) {
        cout << "------------------------" << endl;
        cout << "Nama: " << temp->info.Nama << endl;
        cout << "SKU: " << temp->info.SKU << endl;
        cout << "Jumlah: " << temp->info.Jumlah << endl;
        cout << "Harga Satuan: " << temp->info.HargaSatuan << endl;
        cout << "Diskon Persen: " << temp->info.DiskonPersen << endl;
        temp = temp->next;
        cout << "------------------------" << endl;
    }
}  

void searchByPriceRange(List L, float minPrice, float maxPrice) {
    address temp = L.head;
    bool found = false;
    while (temp != Nil) {
        if (temp->info.HargaSatuan >= minPrice && temp->info.HargaSatuan <= maxPrice) {
            cout << "Nama: " << temp->info.Nama << ", SKU: " << temp->info.SKU
                 << ", Jumlah: " << temp->info.Jumlah << ", Harga Satuan: " << temp->info.HargaSatuan
                 << ", Diskon Persen: " << temp->info.DiskonPersen << "%" << endl;
            found = true;
        }
        temp = temp->next;
    }
    if (!found) {
        cout << "No products found in the price range " << minPrice << " to " << maxPrice << "." << endl;
    }
}

void updateAtPosition(List &L, int position) {
    if (position < 1) {
        cout << "Invalid position!" << endl;
        return;
    }
    address temp = L.head;
    int currentPos = 1;
    while (temp != Nil && currentPos < position) {
        temp = temp->next;
        currentPos++;
    }
    if (temp == Nil) {
        cout << "Position exceeds list length!" << endl;
        return;
    }
    cout << "Updating product at position " << position << ":" << endl;
    cout << "Masukan Nama Baru: ";
    cin >> temp->info.Nama;
    cout << "Masukan SKU Baru: ";
    cin >> temp->info.SKU;
    cout << "Masukan Jumlah Baru: ";
    cin >> temp->info.Jumlah;
    cout << "Masukan Harga Satuan Baru: ";
    cin >> temp->info.HargaSatuan;
    cout << "Masukan Diskon Persen Baru: ";
    cin >> temp->info.DiskonPersen;
}

void hargaAkhir(List L, float &totalHarga) {
    totalHarga = 0.0;
    address temp = L.head;
    while (temp != Nil) {
        float hargaSetelahDiskon = temp->info.HargaSatuan * (1 - temp->info.DiskonPersen / 100);
        totalHarga += hargaSetelahDiskon * temp->info.Jumlah;
        temp = temp->next;
    }
}
```
*main.cpp*
```C++
#include "SLLInventory.h"
#include <iostream>
using namespace std;

int main() {
    List inventory;
    createList(inventory);
    product prod1 = {"Pulpen", "A001", 20, 2500.0, 0.0};
    product prod2 = {"Buku Tulis", "A002", 15, 5000.0, 10.0};
    product prod3 = {"Penghapus", "A003", 30, 1500.0, 0.0};

    address addr1 = allocate(prod1);
    address addr2 = allocate(prod2);
    address addr3 = allocate(prod3);
    insertFirst(inventory, addr1);
    insertLast(inventory, addr2);
    insertAfter(inventory, addr1, addr3);
    cout << "--- Inventory List ---" << endl;
    viewList(inventory);
   
    deleteFirst(inventory, addr1);
    deallocate(addr1);
    cout << "--- Inventory List after deleting first item ---" << endl;
    viewList(inventory);

    updateAtPosition(inventory, 2);
    cout << "--- Inventory List after updating item at position 2---" << endl;
    viewList(inventory);

    searchByPriceRange(inventory, 2000.0, 7000.0);
    return 0;
}
```

Screenshoots
<img width="840" height="1012" alt="image" src="https://github.com/user-attachments/assets/da0a0bdb-86ae-4f53-bde0-700ffd31482c" />
<img width="647" height="1014" alt="image" src="https://github.com/user-attachments/assets/52b34693-6d5a-42a0-9b3b-31292ff59c3f" />

