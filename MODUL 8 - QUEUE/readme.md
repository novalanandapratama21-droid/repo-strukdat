# <h1 align="center">Laporan Praktikum Modul Queue </h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

Queue adalah struktur data linear yang bekerja dengan prinsip FIFO (First In First Out), yaitu elemen yang pertama masuk ke dalam queue akan menjadi elemen pertama yang keluar. Queue memiliki dua penunjuk utama, yaitu head sebagai posisi penghapusan elemen dan tail sebagai posisi penambahan elemen. Operasi utama dalam queue terdiri dari enqueue, yaitu proses menambahkan elemen pada bagian tail, dan dequeue, yaitu proses menghapus elemen pada bagian head. Pada implementasi menggunakan array, salah satu mekanisme yang digunakan adalah Queue Alternatif 1, di mana posisi head tetap (diam) selama queue tidak kosong, sedangkan tail bergerak mengikuti penambahan dan penghapusan elemen, dengan cara menggeser data saat terjadi penghapusan.
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
*queue.h*
```C++
#ifndef QUEUE_H
#define QUEUE_H

#include <iostream>
using namespace std;

#define MAX 5

typedef int infotype;

struct Queue {
    infotype info[MAX];
    int head;
    int tail;
};

void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
infotype dequeue(Queue &Q);
void printInfo(Queue Q);

#endif
```
*queue.cpp*
```C++
#include "queue.h"

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (!isFullQueue(Q)) {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q) {
    infotype x;
    if (!isEmptyQueue(Q)) {
        x = Q.info[Q.head];

        for (int i = Q.head; i < Q.tail; i++) {
            Q.info[i] = Q.info[i + 1];
        }
        Q.tail--;

        if (Q.tail < Q.head) {
            Q.head = -1;
            Q.tail = -1;
        }
        return x;
    }
    return -1;
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << "\t | ";
    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
}
```
*main.cpp*
```C++
#include <iostream>
#include "queue.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Queue Q;
    createQueue(Q);

    cout << "----------------------" << endl;
    cout << "H - T  | Queue Info" << endl;
    cout << "----------------------" << endl;

    printInfo(Q);

    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);

    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);

    enqueue(Q, 4); printInfo(Q);

    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);

    return 0;
}
```
#### Output:
<img width="860" height="440" alt="image" src="https://github.com/user-attachments/assets/671daa1c-5c60-48a1-a137-e864f86b53ec" />

Program Queue pada soal nomor 1 mengimplementasikan ADT Queue menggunakan array dengan kapasitas tetap sebanyak lima elemen. Proses createQueue digunakan untuk menginisialisasi queue dalam keadaan kosong dengan nilai head dan tail bernilai -1. Operasi enqueue berfungsi untuk menambahkan data ke dalam queue dengan memajukan posisi tail, sedangkan operasi dequeue berfungsi untuk menghapus data paling depan dengan cara menggeser elemen ke kiri agar posisi head tetap berada di indeks 0. Fungsi printInfo digunakan untuk menampilkan nilai head, tail, serta isi queue sehingga perubahan kondisi queue dapat diamati setelah setiap operasi dilakukan.

#### Full code Screenshot:
<img width="545" height="658" alt="image" src="https://github.com/user-attachments/assets/53c66486-a612-4287-ac5f-0a7cb54aaad3" />
<img width="537" height="994" alt="image" src="https://github.com/user-attachments/assets/9d6ff5d3-6d3b-419d-bf46-f9cae91da5c0" />
<img width="514" height="664" alt="image" src="https://github.com/user-attachments/assets/8a3f4212-2c48-4334-9589-4fde39f711b8" />

### 2. [Soal]
*queue.h*
```C++
    #ifndef QUEUE_H
    #define QUEUE_H

    #include <iostream>
    using namespace std;

    #define MAX 5

    typedef int infotype;

    struct Queue {
        infotype info[MAX];
        int head;
        int tail;
    };

    void createQueue(Queue &Q);
    bool isEmptyQueue(Queue Q);
    bool isFullQueue(Queue Q);
    void enqueue(Queue &Q, infotype x);
    infotype dequeue(Queue &Q);
    void printInfo(Queue Q);

    #endif
```
*queue.cpp*
```C++
#include "queue.h"

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (!isFullQueue(Q)) {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q) {
    infotype x = -1;
    if (!isEmptyQueue(Q)) {
        x = Q.info[Q.head];
        Q.head++;

        if (Q.head > Q.tail) {
            Q.head = -1;
            Q.tail = -1;
        }
    }
    return x;
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << " | ";
    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
}
```
*main.cpp*
```C++
#include <iostream>
#include "queue.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Queue Q;
    createQueue(Q);

    cout << "----------------------" << endl;
    cout << "H - T  | Queue Info" << endl;
    cout << "----------------------" << endl;

    printInfo(Q);

    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);

    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);

    enqueue(Q, 4); printInfo(Q);

    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);

    return 0;
}
```
#### Output:
<img width="757" height="337" alt="image" src="https://github.com/user-attachments/assets/b32203d7-8f67-45c3-8af7-857dcec8fca8" />

