# <h1 align="center">Laporan Praktikum Modul Tree </h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori
Tree adalah struktur data non-linear yang terdiri dari node-node yang tersusun secara hierarki. Binary Tree merupakan tree yang setiap node-nya memiliki maksimal dua child, yaitu left dan right. Binary Search Tree (BST) adalah binary tree terurut dengan aturan bahwa node pada subtree kiri bernilai lebih kecil dari parent, sedangkan node pada subtree kanan bernilai lebih besar. Dengan aturan ini, proses pencarian dan penyisipan data dapat dilakukan secara efisien menggunakan metode rekursif.
## Guided 

### 1. [Queue]
*queue.h*
```C++
#ifndef QUEUE_H
#define QUEUE_H

#include<iostream>
using namespace std;

const int MAKSIMAL = 5;

struct queue{
    string nama[MAKSIMAL];
    int head;
    int tail;
};

bool isFull(queue Q);
bool isEmpty(queue Q);
void CreateQueue(queue &Q); //terbentuk queue dengan head = -1 dan tail = -1 
void enQueue(queue &Q, string nama);
void deQueue(queue &Q);
void viewQueue(queue Q);

#endif
```
*queue.cpp*
```C++
#include "queue.h"
#include <iostream>

using namespace std;

// NOTE : 
// Implementasi 1 = head diam, tail bergerak (Queue Linear Statis, kerana head nya tetap diam)
// Implementasi 2 = head bergerak, tail bergerak (Queue Linear Dinamis, karena head & tail nya sama-sama bergerak)
// Implementasi 3 = head dan tail berputar (Queue Circular, karena jika udh mentok tapi masih ada space, diputar sehingga tail bisa ada didepan head)

bool isEmpty(queue Q){
    if(Q.head == -1 && Q.tail == -1){
        return true;
    } else {
        return false;
    }
}

// //isFull implmenetasi 1 & 2
// bool isFull(queue Q){
//     if(Q.tail == MAKSIMAL - 1){
//         return true;
//     } else {
//         return false;
//     }
// }

//isFull implementasi 3
bool isFull(queue Q){
    if((Q.tail + 1) % MAKSIMAL == Q.head){
        return true;
    } else {
        return false;
    }
}

void CreateQueue(queue &Q){ //terbentuk queue dengan head = -1 dan tail = -1 
    Q.head = -1;
    Q.tail = -1;
}
 
// //enqueue implementasi 1 & 2
// void enQueue(queue &Q, string nama){
//     if(isFull(Q) == true){
//         cout << "Queue sudah penuh!" << endl;
//     } else {
//         if(isEmpty(Q) == true){
//             Q.head = Q.tail = 0;
//         } else {
//             Q.tail++;
//         }
//         Q.nama[Q.tail] = nama;
//         cout << "nama " << nama << " berhasil ditambahkan kedalam queue!" << endl;
//     }
// }

//enQueue implementasi 3
void enQueue(queue &Q, string nama){
    if(isFull(Q) == true){
        cout << "Queue sudah penuh!" << endl;
    } else {
        if(isEmpty(Q) == true){
            Q.head = Q.tail = 0;
        } else {
            Q.tail = (Q.tail + 1) % MAKSIMAL; // bergerak melingkar
        }
        Q.nama[Q.tail] = nama;
        cout << "nama " << nama << " berhasil ditambahkan kedalam queue!" << endl;
    }
}

// //dequeue implementasi 1
// void deQueue(queue &Q){
//     if(isEmpty(Q) == true){
//         cout << "Queue kosong!" << endl;
//     } else {
//         cout << "Mengahapus data " << Q.nama[Q.head] << "..." << endl;
//         for(int i = 0; i < Q.tail; i++){
//             Q.nama[i] =  Q.nama[i+1];
//         }
//         Q.tail--;
//         if(Q.tail < 0){ //kalo semua isi queue nya udh dikelaurin, set head & tail ke -1
//             Q.head = -1;
//             Q.tail = -1;
//         }
//     }
// }

// //dequeue implementasi 2
// void deQueue(queue &Q){
//     if(isEmpty(Q) == true){
//         cout << "Queue kosong!" << endl;
//     } else {
//         cout << "Mengahapus data " << Q.nama[Q.head] << "..." << endl;
//         Q.head++;
//         if(Q.head > Q.tail){ //kalo elemennya udh abis (head akan lebih 1 dari tail), maka reset ulang head & tail ke -1
//             Q.head = -1;
//             Q.tail = -1;
//         }
//     }
// }

//deQueue implementasi 3
void deQueue(queue &Q){
    if(isEmpty(Q) == true){
        cout << "Queue kosong!" << endl;
    } else {
        cout << "Mengahapus data " << Q.nama[Q.head] << "..." << endl;
        if(Q.head == Q.tail){ //kalo elemennya tinggal 1, langsungkan saja head & tail nya reset ke -1
            Q.head = -1;
            Q.tail = -1;
        } else {
            Q.head = (Q.head + 1) % MAKSIMAL; // bergerak melingkar
        }
    }
}

// //viewQueue implementasi 1 & 2
// void viewQueue(queue Q){
//     if(isEmpty(Q) == true){
//         cout << "Queue kosong!" << endl;
//     } else {
//         for(int i = Q.head; i <= Q.tail; i++){
//             cout << i -  Q.head + 1 << ". " << Q.nama[i] << endl;
//         }
//     }
//     cout << endl;
// }

//viewQueue implementasi 3
void viewQueue(queue Q){
    if(isEmpty(Q) == true){
        cout << "Queue kosong!" << endl;
    } else {
        int i = Q.head;
        int count = 1;
        while(true){
            cout << count << ". " << Q.nama[i] << endl;
            if(i == Q.tail){
                break;
            }
            i = (i + 1) % MAKSIMAL;
            count++;
        }   
    }
}
```
*main.cpp*
```C++
#include "queue.h"
#include <iostream>

using namespace std;

int main(){
    queue Q;

    CreateQueue(Q);
    enQueue(Q, "dhimas");
    enQueue(Q, "Arvin");
    enQueue(Q, "Rizal");
    enQueue(Q, "Hafizh");
    enQueue(Q, "Fathur");
    enQueue(Q, "Atha");
    cout << endl;

    cout << "--- Isi Queue Setelah enQueue ---" << endl;
    viewQueue(Q);

    deQueue(Q);
    deQueue(Q);
    deQueue(Q);
    deQueue(Q);
    // deQueue(Q);
    // deQueue(Q);
    cout << endl;

    cout << "--- Isi Queue Setelah deQueue ---" << endl;
    viewQueue(Q);

    return 0;
}
```

