# <h1 align="center">Laporan Praktikum Modul Tree </h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori
Tree adalah struktur data non-linear yang terdiri dari node-node yang tersusun secara hierarki. Binary Tree merupakan tree yang setiap node-nya memiliki maksimal dua child, yaitu left dan right. Binary Search Tree (BST) adalah binary tree terurut dengan aturan bahwa node pada subtree kiri bernilai lebih kecil dari parent, sedangkan node pada subtree kanan bernilai lebih besar. Dengan aturan ini, proses pencarian dan penyisipan data dapat dilakukan secara efisien menggunakan metode rekursif.
## Guided 

### 1. [TREE]
*bst.h*
```C++
#ifndef BST_H
#define BST_H
#define Nil nullptr

using namespace std;

typedef struct BST *Node; //alis pointer = node

struct BST{ // nama structnya BST 
    int angka;
    node left;
    node right;
};

typedef node BinTree; //alias tree = BinTree (merujuk ke node root dari BST)

bool isEmpty(BinTree tree);
void createTree(Bintree &tree);
node alokasi(int angka);
void dealokasi(node nodeHapus);

void insertNode(BimTree &tree, node nodeBaru);
void searchByData(BinTree tree, int angka);
void preOrder(BInTree tree);
void inOrder(BinTree tree);
void postOrder(BinTree tree);

bool deleteNode(BinTree &tree, int angka);
node mostRight(BinTree tree);
node mostLeft(BinTree tree);
void deleteTree(BinTree &tree);
int size(BinTree tree);
int hegight(BinTree tree);

#endif
}
```
*bst.cpp*
```C++
#include <iostream>
#include "bst.h"

using namespace std;

int main() {
    BinTree tree;
    createTree(tree);

    int pilih, angka;

    do {
        cout << "========= MENU BST =========" << endl;
        cout << "1. Insert Node" << endl;
        cout << "2. Delete Node" << endl;
        cout << "3. Search Data" << endl;
        cout << "4. Tampilkan PreOrder" << endl;
        cout << "5. Tampilkan InOrder" << endl;
        cout << "6. Tampilkan PostOrder" << endl;
        cout << "7. Size Tree (jumlah node)" << endl;
        cout << "8. Height Tree (tinggi level)" << endl;
        cout << "9. Tampilkan mostright" << endl;
        cout << "10. Tampilkan mostleft" << endl;
        cout << "11. Delete Seluruh Tree" << endl;
        cout << "0. Keluar" << endl;
        cout << "pilihan anda : ";
        cin >> pilih;
        cout << endl;

        switch (pilih){
        case 1:
            cout << "Masukkan angka: ";
            cin >> angka;
            insertNode(tree, alokasi(angka));
            cout << endl;
            break;

        case 2:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                cout << "Masukkan angka yang ingin dihapus: ";
                cin >> angka;
                if(deleteNode(tree, angka)){
                    cout << "Data " << angka << " berhasil dihapus!" << endl;
                } else {
                    cout << "Data " << angka << " tidak ditemukan!" << endl;
                }
            }
            cout << endl;
            break;

        case 3:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                cout << "Masukkan angka yang ingin dicari: ";
                cin >> angka;
                searchByData(tree, angka);
            }
            cout << endl;
            break;

        case 4:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                cout << "PreOrder : ";
                preOrder(tree);
                cout << endl;
            }
            cout << endl;
            break;

        case 5:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                cout << "InOrder : ";
                inOrder(tree);
                cout << endl;
            }
            cout << endl;
            break;

        case 6:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                cout << "PostOrder : ";
                postOrder(tree);
                cout << endl;
            }
            cout << endl;
            break;

        case 7:
            cout << "Size Tree = " << size(tree) << endl;
            cout << endl;
            break;

        case 8:
            cout << "Height Tree = " << height(tree) << endl;
            cout << endl;
            break;

        case 9: 
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
                cout << endl;
            } else {
                cout << "Mostright : " << mostRight(tree)->angka << endl;
                cout << endl;
            }
            break;
        
        case 10:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
                cout << endl;
            } else {
                cout << "Mostleft : " << mostLeft(tree)->angka << endl;
                cout << endl;
            }
            break;

        case 11:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                deleteTree(tree);
                cout << "Seluruh tree berhasil dihapus!" << endl;
            }
            cout << endl;
            break;

        case 0:
            cout << "Keluar dari program..." << endl;
            break;

        default:
            cout << "Pilihan tidak valid!" << endl;
            break;
        }

    } while (pilih != 0);

    return 0;
}
```
*main.cpp*
```C++
#include "bst.h"
#include <iostream>

using namespace std;

//NOTE : parameter tree disini maksudnya merujuk ke node; baik itu node root atau node lain dari tree

bool isEmpty(BinTree tree){
    if(tree == Nil){
        return true;
    } else {
        return false;
    }
}

void createTree(BinTree &tree){
    tree = Nil;
}

node alokasi(int angkaInput){
    node nodeBaru = new BST;
    nodeBaru->angka = angkaInput;
    nodeBaru->left = Nil;
    nodeBaru->right = Nil;
    return nodeBaru;
}

void dealokasi(node nodeHapus){
    delete nodeHapus;
}

void insertNode(BinTree &tree, node nodeBaru){
    if(tree == Nil){
        tree = nodeBaru;
        cout << "Node " << nodeBaru->angka << " berhasil ditambahkan ke dalam tree!" << endl;
        return;
    } else if(nodeBaru->angka < tree->angka){
        insertNode(tree->left, nodeBaru);
    } else if(nodeBaru->angka > tree->angka){
        insertNode(tree->right, nodeBaru);
    }
}

void searchByData(BinTree tree, int angkaCari){
    if(isEmpty(tree) == true){
        cout << "Tree kosong!" << endl;
    } else {
        node nodeBantu = tree;
        node parent = Nil;
        bool ketemu = false;
        while(nodeBantu != Nil){
            if(angkaCari < nodeBantu->angka){
                parent = nodeBantu;
                nodeBantu = nodeBantu->left;
            } else if(angkaCari > nodeBantu->angka){
                parent = nodeBantu;
                nodeBantu = nodeBantu->right;
            } else if(angkaCari == nodeBantu->angka){
                ketemu = true;
                break;
            }
        }
        if(ketemu == false){
            cout << "Data tidak ditemukan" << endl;
        } else if(ketemu == true){
            cout << "Data ditemukan didalam tree!" << endl;
            cout << "Data Angka : " << nodeBantu->angka << endl;

            //menampilkan parentnya & pengecekan sibling
            node sibling = Nil;
            if(parent != Nil){
                cout << "Parent : " << parent->angka << endl;
                if(parent->left == nodeBantu){
                    sibling = parent->right;
                } else if(parent->right == nodeBantu){
                    sibling = parent->left;
                }
            } else {
                cout << "Parent : - (node root)"<< endl;
            }

            //menampilkan siblingnya
            if(sibling != Nil){
                cout << "Sibling : " << sibling->angka << endl;
            } else {
                cout << "Sibling : - " << endl;
            }

            //menampilkan childnya
            if(nodeBantu->left != Nil){
                cout << "Child kiri : " << nodeBantu->left->angka << endl;
            } else if(nodeBantu->left == Nil){
                cout << "Child kiri : -" << endl;
            }
            if(nodeBantu->right != Nil){
                cout << "Child kanan : " << nodeBantu->right->angka << endl;
            } else if(nodeBantu->right == Nil){
                cout << "Child kanan : -" << endl;
            }
        }
    }
}

void preOrder(BinTree tree){
    if(tree == Nil){
        return;
    }
    cout << tree->angka << " - ";
    preOrder(tree->left);
    preOrder(tree->right);
}

void inOrder(BinTree tree){
    if(tree == Nil){
        return;
    }
    inOrder(tree->left);
    cout << tree->angka << " - ";
    inOrder(tree->right);
}

void postOrder(BinTree tree){
    if(tree == Nil){
        return;
    }
    postOrder(tree->left);
    postOrder(tree->right);
    cout << tree->angka << " - ";
}



bool deleteNode(BinTree &tree, int angka) {
    if (tree == Nil) {
        return false; //data tidak ditemukan di subtree ini
    } else {
        if (angka < tree->angka) {
            return deleteNode(tree->left, angka);
        } else if (angka > tree->angka) {
            return deleteNode(tree->right, angka);
        } else {
            //jika node yang mau dihapus ditemukan
            //Case 1 : node yang mau dihapus adalah leaf
            if (tree->left == Nil && tree->right == Nil) {
                node tmp = tree;
                tree = Nil;
                dealokasi(tmp);
            }
            //Case 2 : node yang mau dihapus hanya punya right child
            else if (tree->left == Nil) {
                node tmp = tree;
                tree = tree->right;
                dealokasi(tmp);
            }
            //Case 3 : node yang mau dihapus hanya punya left child
            else if (tree->right == Nil) {
                node tmp = tree;
                tree = tree->left;
                dealokasi(tmp);
            }
            // Case 4 : jika node yang mau dihapus punya dua child, maka ambil mostleft dari subtree kanan untuk menggantikan node yang mau dihapus
            else {
                //mostleft dari subtree kanan = node successor (node penerus)
                node successor = mostLeft(tree->right);
                //salin data successor ke node saat ini
                tree->angka = successor->angka;
                //hapus successor pada subtree kanan
                return deleteNode(tree->right, successor->angka);
            }
            return true; //berhasil dihapus
        }
    }
}

node mostRight(BinTree tree){
    while (tree->right != Nil){
        tree = tree->right;
    }
    return tree;    
}

node mostLeft(BinTree tree){
    while (tree->left != Nil){
        tree = tree->left;
    }
    return tree;
}

void deleteTree(BinTree &tree){
    if(tree == Nil){
        return;
    } else {
        deleteTree(tree->left);
        deleteTree(tree->right);
        dealokasi(tree);
        tree = Nil;
    }
}

int size(BinTree tree){ //mengembalikan jumlah semua node
    if(isEmpty(tree) == true){
        return 0;
    } else {
        return 1 + size(tree->left) + size(tree->right);
    }
    cout << endl;
}

int height(BinTree tree){ //mengembalikan jumlah level tree
    if(isEmpty(tree) == true){
        return -1; //tree kosong jika height = -1
    } else {
        int hl = height(tree->left);
        int hr = height(tree->right);
        int maxHeight;
        if (hl > hr){
            maxHeight = hl;
        } else {
            maxHeight = hr;
        }
        return 1 + maxHeight;
    }
    cout << endl;
}
```