ADT Queue diimplementasikan menggunakan array dengan mekanisme Queue Alternatif 2, yaitu head bergerak dan tail bergerak. Pada mekanisme ini, proses enqueue dilakukan dengan menambahkan elemen di posisi tail dan memajukan nilai tail, sedangkan proses dequeue dilakukan dengan mengambil elemen pada posisi head lalu memajukan nilai head tanpa melakukan pergeseran data. Pendekatan ini lebih efisien dibanding Alternatif 1 karena tidak membutuhkan proses penggeseran elemen, namun memiliki kelemahan berupa kemungkinan terjadinya queue penuh semu, yaitu kondisi ketika array terlihat penuh meskipun masih terdapat ruang kosong di bagian awal array.

#### Full code Screenshot:
<img width="508" height="573" alt="image" src="https://github.com/user-attachments/assets/38f674a1-b3bc-4754-83da-bf222b7bed7c" />
<img width="492" height="927" alt="image" src="https://github.com/user-attachments/assets/c8278dc2-36ea-4a15-9102-5c95db894d0d" />
<img width="544" height="669" alt="image" src="https://github.com/user-attachments/assets/e8d16345-4a35-4d24-a127-198359027bc1" />

### 3. [Soal]
*queue.h*
```C++
    #ifndef QUEUE_H
    #define QUEUE_H

    #include <iostream>
    using namespace std;

    #define MAX 5

    typedef int infotype;

    struct Queue {
        infotype info[MAX];
        int head;
        int tail;
    };

    void createQueue(Queue &Q);
    bool isEmptyQueue(Queue Q);
    bool isFullQueue(Queue Q);
    void enqueue(Queue &Q, infotype x);
    infotype dequeue(Queue &Q);
    void printInfo(Queue Q);

    #endif
```
*queue.cpp*
```C++
#include "queue.h"

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (!isFullQueue(Q)) {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q) {
    infotype x = -1;
    if (!isEmptyQueue(Q)) {
        x = Q.info[Q.head];
        Q.head++;

        if (Q.head > Q.tail) {
            Q.head = -1;
            Q.tail = -1;
        }
    }
    return x;
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << " | ";
    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
}
```
*main.cpp*
```C++
#include <iostream>
#include "queue.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Queue Q;
    createQueue(Q);

    cout << "----------------------" << endl;
    cout << "H - T  | Queue Info" << endl;
    cout << "----------------------" << endl;

    printInfo(Q);

    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);

    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);

    enqueue(Q, 4); printInfo(Q);

    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);

    return 0;
}
```
#### Output:
<img width="770" height="351" alt="image" src="https://github.com/user-attachments/assets/93bbb187-3b55-47ee-ac5c-2cd9cdc0bf09" />

Pada soal nomor 3, ADT Queue diimplementasikan menggunakan mekanisme Queue Alternatif 3, di mana head dan tail bergerak secara berputar (circular) mengikuti indeks array. Proses enqueue dan dequeue dilakukan dengan memanfaatkan operasi modulo sehingga head dan tail dapat kembali ke indeks awal ketika mencapai batas akhir array. Mekanisme ini menghilangkan kebutuhan pergeseran data serta mencegah terjadinya kondisi penuh semu seperti pada Alternatif 2. Oleh karena itu, Queue Alternatif 3 merupakan implementasi yang paling efisien karena seluruh ruang array dapat dimanfaatkan secara optimal.

#### Full code Screenshot:
<img width="482" height="563" alt="image" src="https://github.com/user-attachments/assets/9e581e56-5f7e-4bd7-81a0-90f3f640f794" />
<img width="507" height="1026" alt="image" src="https://github.com/user-attachments/assets/5f5c764b-3f10-4225-9beb-079aee850b04" />
<img width="500" height="661" alt="image" src="https://github.com/user-attachments/assets/ef8a8fcc-080f-4dd1-94dc-21f82d99d2ed" />

## Kesimpulan
Berdasarkan hasil praktikum yang telah dilakukan, dapat disimpulkan bahwa struktur data Queue bekerja dengan prinsip FIFO (First In First Out), di mana elemen yang pertama masuk akan menjadi elemen pertama yang keluar. Implementasi Queue menggunakan array dapat dilakukan dengan beberapa mekanisme, yaitu Alternatif 1, Alternatif 2, dan Alternatif 3. Pada Alternatif 1, posisi head bersifat tetap sedangkan tail bergerak dengan konsekuensi adanya pergeseran data saat dequeue. Alternatif 2 menghilangkan pergeseran data dengan membuat head dan tail sama-sama bergerak, namun berpotensi menimbulkan kondisi penuh semu. Sementara itu, Alternatif 3 atau circular queue merupakan implementasi yang paling efisien karena head dan tail bergerak secara berputar sehingga seluruh ruang array dapat dimanfaatkan secara optimal tanpa pergeseran data. Melalui praktikum ini, pemahaman mengenai berbagai teknik implementasi Queue dan kelebihan serta kekurangannya dapat dipelajari dengan baik.

## Referensi
[1] W3Schools. (2025). Queues (Data Structures & Algorithms). https://www.w3schools.com/dsa/dsa_data_queues.php
[2] GeeksforGeeks. (2025). Queue Data Structure. https://www.geeksforgeeks.org/dsa/queue-data-structure/
[3] TutorialsPoint. (2025). Circular Queue Data Structure. https://www.tutorialspoint.com/data_structures_algorithms/circular_queue_data_structure.htm


