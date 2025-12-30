# <h1 align="center">Laporan Praktikum Modul Graph </h1>
<p align="center">Noval Ananda Pratama</p>

## Dasar Teori
Graph merupakan struktur data yang terdiri dari sekumpulan simpul (vertex) dan sisi (edge) yang merepresentasikan hubungan antar simpul. Pada graph tidak berarah, setiap sisi menghubungkan dua simpul tanpa arah tertentu sehingga hubungan bersifat dua arah. Graph dapat direpresentasikan menggunakan multilist, di mana setiap node menyimpan daftar edge yang terhubung dengannya. Penelusuran graph dapat dilakukan menggunakan Depth First Search (DFS) yang menelusuri node secara mendalam sebelum berpindah ke cabang lain, serta Breadth First Search (BFS) yang menelusuri node berdasarkan tingkat atau level dari node awal.

## Guided 

### 1. [TREE]
*graph.h*
```C++
#ifndef GRAPH_H
#define GRAPH_H

#include <iostream>

using namespace std;

typedef char infoGraph;
typedef struct ElmNode *adrNode;
typedef struct ElmEdge *adrEdge;

struct ElmNode {
    infoGraph info;      //menyimpan data node (misal: char/int)
    int visited;        //Penanda untuk traversal (0/1) (penanda apakah node sudah dikunjungi)
    adrEdge firstEdge; //Pointer ke edge pertama yang terhubung
    adrNode Next;     //Pointer ke node berikutnya dalam graph
};

struct ElmEdge {
    adrNode Node;  //Pointer yang menunjuk ke lokasi node tujuan
    adrEdge Next;  //Pointer ke edge berikutnya (jika satu node memiliki banyak cabang)
};

struct Graph {
    adrNode First;  //Pointer ke node pertama dalam list graph
};

void CreateGraph(Graph &G);  //prosedur untuk mengeset fitur dari graph sebagai NULL
adrNode AlokasiNode(infoGraph data);  //alokasi node baru
adrEdge AlokasiEdge(adrNode nodeTujuan);  //alokasi Edge baru

void InsertNode(Graph &G, infoGraph data);  //menambahkan node ke dalam graph
adrNode FindNode(Graph G, infoGraph data);  //function untuk mencari alamat node berdasarkan nilai info yang diberikan
void ConnectNode(Graph &G, infoGraph info1, infoGraph info2); //prosedur untuk menghubungkan dua node (membuat edge dari info1 ke info2)
void DisconnectNode(adrNode node1, adrNode node2);  //prosedur untuk memutuskan hubungan dua node (menghapus edge dari node1 ke node2)
void DeleteNode(Graph &G, infoGraph X);  //prosedur untuk menghapus node X beserta semua Edge yang terhubung

void PrintInfoGraph(Graph G);  //Menampilkan isi graph(Adjency list)
void ResetVisited(Graph &G);  //Reset status visited sebelum traversal
void PrintBFS(Graph G, infoGraph StartInfo);  //traversal Breadth Search / BFS (Menggunakan queue untuk menelusuri node berdasarkan tingkat)
void PrintDFS(Graph G, infoGraph StartInfo);  //traversal Depth First Search / DFS (menggunakan stack untuk menelusuri node secara mendalam)

#endif
```
*graph.cpp*
```C++
#include "graph.h"
#include <iostream>
#include <queue> //library queue untuk BFS
#include <stack> //library stack untuk DFS

using namespace std;

//prosedur untuk mengeset first dari graph sebagai NULL
void CreateGraph(Graph &G) {
    G.First = NULL;
}

//alokasi Node baru
adrNode AlokasiNode(infoGraph data) {
    adrNode nodeBaru = new ElmNode;
    nodeBaru->info = data;
    nodeBaru->visited = 0; //isinya 0/1
    nodeBaru->firstEdge = NULL;
    nodeBaru->Next = NULL;
    return nodeBaru;
}

//alokasi Edge baru
adrEdge AlokasiEdge(adrNode nodeTujuan) {
    adrEdge edgeBaru = new ElmEdge;
    edgeBaru->Node = nodeTujuan;
    edgeBaru->Next = NULL;
    return edgeBaru;
}

//Menambahkan Node ke dalam Graph
void InsertNode(Graph &G, infoGraph data) {
    adrNode nodeBaru = AlokasiNode(data);
    if (G.First == NULL) {
        G.First = nodeBaru;
    } else {
        //konsepnya insert last
        adrNode nodeBantu = G.First;
        while (nodeBantu->Next != NULL) {
            nodeBantu = nodeBantu->Next;
        }
        nodeBantu->Next = nodeBaru;
    }
}

//function untuk mencari alamat Node berdasarkan infonya
adrNode FindNode(Graph G, infoGraph data) {
    adrNode nodeBantu = G.First;
    while (nodeBantu != NULL) {
        if (nodeBantu->info == data) {
            return nodeBantu;
        }
        nodeBantu = nodeBantu->Next;
    }
    return NULL;
}

//prosedur untuk menghubungkan dua Node (Undirected Graph)
void ConnectNode(Graph &G, infoGraph info1, infoGraph info2) {
    adrNode node1 = FindNode(G, info1);
    adrNode node2 = FindNode(G, info2);

    if (node1 != NULL && node2 != NULL) {
        //Hubungkan node1 ke node2
        adrEdge Edge1 = AlokasiEdge(node2);
        Edge1->Next = node1->firstEdge; // Insert First pada list edge
        node1->firstEdge = Edge1;

        //Hubungkan node2 ke node1 (Karena Undirected/Bolak-balik)
        adrEdge Edge2 = AlokasiEdge(node1);
        Edge2->Next = node2->firstEdge;
        node2->firstEdge = Edge2;
    } else {
        cout << "Node tidak ditemukan!" << endl;
    }
}

//prosedur untuk memutuskan hubungan dua node
void DisconnectNode(adrNode node1, adrNode node2) {
    if (node1 != NULL && node2 != NULL) {
        adrEdge edgeBantu = node1->firstEdge;
        adrEdge PrevE = NULL;

        //Cari edge yang mengarah ke node2 di dalam list milik node1
        while (edgeBantu != NULL && edgeBantu->Node != node2) {
            PrevE = edgeBantu;
            edgeBantu = edgeBantu->Next;
        }

        if (edgeBantu != NULL) { //jika Edge ditemukan
            if (PrevE == NULL) {
                //Hapus edge pertama
                node1->firstEdge = edgeBantu->Next;
            } else {
                //Hapus edge di tengah/akhir
                PrevE->Next = edgeBantu->Next;
            }
            delete edgeBantu;
        }
    }
}

//prosedur untuk menghapus Node X beserta semua edge yang berhubungan dengannya
void DeleteNode(Graph &G, infoGraph X) {
    //1. Cari Node yang akan dihapus (nodeHapus)
    adrNode nodeHapus = FindNode(G, X);
    if (nodeHapus == NULL) {
        cout << "Node tidak ditemukan." << endl;
        return;
    }

    //2. Hapus semua Edge yang MENGARAH ke nodeHapus (Incoming Edges)
    //cek setiap node di graph, apakah punya edge ke nodeHapus
    adrNode nodeLainnya = G.First;
    while (nodeLainnya != NULL) {
        DisconnectNode(nodeLainnya, nodeHapus); //putus hubungan nodeLainnya ke nodeHapus
        nodeLainnya = nodeLainnya->Next;
    }

    //3. Hapus semua Edge yang KELUAR dari nodeHapus (Outgoing Edges)
    //Deallokasi list edge milik nodeHapus
    adrEdge edgeBantu = nodeHapus->firstEdge;
    while (edgeBantu != NULL) {
        adrEdge tempE = edgeBantu;
        edgeBantu = edgeBantu->Next;
        delete tempE;
    }
    nodeHapus->firstEdge = NULL;

    //4. Hapus nodeHapus dari List Utama Graph
    if (G.First == nodeHapus) {
        //jika nodeHapus di awal
        G.First = nodeHapus->Next;
    } else {
        //jika nodeHapus di tengah/akhir
        adrNode nodeBantu = G.First;
        while (nodeBantu->Next != nodeHapus) {
            nodeBantu = nodeBantu->Next;
        }
        nodeBantu->Next = nodeHapus->Next;
    }

    //5. delete nodeHapus
    delete nodeHapus;
}

//Menampilkan isi Graph (Adjacency List) 
void PrintInfoGraph(Graph G) {
    adrNode nodeBantu = G.First;
    while (nodeBantu != NULL) {
        cout << "Node " << nodeBantu->info << " terhubung ke: ";
        adrEdge edgeBantu = nodeBantu->firstEdge;
        while (edgeBantu != NULL) {
            cout << edgeBantu->Node->info << " "; //Akses info dari node tujuan
            edgeBantu = edgeBantu->Next;
        }
        cout << endl;
        nodeBantu = nodeBantu->Next;
    }
}

//Reset status visited sebelum traversal
void ResetVisited(Graph &G) {
    adrNode nodeReset = G.First;
    while (nodeReset != NULL) {
        nodeReset->visited = 0;
        nodeReset = nodeReset->Next;
    }
}

//traversal Breadth First Search / BFS (Menggunakan Queue)
void PrintBFS(Graph G, infoGraph StartInfo) {
    ResetVisited(G);
    adrNode StartNode = FindNode(G, StartInfo);
    
    if (StartNode == NULL) return;

    queue<adrNode> Qyu;
    
    //Enqueue start
    Qyu.push(StartNode);
    StartNode->visited = 1;

    cout << "BFS Traversal: ";
    while (!Qyu.empty()) {
        adrNode nodeBantu = Qyu.front();
        Qyu.pop();
        cout << nodeBantu->info << " - ";

        //Cek semua tetangga atau edge nya
        adrEdge edgeBantu = nodeBantu->firstEdge;
        while (edgeBantu != NULL) {
            if (edgeBantu->Node->visited == 0) {
                edgeBantu->Node->visited = 1;
                Qyu.push(edgeBantu->Node);
            }
            edgeBantu = edgeBantu->Next;
        }
    }
    cout << endl;
}

//Traversal Depth First Search / DFS (Menggunakan Stack)
void PrintDFS(Graph G, infoGraph StartInfo) {
    ResetVisited(G);
    adrNode StartNode = FindNode(G, StartInfo);
    
    if (StartNode == NULL) return;

    stack<adrNode> Stak;
    
    Stak.push(StartNode);

    cout << "DFS Traversal: ";
    while (!Stak.empty()) {
        adrNode nodeBantu = Stak.top();
        Stak.pop();

        if (nodeBantu->visited == 0) {
            nodeBantu->visited = 1;
            cout << nodeBantu->info << " - ";

            //masukkan tetangga ke stack
            adrEdge edgeBantu = nodeBantu->firstEdge;
            while (edgeBantu != NULL) {
                if (edgeBantu->Node->visited == 0) {
                    Stak.push(edgeBantu->Node);
                }
                edgeBantu = edgeBantu->Next;
            }
        }
    }
    cout << endl;
}
```
*main.cpp*
```C++
#include "graph.h"
#include <iostream>
#include <queue>
#include <stack>
using namespace std;
int main(){
    Graph G;
    CreateGraph(G);

    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');
    InsertNode(G, 'F');
    
    //hubungkan antar node
    ConnectNode(G, 'A', 'B');
    ConnectNode(G, 'A', 'D');
    ConnectNode(G, 'B', 'C');
    ConnectNode(G, 'D', 'C');
    ConnectNode(G, 'B', 'E');
    ConnectNode(G, 'C', 'E');
    ConnectNode(G, 'C', 'F');
    ConnectNode(G, 'E', 'F');

    cout << "=== REPRESENTASI ADJACENCY LIST ===" << endl;
    PrintInfoGraph(G);
    cout << endl;

    cout << "=== HASIL TRAVERSAL ===" << endl;
    //mulai traversal dari node A
    PrintBFS(G, 'A');  //BFS
    PrintDFS(G, 'A');  //DFS
    cout << endl;

    cout << "=== HAPUS NODE E ===" << endl;
    DeleteNode(G, 'E');
    if(FindNode(G, 'E') == NULL) {
        cout << "node E berhasil dihapus" << endl;
    } else {
        cout << "Node E tidak berhasil dihapus" << endl;
    }
    cout << endl;

    cout << "=== REPRESENTASI ADJACENCY LIST ===" << endl;
    PrintInfoGraph(G);
    cout << endl;

    cout << "=== HASIL TRAVERSAL ===" << endl;
    //mulai traversal dari node A
    PrintBFS(G, 'A');  //BFS
    PrintDFS(G, 'A');  //DFS

    return 0;
}
```

