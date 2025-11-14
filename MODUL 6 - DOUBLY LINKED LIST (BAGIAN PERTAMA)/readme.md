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