Program ini menerapkan ADT Queue menggunakan array dengan mekanisme circular queue. Posisi head dan tail digunakan untuk mengatur elemen terdepan dan terakhir pada queue. Proses enQueue menambahkan data pada tail dengan pergerakan melingkar, sedangkan deQueue menghapus data pada head dan menggeser posisinya secara melingkar. Dengan mekanisme ini, seluruh ruang array dapat dimanfaatkan secara optimal dan urutan data tetap mengikuti prinsip FIFO.

## Unguided 

### 1. [Soal]
*bstree.h*
```C++
#ifndef BSTREE_H
#define BSTREE_H

#define Nil NULL

typedef int infotype;
typedef struct Node* address;

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);

void insertNode(address &root, infotype x);
address findNode(infotype x, address root);

void InOrder(address root);

#endif
```
*bstree.cpp*
```C++
#include <iostream>
#include "bstree.h"

using namespace std;

address alokasi(infotype x) {
    address P = new Node;
    if (P != Nil) {
        P->info = x;
        P->left = Nil;
        P->right = Nil;
    }
    return P;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else {
        if (x < root->info) {
            insertNode(root->left, x);
        } else if (x > root->info) {
            insertNode(root->right, x);
        }
    }
}

address findNode(infotype x, address root) {
    if (root == Nil) {
        return Nil;
    } else if (x == root->info) {
        return root;
    } else if (x < root->info) {
        return findNode(x, root->left);
    } else {
        return findNode(x, root->right);
    }
}

void InOrder(address root) {
    if (root != Nil) {
        InOrder(root->left);
        cout << root->info << " - ";
        InOrder(root->right);
    }
}
```
*main.cpp*
```C++
#include <iostream>
#include "bstree.h"

using namespace std;

int main() {
    cout << "Hello World!" << endl;

    address root = Nil;

    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6);
    insertNode(root, 7);

    InOrder(root);

    return 0;
}
```
#### Output:
<img width="781" height="152" alt="image" src="https://github.com/user-attachments/assets/3441b4e5-8abe-48e9-a161-89327c242939" />