Program ini mengimplementasikan Graph tidak berarah menggunakan representasi adjacency list berbasis pointer. Setiap node menyimpan data, daftar edge, dan penanda kunjungan. Proses traversal dilakukan menggunakan Breadth First Search (BFS) dengan queue dan Depth First Search (DFS) dengan stack untuk menelusuri seluruh node tanpa pengulangan. Program juga mendukung penambahan, penghubungan, dan penghapusan node beserta edge yang terkait.
## Unguided 

### 1. [Soal]
*graph.h*
```C++
#ifndef GRAPH_H
#define GRAPH_H

#include <iostream>
using namespace std;

#define Nil NULL

typedef char infoGraph;
typedef struct ElmNode *adrNode;
typedef struct ElmEdge *adrEdge;

struct ElmEdge {
    adrNode Node;
    adrEdge Next;
};

struct ElmNode {
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode Next;
};

struct Graph {
    adrNode first;
};

void CreateGraph(Graph &G);
adrNode AllocateNode(infoGraph X);
adrEdge AllocateEdge(adrNode N);

void InsertNode(Graph &G, infoGraph X);
void ConnectNode(adrNode N1, adrNode N2);
void PrintInfoGraph(Graph G);

void PrintDFS(Graph G, adrNode N);
void PrintBFS(Graph G, adrNode N);

#endif
```
*graph.cpp*
```C++
#include "graph.h"
#include <queue>

void CreateGraph(Graph &G) {
    G.first = Nil;
}

adrNode AllocateNode(infoGraph X) {
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = Nil;
    P->Next = Nil;
    return P;
}

adrEdge AllocateEdge(adrNode N) {
    adrEdge P = new ElmEdge;
    P->Node = N;
    P->Next = Nil;
    return P;
}

void InsertNode(Graph &G, infoGraph X) {
    adrNode P = AllocateNode(X);
    P->Next = G.first;
    G.first = P;
}

void ConnectNode(adrNode N1, adrNode N2) {
    adrEdge E1 = AllocateEdge(N2);
    E1->Next = N1->firstEdge;
    N1->firstEdge = E1;

    adrEdge E2 = AllocateEdge(N1);
    E2->Next = N2->firstEdge;
    N2->firstEdge = E2;
}

void PrintInfoGraph(Graph G) {
    adrNode P = G.first;
    while (P != Nil) {
        cout << P->info << " : ";
        adrEdge E = P->firstEdge;
        while (E != Nil) {
            cout << E->Node->info << " ";
            E = E->Next;
        }
        cout << endl;
        P = P->Next;
    }
}

void PrintDFS(Graph G, adrNode N) {
    if (N != Nil && N->visited == 0) {
        cout << N->info << " ";
        N->visited = 1;
        adrEdge E = N->firstEdge;
        while (E != Nil) {
            PrintDFS(G, E->Node);
            E = E->Next;
        }
    }
}

void PrintBFS(Graph G, adrNode N) {
    queue<adrNode> Q;
    Q.push(N);

    while (!Q.empty()) {
        adrNode P = Q.front();
        Q.pop();

        if (P->visited == 0) {
            cout << P->info << " ";
            P->visited = 1;

            adrEdge E = P->firstEdge;
            while (E != Nil) {
                if (E->Node->visited == 0)
                    Q.push(E->Node);
                E = E->Next;
            }
        }
    }
}
```
*main.cpp*
```C++
#include "graph.h"

int main() {
    Graph G;
    CreateGraph(G);

    InsertNode(G, 'H');
    InsertNode(G, 'G');
    InsertNode(G, 'F');
    InsertNode(G, 'E');
    InsertNode(G, 'D');
    InsertNode(G, 'C');
    InsertNode(G, 'B');
    InsertNode(G, 'A');

    adrNode A = G.first;
    adrNode B = A->Next;
    adrNode C = B->Next;
    adrNode D = C->Next;
    adrNode E = D->Next;
    adrNode F = E->Next;
    adrNode Gg = F->Next;
    adrNode H = Gg->Next;

    ConnectNode(A, B);
    ConnectNode(A, C);
    ConnectNode(B, D);
    ConnectNode(B, E);
    ConnectNode(C, F);
    ConnectNode(C, Gg);
    ConnectNode(D, H);
    ConnectNode(E, H);
    ConnectNode(F, H);
    ConnectNode(Gg, H);

    cout << "DFS : ";
    PrintDFS(G, A);

    adrNode P = G.first;
    while (P != Nil) {
        P->visited = 0;
        P = P->Next;
    }

    cout << endl << "BFS : ";
    PrintBFS(G, A);

    return 0;
}
```
#### Output:
<img width="785" height="152" alt="image" src="https://github.com/user-attachments/assets/781d513a-2ad2-4282-a7ce-855baabc54eb" />

