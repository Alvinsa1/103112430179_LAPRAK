# <h1 align="center">Laporan Praktikum Modul 8 <br> QUEUE</h1>
<p align="center">Alvinsa Hafizh Arkaan - 103112430179</p>

## Dasar Teori
Queue (antrian) adalah struktur data linear yang mengikuti prinsip FIFO (First In, First Out), artinya elemen yang pertama masuk akan menjadi elemen pertama yang keluar. Konsep ini mirip dengan antrian di dunia nyata, seperti antrian di kasir, di mana orang yang datang lebih dulu akan dilayani lebih dulu. Queue memiliki dua operasi utama: enqueue, yaitu menambahkan elemen ke bagian belakang antrian, dan dequeue, yaitu menghapus elemen dari bagian depan antrian. Selain itu, terdapat operasi lain seperti peek/front untuk melihat elemen terdepan tanpa menghapusnya dan isEmpty untuk mengecek apakah antrian kosong. Cara kerja queue dimulai ketika data baru masuk dengan operasi enqueue yang menempatkannya di baris paling belakang, kemudian saat diperlukan, data di bagian paling depan akan diambil menggunakan operasi dequeue, sehingga menjaga urutan pemrosesan data secara teratur sesuai prinsip FIFO.

## Guide

```go
#include <iostream>
using namespace std;

#define MAX 5 // ukuran maksimal queue

// Struktur Queue
struct Queue {
    int data[MAX];
    int head;
    int tail;
};

// Membuat antrean kosong
void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmpty(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFull(Queue Q) {
    return (Q.tail == MAX - 1);
}

// Menampilkan isi antrian
void printQueue(Queue Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong!" << endl;
    } else {
        cout << "Queue : ";
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.data[i] << " ";
        }
        cout << endl;
    }
}

void enqueue(Queue &Q, int x) {
    if (isFull(Q)) {
        cout << "Queue penuh! Tidak bisa menambah data." << endl;
    } else {
        if (isEmpty(Q)) {
            Q.head = Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.data[Q.tail] = x;
        cout << "Enqueue: " << x << endl;
    }
}

void dequeue(Queue &Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong! Tidak ada data yang dihapus." << endl;
    } else {
        cout << "Dequeue: " << Q.data[Q.head] << endl;
        // Jika hanya 1 elemen
        if (Q.head == Q.tail) {
            Q.head = Q.tail = -1;
        } else {
            // Geser semua elemen ke kiri
            for (int i = Q.head; i < Q.tail; i++) {
                Q.data[i] = Q.data[i + 1];
            }
            Q.tail--;
        }
    }
}

int main() {
    Queue Q;
    enqueue(Q, 5);
    enqueue(Q, 2);
    enqueue(Q, 7);
    printQueue(Q);

    dequeue(Q);
    printQueue(Q);

    enqueue(Q, 4);
    enqueue(Q, 9);
    printQueue(Q);

    dequeue(Q);
    dequeue(Q);
    printQueue(Q);

    return 0;
}
```


## Unguide