Program ini mengimplementasikan ADT Binary Search Tree menggunakan linked list. Struktur Node terdiri dari elemen info, left, dan right. Fungsi alokasi digunakan untuk membuat node baru. Fungsi insertNode menyisipkan data ke dalam tree secara rekursif sesuai aturan BST. Fungsi findNode digunakan untuk mencari data dalam tree, sedangkan fungsi InOrder menampilkan isi tree dengan metode inorder sehingga data ditampilkan dalam urutan menaik.

#### Full code Screenshot:
<img width="488" height="566" alt="image" src="https://github.com/user-attachments/assets/3c2e57a4-ab1b-42e9-99e0-d8df7b2bb87c" />
<img width="568" height="1003" alt="image" src="https://github.com/user-attachments/assets/8e246990-c339-4d3e-8fa2-fb5c79c7f871" />
<img width="450" height="570" alt="image" src="https://github.com/user-attachments/assets/dd498d49-093d-4552-bd50-b88b43eee5d8" />

### 2. [Soal]
*bstree.h*
```C++
#ifndef BSTREE_H
#define BSTREE_H

#define Nil NULL

typedef int infotype;
typedef struct Node* address;

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);

void insertNode(address &root, infotype x);
address findNode(infotype x, address root);

void InOrder(address root);

#endif
```
*bstree.cpp*
```C++
#include <iostream>
#include "bstree.h"

using namespace std;

address alokasi(infotype x) {
    address P = new Node;
    if (P != Nil) {
        P->info = x;
        P->left = Nil;
        P->right = Nil;
    }
    return P;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else {
        if (x < root->info) {
            insertNode(root->left, x);
        } else if (x > root->info) {
            insertNode(root->right, x);
        }
    }
}

address findNode(infotype x, address root) {
    if (root == Nil) {
        return Nil;
    } else if (x == root->info) {
        return root;
    } else if (x < root->info) {
        return findNode(x, root->left);
    } else {
        return findNode(x, root->right);
    }
}

void InOrder(address root) {
    if (root != Nil) {
        InOrder(root->left);
        cout << root->info << " - ";
        InOrder(root->right);
    }
}
```
*main.cpp*
```C++
#include <iostream>
#include "bstree.h"

using namespace std;

int main() {
    cout << "Hello World!" << endl;

    address root = Nil;

    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6);
    insertNode(root, 7);

    InOrder(root);

    return 0;
}
```
#### Output:
<img width="781" height="152" alt="image" src="https://github.com/user-attachments/assets/3441b4e5-8abe-48e9-a161-89327c242939" />

Program ini mengimplementasikan ADT Binary Search Tree menggunakan linked list. Struktur Node terdiri dari elemen info, left, dan right. Fungsi alokasi digunakan untuk membuat node baru. Fungsi insertNode menyisipkan data ke dalam tree secara rekursif sesuai aturan BST. Fungsi findNode digunakan untuk mencari data dalam tree, sedangkan fungsi InOrder menampilkan isi tree dengan metode inorder sehingga data ditampilkan dalam urutan menaik.

#### Full code Screenshot:
<img width="488" height="566" alt="image" src="https://github.com/user-attachments/assets/3c2e57a4-ab1b-42e9-99e0-d8df7b2bb87c" />
<img width="568" height="1003" alt="image" src="https://github.com/user-attachments/assets/8e246990-c339-4d3e-8fa2-fb5c79c7f871" />
<img width="450" height="570" alt="image" src="https://github.com/user-attachments/assets/dd498d49-093d-4552-bd50-b88b43eee5d8" />