Program ini mengimplementasikan ADT Graph tidak berarah menggunakan representasi multilist, di mana setiap node menyimpan daftar edge yang terhubung dengannya. Prosedur DFS menelusuri graph secara mendalam menggunakan rekursi, sedangkan BFS menelusuri graph berdasarkan level menggunakan queue. Implementasi ini sesuai dengan ilustrasi graph pada modul dan menghasilkan urutan penelusuran DFS dan BFS yang benar.

#### Full code Screenshot:
<img width="517" height="885" alt="image" src="https://github.com/user-attachments/assets/21b6e56f-b017-48a5-b11e-86dd5ba89171" />
<img width="541" height="825" alt="image" src="https://github.com/user-attachments/assets/c80ee7ab-4767-46ac-a929-54c4a7eace55" />
<img width="529" height="987" alt="image" src="https://github.com/user-attachments/assets/edc70d14-22a6-4a4c-952b-dccfb6458b1c" />

## Kesimpulan
Berdasarkan hasil implementasi dan pengujian, ADT Graph tidak berarah berhasil dibangun menggunakan representasi multilist. Seluruh node dan edge dapat terhubung dengan benar sesuai dengan ilustrasi graph pada modul. Proses penelusuran menggunakan algoritma Depth First Search (DFS) dan Breadth First Search (BFS) dapat dijalankan dengan baik tanpa terjadi pengulangan node yang tidak semestinya. Perbedaan urutan hasil penelusuran DFS dan BFS yang muncul disebabkan oleh urutan penyimpanan edge pada adjacency list, sehingga memungkinkan adanya lebih dari satu urutan traversal yang valid meskipun struktur graph yang digunakan sama.

## Referensi
[1] Modul 14 Struktur Data: Graph. Fakultas Informatika, School of Computing, Telkom University. 
[2] GeeksforGeeks. (2023). Breadth First Search (BFS) for a Graph. https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/
[3] GeeksforGeeks. (2023). Depth First Search (DFS) for a Graph. https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/