### Soal 1
> ![Screenshot bagian x](https://github.com/.png)

### queue.h
```go
#ifndef QUEUE_H
#define QUEUE_H

typedef int infotype;

typedef struct {
    infotype info[5];
    int head;
    int tail;
} Queue;

void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
infotype dequeue(Queue &Q);
void printInfo(Queue Q);

#endif

```

### queue.cpp
```go
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q) {
    Q.head = 0;
    Q.tail = -1;
    for(int i = 0; i < 5; i++) {
        Q.info[i] = 0;
    }
}

bool isEmptyQueue(Queue Q) {
    return (Q.tail < Q.head);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == 4);
}

void enqueue(Queue &Q, infotype x) {
    if (!isFullQueue(Q)) {
        Q.tail++;
        Q.info[Q.tail] = x;
    } else {
        cout << "Queue Penuh!" << endl;
    }
}

infotype dequeue(Queue &Q) {
    if (!isEmptyQueue(Q)) {
        infotype x = Q.info[Q.head];

        for (int i = 0; i < Q.tail; i++) {
            Q.info[i] = Q.info[i + 1];
        }

        Q.tail--;
        return x;
    } else {
        cout << "Queue Kosong!" << endl;
        return -1;
    }
}

void printInfo(Queue Q) {
    cout << "H=" << Q.head << ", T=" << Q.tail << " | Queue Info : ";

    if (isEmptyQueue(Q)) {
        cout << "empty queue" << endl;
        return;
    }

    for (int i = Q.head; i <= Q.tail; i++) {
        cout << Q.info[i] << " ";
    }
    cout << endl;
}

```

### main.cpp
```go
#include <iostream>
#include "queue.h"
using namespace std;

int main() {
    cout << "Hello World" << endl;
    Queue Q;
    createQueue(Q);

    cout << "--------------------------" << endl;
    cout << "H - T \t | Queue info" << endl;
    cout << "--------------------------" << endl;

    printInfo(Q);
    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    dequeue(Q); printInfo(Q);
    dequeue(Q); printInfo(Q);

    return 0;
}
   
```

> Output
> ![Screenshot bagian x](https://github.com/.png)

Program di atas mengimplementasikan struktur data Queue (antrian) menggunakan array statis berukuran tetap (MAX = 5) dengan konsep FIFO. Queue disimpan dalam struct yang memiliki array info serta indeks head dan tail untuk menandai elemen depan dan belakang. Fungsi createQueue menginisialisasi queue agar kosong, isEmptyQueue dan isFullQueue mengecek kondisi queue, enqueue menambah elemen ke belakang antrian jika belum penuh, sedangkan dequeue menghapus elemen terdepan dan mengatur ulang posisi head–tail, termasuk mereset queue saat hanya tersisa satu elemen. Fungsi printInfo menampilkan posisi head, tail, dan seluruh isi antrian. Pada fungsi main, program membuat queue, lalu melakukan serangkaian operasi enqueue dan dequeue sambil mencetak kondisi queue setiap langkah untuk menunjukkan bagaimana antrian berubah seiring penambahan dan penghapusan elemen.
### Soal 2
> ![Screenshot bagian x](https://github.com/.png)

### queue.cpp
```go
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q){
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q){
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q){
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x){
    if (isFullQueue(Q)){
        cout << "Queue penuh!" << endl;
        return;
    }

    if (isEmptyQueue(Q)){
        Q.head = 0;
        Q.tail = 0;
        Q.info[Q.tail] = x;
    } else {
        Q.tail++;
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q){
    if (isEmptyQueue(Q)){
        cout << "Queue kosong!" << endl;
        return -1;
    }

    infotype val = Q.info[Q.head];

    if (Q.head == Q.tail){
        createQueue(Q);
    } else {
        Q.head++;  
    }

    return val;
}

void printInfo(Queue Q){
    cout << Q.head << " - " << Q.tail << "\t|\t";

    if (isEmptyQueue(Q)){
        cout << "empty queue" << endl;
        return;
    }

    for (int i = Q.head; i <= Q.tail; i++){
        cout << Q.info[i] << " ";
    }
    cout << endl;
}

```

> Output
> ![Screenshot bagian x](https://github.com/.png)

Kode di atas merupakan implementasi struktur data Queue (antrian) menggunakan array statis dengan konsep FIFO (First In First Out). Fungsi createQueue menginisialisasi queue dengan menjadikan head dan tail bernilai -1 sebagai tanda bahwa queue masih kosong. Fungsi isEmptyQueue memeriksa apakah queue kosong dengan mengecek apakah kedua indeks tersebut bernilai -1, sedangkan isFullQueue mengecek apakah indeks tail telah mencapai batas maksimum array. Fungsi enqueue menambahkan elemen baru ke bagian belakang antrian: jika queue penuh, ditampilkan pesan peringatan; jika masih kosong, head dan tail diset ke 0; jika sudah ada elemen, tail dinaikkan lalu data baru disimpan. Fungsi dequeue menghapus elemen terdepan: jika kosong ditampilkan pesan, jika hanya ada satu elemen maka queue di-reset, dan jika ada lebih dari satu elemen maka head dinaikkan. Fungsi printInfo menampilkan posisi head–tail serta isi queue; jika kosong, ditampilkan pesan “empty queue”. Kode ini menunjukkan operasi dasar queue menggunakan array linear tanpa mekanisme circular queue.

### Soal 3
> ![Screenshot bagian x](https://github.com/.png)

### queue.cpp
```go
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q){
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q){
    return (Q.head == -1);
}

bool isFullQueue(Queue Q){
    return ((Q.tail + 1) % MAX == Q.head);
}

void enqueue(Queue &Q, infotype x){
    if (isFullQueue(Q)){
        cout << "Queue penuh!" << endl;
        return;
    }

    if (isEmptyQueue(Q)){
        Q.head = 0;
        Q.tail = 0;
        Q.info[Q.tail] = x;
    } else {
        Q.tail = (Q.tail + 1) % MAX;
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q){
    if (isEmptyQueue(Q)){
        cout << "Queue kosong!" << endl;
        return -1;
    }

    infotype val = Q.info[Q.head];

    if (Q.head == Q.tail){  
        createQueue(Q);     
    } else {
        Q.head = (Q.head + 1) % MAX;
    }

    return val;
}

void printInfo(Queue Q){
    cout << Q.head << " - " << Q.tail << "\t|\t";

    if (isEmptyQueue(Q)){
        cout << "empty queue" << endl;
        return;
    }

    int i = Q.head;
    while (true){
        cout << Q.info[i] << " ";
        if (i == Q.tail) break;
        i = (i + 1) % MAX;
    }

    cout << endl;
}
 
```

> Output
> ![Screenshot bagian x](https://github.com/.png)

Kode di atas merupakan implementasi circular queue menggunakan array statis berukuran tetap, di mana indeks head dan tail bergerak melingkar dengan operasi modulo. Fungsi createQueue menginisialisasi queue sebagai kosong dengan head dan tail bernilai -1, sedangkan isEmptyQueue memeriksa kekosongan hanya dengan mengecek head, dan isFullQueue menentukan apakah queue penuh dengan melihat apakah posisi setelah tail kembali ke head. Fungsi enqueue menambahkan elemen ke antrian: jika queue kosong, head dan tail diset ke 0; jika tidak, tail digeser ke indeks berikutnya menggunakan operasi (tail + 1) % MAX sebelum menyimpan data. Fungsi dequeue menghapus elemen terdepan dan mengembalikannya: jika hanya ada satu elemen, queue di-reset, sedangkan jika lebih, head digeser menggunakan modulo. Fungsi printInfo menampilkan posisi head–tail serta seluruh isi queue dengan perulangan melingkar hingga mencapai tail. Dengan mekanisme circular queue ini, ruang array dimanfaatkan lebih efisien dibanding queue linear biasa.

## Referensi
1. https://www.w3schools.com/cpp/cpp_functions.asp
2. https://www.w3schools.com/cpp/cpp_arrays.asp
3. https://www.w3schools.com/cpp/cpp_user_input.asp
4. https://www.w3schools.com/cpp/cpp_while_loop.asp
5. https://www.w3schools.com/cpp/cpp_stacks.asp