Program ini mengimplementasikan Binary Search Tree (BST) menggunakan pointer dengan operasi insert, search, delete, dan traversal. Struktur tree dijaga agar tetap terurut sesuai aturan BST. Selain itu, program dapat menghitung jumlah node, tinggi tree, serta menampilkan node paling kiri dan paling kanan secara rekursif.

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

int hitungNode(address root);
int hitungTotal(address root);
int hitungKedalaman(address root, int start);

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

int hitungNode(address root) {
    if (root == Nil) {
        return 0;
    } else {
        return 1 + hitungNode(root->left) + hitungNode(root->right);
    }
}

int hitungTotal(address root) {
    if (root == Nil) {
        return 0;
    } else {
        return root->info 
               + hitungTotal(root->left) 
               + hitungTotal(root->right);
    }
}

int hitungKedalaman(address root, int start) {
    if (root == Nil) {
        return start;
    } else {
        int kiri  = hitungKedalaman(root->left, start + 1);
        int kanan = hitungKedalaman(root->right, start + 1);
        return (kiri > kanan) ? kiri : kanan;
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
    insertNode(root,1);
    insertNode(root,2);
    insertNode(root,6);
    insertNode(root,4);
    insertNode(root,5);
    insertNode(root,3);
    insertNode(root,6);
    insertNode(root,7);

    InOrder(root);
    cout << endl;

    cout << "kedalaman : " << hitungKedalaman(root, 0) << endl;
    cout << "jumlah node : " << hitungNode(root) << endl;
    cout << "total : " << hitungTotal(root) << endl;

    return 0;
}
```
#### Output:
<img width="802" height="188" alt="image" src="https://github.com/user-attachments/assets/e0de32d1-37c0-477b-8eaa-01d280d012f9" />

Fungsi hitungNode digunakan untuk menghitung jumlah node dalam Binary Search Tree dengan menjumlahkan seluruh node secara rekursif. Fungsi hitungTotal menghitung total nilai info dari seluruh node dalam tree dengan menjumlahkan nilai setiap node. Fungsi hitungKedalaman digunakan untuk menentukan kedalaman maksimal tree dengan membandingkan kedalaman subtree kiri dan kanan secara rekursif.

#### Full code Screenshot:
<img width="538" height="614" alt="image" src="https://github.com/user-attachments/assets/fa2179f8-8ed6-404b-9098-31436720bc36" />
<img width="641" height="939" alt="image" src="https://github.com/user-attachments/assets/0ddfe194-b893-41fe-88c4-5f0c049cedf8" />
<img width="622" height="622" alt="image" src="https://github.com/user-attachments/assets/0e9781b5-a293-47dc-ac44-73fa9b25f4ce" />

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

int hitungNode(address root);
int hitungTotal(address root);
int hitungKedalaman(address root, int start);

void PreOrder(address root);
void PostOrder(address root);

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

int hitungNode(address root) {
    if (root == Nil) {
        return 0;
    } else {
        return 1 + hitungNode(root->left) + hitungNode(root->right);
    }
}

int hitungTotal(address root) {
    if (root == Nil) {
        return 0;
    } else {
        return root->info 
               + hitungTotal(root->left) 
               + hitungTotal(root->right);
    }
}

int hitungKedalaman(address root, int start) {
    if (root == Nil) {
        return start;
    } else {
        int kiri  = hitungKedalaman(root->left, start + 1);
        int kanan = hitungKedalaman(root->right, start + 1);
        return (kiri > kanan) ? kiri : kanan;
    }
}

void PreOrder(address root) {
    if (root != Nil) {
        cout << root->info << " - ";
        PreOrder(root->left);
        PreOrder(root->right);
    }
}

void PostOrder(address root) {
    if (root != Nil) {
        PostOrder(root->left);
        PostOrder(root->right);
        cout << root->info << " - ";
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
    insertNode(root,1);
    insertNode(root,2);
    insertNode(root,6);
    insertNode(root,4);
    insertNode(root,5);
    insertNode(root,3);
    insertNode(root,6);
    insertNode(root,7);

    InOrder(root);
    cout << endl;

    cout << "kedalaman : " << hitungKedalaman(root, 0) << endl;
    cout << "jumlah node : " << hitungNode(root) << endl;
    cout << "total : " << hitungTotal(root) << endl;
    
    cout << "PreOrder : ";
        PreOrder(root);
    cout << endl;

    cout << "PostOrder : ";
        PostOrder(root);
    cout << endl;

    return 0;
}
```
#### Output:
<img width="786" height="232" alt="image" src="https://github.com/user-attachments/assets/1af9a454-e522-48ae-895e-eb0e3d5b74e7" />

Program ini mengimplementasikan ADT Binary Search Tree menggunakan linked list. Struktur Node terdiri dari elemen info, left, dan right. Fungsi alokasi digunakan untuk membuat node baru. Fungsi insertNode menyisipkan data ke dalam tree secara rekursif sesuai aturan BST. Fungsi findNode digunakan untuk mencari data dalam tree, sedangkan fungsi InOrder menampilkan isi tree dengan metode inorder sehingga data ditampilkan dalam urutan menaik.

#### Full code Screenshot:
<img width="515" height="618" alt="image" src="https://github.com/user-attachments/assets/57ce0470-5295-466b-bd9c-fe533073ca8f" />
<img width="601" height="995" alt="image" src="https://github.com/user-attachments/assets/8ee38e64-35ef-42e0-a074-6c2e38ced0fd" />
<img width="655" height="948" alt="image" src="https://github.com/user-attachments/assets/cb21a958-7798-4023-b14a-fa1cb682af28" />
<img width="618" height="766" alt="image" src="https://github.com/user-attachments/assets/fdb58cec-2871-4378-a23f-b243a50eb912" />

## Kesimpulan
Berdasarkan hasil praktikum Modul Tree, dapat disimpulkan bahwa struktur data Binary Search Tree (BST) merupakan struktur data non-linear yang menyimpan data secara terurut. Implementasi BST menggunakan linked list dan rekursi memudahkan proses penyisipan, pencarian, serta traversal data. Traversal inorder menghasilkan urutan data menaik, sedangkan preorder dan postorder digunakan untuk melihat struktur tree. Selain itu, fungsi rekursif dapat digunakan untuk menghitung jumlah node, total nilai node, dan kedalaman tree secara efisien. Dengan praktikum ini, konsep dasar tree dan penerapannya dalam pemrograman C++ dapat dipahami dengan baik.

## Referensi
[1] GeeksforGeeks. (2025). Binary Search Tree (BST). https://www.geeksforgeeks.org/binary-search-tree-data-structure/  
[2] TutorialsPoint. (2025). Binary Search Tree. https://www.tutorialspoint.com/data_structures_algorithms/binary_search_tree.htm
