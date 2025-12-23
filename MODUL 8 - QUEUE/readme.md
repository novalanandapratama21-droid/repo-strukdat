# <h1 align="center">Laporan Praktikum Modul Queue </h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

Queue adalah struktur data linear yang bekerja dengan prinsip FIFO (First In First Out), yaitu elemen yang pertama masuk ke dalam queue akan menjadi elemen pertama yang keluar. Queue memiliki dua penunjuk utama, yaitu head sebagai posisi penghapusan elemen dan tail sebagai posisi penambahan elemen. Operasi utama dalam queue terdiri dari enqueue, yaitu proses menambahkan elemen pada bagian tail, dan dequeue, yaitu proses menghapus elemen pada bagian head. Pada implementasi menggunakan array, salah satu mekanisme yang digunakan adalah Queue Alternatif 1, di mana posisi head tetap (diam) selama queue tidak kosong, sedangkan tail bergerak mengikuti penambahan dan penghapusan elemen, dengan cara menggeser data saat terjadi penghapusan.
## Guided 

### 1. [Stack]
*stack.h*
```C++

```
*stack.cpp*
```C++

```
*main.cpp*
```C++

```

Program ini mengimplementasikan struktur data Stack menggunakan array dengan kapasitas tetap. Stack disimpan dalam struct stackTable yang memiliki array data dan variabel top sebagai penanda elemen teratas. Fungsi dasar seperti push dan pop digunakan untuk menambah dan menghapus elemen sesuai prinsip LIFO, sedangkan isEmpty dan isFull memeriksa kondisi stack. Fungsi update memungkinkan perubahan nilai pada posisi tertentu yang dihitung dari bagian atas stack, view menampilkan seluruh isi stack dari atas ke bawah, dan searchData melakukan pencarian elemen mulai dari top. Dalam fungsi main, beberapa data dimasukkan, dihapus, diperbarui, dan dicari sehingga menunjukkan bagaimana operasi-operasi stack bekerja secara keseluruhan.

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
*stack.h*
```C++
#ifndef STACK_H
#define STACK_H

typedef int infotype;

typedef struct {
    infotype info[20];
    int top;
} Stack;

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);

#endif
```
*stack.cpp*
```C++
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < 19) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        int x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);

    while (S.top != -1) {
        push(temp, pop(S));
    }

    S = temp;
}

void pushAscending(Stack &S, infotype x) {
    Stack temp;
    createStack(temp);

    while (S.top != -1 && S.info[S.top] > x) {
        push(temp, pop(S));
    }

    push(S, x);

    while (temp.top != -1) {
        push(S, pop(temp));
    }
}

```
*main.cpp*
```C++
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    pushAscending(S, 3);
    pushAscending(S, 4);
    pushAscending(S, 8);
    pushAscending(S, 2);
    pushAscending(S, 3);
    pushAscending(S, 9);

    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```
#### Output:
<img width="787" height="183" alt="image" src="https://github.com/user-attachments/assets/7340f79e-c980-47ef-8d51-683a56ba4121" />

Fungsi pushAscending memasukkan data ke stack sambil menjaga agar elemen-elemen di dalamnya tetap terurut naik. Cara kerjanya adalah memindahkan sementara elemen yang lebih besar, memasukkan nilai baru, lalu mengembalikan elemen yang dipindahkan. Di main, beberapa nilai dimasukkan dengan pushAscending, sehingga stack langsung tersusun ascending. Setelah ditampilkan, stack dibalik dengan balikStack dan hasilnya ditampilkan kembali.

#### Full code Screenshot:
<img width="429" height="450" alt="image" src="https://github.com/user-attachments/assets/d0e58b3e-2a1e-4495-b214-a1c400759466" />
<img width="368" height="890" alt="image" src="https://github.com/user-attachments/assets/5d090075-39fe-44f9-b741-15e5888487ce" />
<img width="436" height="576" alt="image" src="https://github.com/user-attachments/assets/eacb0216-15b2-4b42-99dd-cb59b21e637d" />

### 3. [Soal]
*stack.h*
```C++
#ifndef STACK_H
#define STACK_H

typedef int infotype;

typedef struct {
    infotype info[20];
    int top;
} Stack;

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);
void getInputStream(Stack &S);

#endif
```
*stack.cpp*
```C++
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < 19) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        int x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);

    while (S.top != -1) {
        push(temp, pop(S));
    }

    S = temp;
}

void pushAscending(Stack &S, infotype x) {
    Stack temp;
    createStack(temp);

    while (S.top != -1 && S.info[S.top] > x) {
        push(temp, pop(S));
    }

    push(S, x);

    while (temp.top != -1) {
        push(S, pop(temp));
    }
}

void getInputStream(Stack &S) {
    char c;

    cin >> c;

    while (c != '\n')
    {
        push(S, c - '0');
        c = cin.get();
    }
}
```
*main.cpp*
```C++
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    getInputStream(S);

    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```
#### Output:
<img width="781" height="199" alt="image" src="https://github.com/user-attachments/assets/c310e061-eee7-474d-bc68-353d6aaa0d28" />

getInputStream membaca input pengguna satu karakter setiap kali, kemudian memasukkan setiap karakter angka ke dalam stack. Pembacaan dilakukan terus-menerus menggunakan cin.get() sampai pengguna menekan tombol ENTER. Setiap karakter yang diterima dikonversi menjadi angka dan langsung dimasukkan ke stack dengan push. Di fungsi main, input dimasukkan sebagai rangkaian angka, lalu isi stack ditampilkan sebelum dan sesudah dibalik menggunakan balikStack.

#### Full code Screenshot:
<img width="419" height="485" alt="image" src="https://github.com/user-attachments/assets/3fdf8e30-5b0a-4e1e-ba72-ea67dcccd39a" />
<img width="309" height="883" alt="image" src="https://github.com/user-attachments/assets/b56f6a8e-6351-432e-9580-9997050d09c5" />
<img width="389" height="503" alt="image" src="https://github.com/user-attachments/assets/6aaccb67-9de1-49de-a9a0-b33b9685f103" />


## Kesimpulan
Kesimpulan dari ketiga program di atas adalah bahwa semuanya menerapkan konsep struktur data stack menggunakan array sebagai media penyimpanan. Program pertama menekankan pada operasi dasar seperti push, pop, menampilkan isi stack, serta membalik urutannya. Program kedua memperluas fungsi stack dengan menambahkan pushAscending yang memungkinkan penyisipan data secara terurut. Program ketiga menambahkan kemampuan membaca input karakter berurutan dari pengguna melalui getInputStream. Dari seluruh program tersebut dapat disimpulkan bahwa implementasi stack dengan array memungkinkan pengelolaan data secara terstruktur berdasarkan prinsip LIFO, sekaligus dapat dikembangkan dengan berbagai fitur tambahan. Pemahaman mengenai indeks array, operasi pada variabel top, serta alur masuk-keluarnya data menjadi hal penting agar stack dapat dikelola dengan benar dan efisien.


## Referensi
[1] GeeksforGeeks. (n.d.). Stack Data Structure. https://www.geeksforgeeks.org/stack-data-structure/
[2] Tutorialspoint. (n.d.). Data Structures — Stack. https://www.tutorialspoint.com/data_structures_algorithms/stack_algorithm.htm
[3] W3Schools. (n.d.). C++ Input and Streams. https://www.w3schools.com/cpp/cpp_files.asp


