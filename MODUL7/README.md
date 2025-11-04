# <h1 align="center">Laporan Praktikum Modul 7 <br> Stack</h1>
<p align="center">Alvinsa Hafizh Arkaan - 103112430179</p>

## Dasar Teori
Stack adalah salah satu struktur data yang bersifat LIFO (Last In, First Out), artinya elemen yang terakhir dimasukkan akan menjadi elemen pertama yang dikeluarkan. Stack sering diibaratkan seperti tumpukan piring: piring yang terakhir diletakkan di atas adalah yang pertama diambil. Dalam implementasinya, stack memiliki dua operasi utama, yaitu push (menambahkan elemen ke dalam stack) dan pop (menghapus elemen dari stack). Selain itu, terdapat operasi tambahan seperti peek/top untuk melihat elemen teratas tanpa menghapusnya, serta isEmpty untuk memeriksa apakah stack kosong. Struktur data ini banyak digunakan dalam pemrograman untuk berbagai keperluan seperti pengelolaan pemanggilan fungsi (function call), pembalikan urutan data, pengecekan tanda kurung dalam ekspresi, serta implementasi algoritma rekursif. Stack dapat diimplementasikan menggunakan array atau linked list, tergantung kebutuhan efisiensi memori dan kemudahan operasi.

## Guide

```go
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpety(Node *top)
{
    return top == nullptr;
}

void push(Node *&top, int data){
    Node *newNode = new Node;
    newNode -> data = data;
    newNode -> next = top;
    top = newNode;
}

int pop(Node *&top)
{
    if (isEmpety(top))
    {
        cout << "Stack Kosong, tidak bisa pop!" << endl;
        return 0;
    }

    int poppedData = top -> data;
    top = top -> next;

    Node *temp;
    return poppedData;
}

void show (Node *top)
{
    if (isEmpety(top))
    {
        cout << "Stack kosong," << endl;
        return;
    }
    cout << "TOP -> ";
    Node *temp = top;

    while (temp != nullptr)
    {
        cout << temp->data << "-> ";
        temp = temp->next;
    }

    cout << "NULL" << endl;

}

int main()
{
    Node *stack = nullptr;

    push(stack, 10);
    push(stack, 20);
    push(stack, 30);

    cout << "Menampilkan isi stack:" << endl;
    show (stack);

    cout << "pop;" << pop(stack) << endl;

    cout << "Menampilkan sisa Stack:" << endl;
    show(stack);

    return 0;
}
```


## Unguide

### Soal 1
> ![Screenshot bagian x](https://github.com/.png)

### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;

typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

#endif

```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
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

    while (S.top >= 0) {
        push(temp, pop(S));
    }

    S = temp;
}

```

### main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    push(S, 3);
    push(S, 4);
    push(S, 2);
    push(S, 9);
    pop(S);
    push(S, 8);
    pop(S);
    push(S, 2);
    pop(S);
    push(S, 3);
    push(S, 9);

    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
   
```

> Output
> ![Screenshot bagian x](https://github.com/.png)

Jadi kode diatas mengimplementasikan struktur data Stack (Tumpukan) menggunakan array statis berukuran 20 (MAX=20) dengan elemen bertipe integer (infotype). Header file (stack.h) mendefinisikan struktur Stack (terdiri dari array info dan penunjuk top) serta mendeklarasikan fungsi-fungsi operasinya, sementara implementasi fungsi-fungsi tersebut menangani proses LIFO (Last-In, First-Out): createStack menginisialisasi top ke -1, push menambahkan elemen setelah memeriksa apakah Stack penuh, pop mengambil dan menghapus elemen teratas setelah memeriksa apakah Stack kosong, printInfo menampilkan isi Stack dari atas ke bawah, dan balikStack menggunakan Stack sementara untuk membalikkan urutan semua elemen. Program utama (main) kemudian mendemonstrasikan fungsi-fungsi ini dengan serangkaian operasi push dan pop, diikuti dengan pencetakan isi Stack sebelum dan sesudah diproses oleh fungsi balikStack.
### Soal 2
> ![Screenshot bagian x](https://github.com/.png)

### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;
typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);

#endif

```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
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
    while (S.top >= 0) {
        push(temp, pop(S));
    }
    S = temp;
}

void pushAscending(Stack &S, infotype x) {
    Stack temp;
    createStack(temp);

    while (S.top >= 0 && S.info[S.top] > x) {
        push(temp, pop(S));
    }

    push(S, x);

    while (temp.top >= 0) {
        push(S, pop(temp));
    }
}

```

### main.cpp
```go
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

> Output
> ![Screenshot bagian x](https://github.com/.png)

Jadi code diatas mengimplementasikan struktur data Stack (Tumpukan) berbasis array statis berukuran 20, namun dengan modifikasi unik melalui fungsi pushAscending yang menjamin elemen Stack selalu terurut secara ascending (dari kecil ke besar, jika dilihat dari bawah ke atas) dengan menggunakan Stack sementara untuk menyimpan dan mengembalikan elemen yang lebih besar selama proses penyisipan. Selain fungsi standar Stack seperti createStack, pop, dan printInfo, program ini juga menyertakan fungsi balikStack untuk membalikkan urutan Stack. Program utama (main) mendemonstrasikan fungsi ini dengan memasukkan serangkaian angka yang tidak terurut menggunakan pushAscending, memverifikasi bahwa outputnya terurut, kemudian memanggil balikStack untuk menunjukkan urutan yang terbalik.

### Soal 3
> ![Screenshot bagian x](https://github.com/.png)

### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;
typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void getInputStream(Stack &S);

#endif

```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
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
    while (S.top >= 0) {
        push(temp, pop(S));
    }
    S = temp;
}

void getInputStream(Stack &S) {
    cout << "Masukkan angka (ENTER untuk selesai): ";

    char c;
    cin.get(c); 

    while (c != '\n') {     
        if (c >= '0' && c <= '9') {   
            push(S, c - '0');        
        }
        cin.get(c);
    }
}   
 
```

### main.cpp
```go
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

> Output
> ![Screenshot bagian x](https://github.com/.png)

Jadi code diatas mengimplementasikan struktur data Stack (Tumpukan) berbasis array statis berkapasitas 20, yang dirancang khusus untuk menerima dan memproses input dari pengguna: fungsi kustom getInputStream membaca karakter dari input stream hingga tombol ENTER ditekan, secara selektif mengekstrak dan mengkonversi setiap karakter digit angka menjadi integer untuk kemudian di-push ke dalam Stack, sementara karakter non-digit diabaikan. Setelah Stack terisi, program ini mencetak isinya sesuai urutan LIFO, kemudian memanggil fungsi balikStack yang menggunakan Stack sementara untuk membalikkan urutan semua elemen, dan diakhiri dengan mencetak kembali urutan Stack yang telah dibalik sebagai demonstrasi manipulasi urutan data.

## Referensi
1. https://www.w3schools.com/cpp/cpp_functions.asp
2. https://www.w3schools.com/cpp/cpp_arrays.asp
3. https://www.w3schools.com/cpp/cpp_user_input.asp
4. https://www.w3schools.com/cpp/cpp_while_loop.asp
5. https://www.w3schools.com/cpp/cpp_stacks.asp

