
  # <h1 align="center">Laporan Praktikum Modul Singly Linked List (Bagian Pertama)</h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori

Modul ini membahas dasar-dasar struktur data **Singly Linked List** dalam bahasa C++. Singly linked list merupakan kumpulan node yang saling terhubung secara searah, di mana setiap node berisi data dan pointer yang menunjuk ke node berikutnya. Berbeda dengan array yang memiliki ukuran tetap, linked list bersifat dinamis sehingga memungkinkan penambahan dan penghapusan elemen dengan mudah tanpa harus menggeser data lain. Di dalam modul dijelaskan cara mendeklarasikan struktur node, membuat pointer head, serta mengimplementasikan operasi dasar seperti menambah, menghapus, dan menampilkan isi list. Dengan mempelajari materi ini, mahasiswa dapat memahami konsep penyimpanan data yang lebih fleksibel dan efisien dalam pengelolaan memori.

## Guided 

### 1. [Singly Linked List (Bagian Pertama)]


Kode ini berfungsi untuk mengelola data mahasiswa menggunakan singly linked list dalam C++. Struktur node menyimpan nama, NIM, dan umur, sedangkan linkedlist menyimpan pointer ke elemen pertama. Fungsi-fungsi di list.cpp digunakan untuk membuat list, menambah atau menghapus node, menampilkan isi list, serta menghitung jumlah elemen. Pada main.cpp, beberapa data mahasiswa dibuat dan dimasukkan ke dalam list menggunakan fungsi insertFirst, insertAfter, dan insertLast, lalu ditampilkan dengan printList. Program ini menunjukkan cara penyimpanan data dinamis yang fleksibel dengan konsep linked list.

## Unguided 

### 1. [Soal]
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

    push(S, 3);
    push(S, 4);
    push(S, 8);
    pop(S);
    push(S, 2);
    push(S, 3);
    pop(S);
    push(S, 9);

    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);

    printInfo(S);

    return 0;
}
```
#### Output:
<img width="785" height="183" alt="image" src="https://github.com/user-attachments/assets/21905806-3133-4832-9a88-82bc969d40e4" />

Program ini mengimplementasikan ADT Stack menggunakan array. Stack menyimpan data dalam array info dan menggunakan variabel top untuk menandai posisi elemen paling atas. Fungsi createStack menginisialisasi stack, push menambah elemen ke atas stack, dan pop menghapus elemen teratas. Fungsi printInfo menampilkan isi stack dari atas ke bawah, sedangkan balikStack membalik urutan stack menggunakan stack sementara. Di fungsi main, beberapa operasi push dan pop dilakukan, kemudian isi stack ditampilkan sebelum dan sesudah dibalik.

#### Full code Screenshot:
<img width="404" height="439" alt="image" src="https://github.com/user-attachments/assets/49b94a02-1d5c-4ffa-a559-b9de0f33df7c" />
<img width="469" height="973" alt="image" src="https://github.com/user-attachments/assets/aa46b6dd-997c-4418-93a5-55a8e09a223a" />
<img width="438" height="638" alt="image" src="https://github.com/user-attachments/assets/3ea58a78-cee0-4f73-870c-0ef48920f927" />

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
Kesimpulan dari kedua program di atas adalah bahwa keduanya menerapkan konsep struktur data dinamis menggunakan singly linked list dalam bahasa C++. Program pertama menekankan pada pembuatan dan penambahan elemen ke dalam list, sedangkan program kedua menambahkan fitur penghapusan elemen serta perhitungan jumlah node. Dari kedua program tersebut dapat disimpulkan bahwa linked list memungkinkan pengelolaan data yang lebih fleksibel dibanding array, karena elemen dapat ditambah atau dihapus tanpa perlu menggeser data lain. Pemahaman tentang pointer dan alokasi memori menjadi hal penting untuk menghindari kesalahan saat mengelola struktur data dinamis seperti ini.


## Referensi
[1] GeeksforGeeks. (n.d.). C++ Program for Deleting a Node in a Linked List. Diakses pada 23 Oktober 2025, dari https://www.geeksforgeeks.org/cpp/cpp-program-for-deleting-a-node-in-a-linked-list/
[2] W3Schools. (n.d.). DSA Linked Lists. Diakses pada 23 Oktober 2025, dari https://www.w3schools.com/dsa/dsa_theory_linkedlists.php