### 3. [Soal]
*bstree.h*
```C++
#ifndef BSTREE_H
#define BSTREE_H

#define Nil NULL

typedef int infotype;
typedef struct Node* address;

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);

void insertNode(address &root, infotype x);
address findNode(infotype x, address root);

void InOrder(address root);

#endif
```
*bstree.cpp*
```C++
#include <iostream>
#include "bstree.h"

using namespace std;

address alokasi(infotype x) {
    address P = new Node;
    if (P != Nil) {
        P->info = x;
        P->left = Nil;
        P->right = Nil;
    }
    return P;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else {
        if (x < root->info) {
            insertNode(root->left, x);
        } else if (x > root->info) {
            insertNode(root->right, x);
        }
    }
}

address findNode(infotype x, address root) {
    if (root == Nil) {
        return Nil;
    } else if (x == root->info) {
        return root;
    } else if (x < root->info) {
        return findNode(x, root->left);
    } else {
        return findNode(x, root->right);
    }
}

void InOrder(address root) {
    if (root != Nil) {
        InOrder(root->left);
        cout << root->info << " - ";
        InOrder(root->right);
    }
}
```
*main.cpp*
```C++
#include <iostream>
#include "bstree.h"

using namespace std;

int main() {
    cout << "Hello World!" << endl;

    address root = Nil;

    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6);
    insertNode(root, 7);

    InOrder(root);

    return 0;
}
```
#### Output:
<img width="781" height="152" alt="image" src="https://github.com/user-attachments/assets/3441b4e5-8abe-48e9-a161-89327c242939" />

Program ini mengimplementasikan ADT Binary Search Tree menggunakan linked list. Struktur Node terdiri dari elemen info, left, dan right. Fungsi alokasi digunakan untuk membuat node baru. Fungsi insertNode menyisipkan data ke dalam tree secara rekursif sesuai aturan BST. Fungsi findNode digunakan untuk mencari data dalam tree, sedangkan fungsi InOrder menampilkan isi tree dengan metode inorder sehingga data ditampilkan dalam urutan menaik.

#### Full code Screenshot:
<img width="488" height="566" alt="image" src="https://github.com/user-attachments/assets/3c2e57a4-ab1b-42e9-99e0-d8df7b2bb87c" />
<img width="568" height="1003" alt="image" src="https://github.com/user-attachments/assets/8e246990-c339-4d3e-8fa2-fb5c79c7f871" />
<img width="450" height="570" alt="image" src="https://github.com/user-attachments/assets/dd498d49-093d-4552-bd50-b88b43eee5d8" />

## Kesimpulan
Berdasarkan hasil praktikum yang telah dilakukan, dapat disimpulkan bahwa struktur data Queue bekerja dengan prinsip FIFO (First In First Out), di mana elemen yang pertama masuk akan menjadi elemen pertama yang keluar. Implementasi Queue menggunakan array dapat dilakukan dengan beberapa mekanisme, yaitu Alternatif 1, Alternatif 2, dan Alternatif 3. Pada Alternatif 1, posisi head bersifat tetap sedangkan tail bergerak dengan konsekuensi adanya pergeseran data saat dequeue. Alternatif 2 menghilangkan pergeseran data dengan membuat head dan tail sama-sama bergerak, namun berpotensi menimbulkan kondisi penuh semu. Sementara itu, Alternatif 3 atau circular queue merupakan implementasi yang paling efisien karena head dan tail bergerak secara berputar sehingga seluruh ruang array dapat dimanfaatkan secara optimal tanpa pergeseran data. Melalui praktikum ini, pemahaman mengenai berbagai teknik implementasi Queue dan kelebihan serta kekurangannya dapat dipelajari dengan baik.

## Referensi
[1] W3Schools. (2025). Queues (Data Structures & Algorithms). https://www.w3schools.com/dsa/dsa_data_queues.php
[2] GeeksforGeeks. (2025). Queue Data Structure. https://www.geeksforgeeks.org/dsa/queue-data-structure/
[3] TutorialsPoint. (2025). Circular Queue Data Structure. https://www.tutorialspoint.com/data_structures_algorithms/circular_queue_data_structure.htm



