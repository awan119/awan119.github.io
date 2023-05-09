---
title: "[筆記] Linked Lists & Binary Lists"
date: 2023-05-01 11:28:15
tags:
- [筆記]
- [linked lists]
categories:
- [資料結構]
---


本人從來沒有認真學習過資料結構，想慢慢重新學習這些。

> 以下內容都是詢問 ChatGPT 做出的回答

# 陣列（Arrays）與連結串列（Linked Lists）
## 陣列（Arrays）

陣列是一種有限長度、具有固定大小的資料結構，它可以存儲一系列具有相同數據型別的元素。在陣列中，每個元素都可以通過一個唯一的索引值來訪問。例如，下面是一個包含5個整數的陣列：
<!-- more -->

```
int array[5] = {1, 2, 3, 4, 5};
可以使用以下方法來訪問陣列中的元素：

// 訪問第3個元素，即3
int x = array[2];

// 將第1個元素設置為6
array[0] = 6;
```

陣列的優點是可以快速訪問元素，但**缺點**是它們的大小是固定的，因此當需要存儲的元素超出陣列大小時，就需要重新分配一個更大的陣列。

## 連結串列（Linked Lists）

連結串列是一種動態資料結構，它可以用於動態地增加和刪除元素。在連結串列中，每個元素都被稱為節點（node），每個節點都包含數據和一個指向下一個節點的指標。下面是一個包含3個整數的連結串列：

```
Copy code
struct Node {
    int data;
    struct Node* next;
};

struct Node* head = NULL;
head = (struct Node*)malloc(sizeof(struct Node));
head->data = 1;
head->next = (struct Node*)malloc(sizeof(struct Node));
head->next->data = 2;
head->next->next = (struct Node*)malloc(sizeof(struct Node));
head->next->next->data = 3;
head->next->next->next = NULL;
```

# Linked list
TBD
```
#include <stdio.h>
#include <stdlib.h>

// 定義一個節點結構
struct Node{
    int data;
    struct Node* next; //每個節點包含當前節點的 data 還有指向下一個節點的地址
};

// 創建一個新節點
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*) malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}

//筆記  Node** 因為希望是修改指針本身的地址，而非修改地址中的值
//因此用雙重指針，這樣可以直接修改節點的位址，不用再 return 值
void append(stuct Node** headRef, int data){
    
    //先創建 data 節點
    struct Node* newNode = createNode(data);

    //新增節點在第一個節點之後
    if (*headRef == NULL){
        *headRef = newNode;  
        return;
    }

    stuct Node* current = *headRef;//宣告 current 紀錄當前的地址
    while (current->next != NULL){
        current = current->next;
    }
    current->next = newNode;
}

// 將 Linked Lists 內容 print 出來 ////////////////// TBD
void printLinkedList(struct Node* head) {
    struct Node* current = head;
    while (current != NULL) {
        printf("%d ", current->data);
        current = current->next;
    }
}

int main(){
    struct Node* head = NULL; //建立第一個節點
    
    //增加後續的節點
    append(&head, 1);
    append(&head, 2);
    append(&head, 3);
    ////////////////// TBD
    // 將 Linked Lists 內容 print 出來
    printf("Linked List contents: ");
    printLinkedList(head);

    return 0;
}
```

## Binary tree in Linked list
以下是我詢問 ChatGPT 提供我一個如何將 Binary tree 印出來的方法

```
#include <stdio.h>
#include <stdlib.h>

// 建立二元樹的節點結構
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// 新增一個節點
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// 遞迴地輸出二元樹的節點值，前序
void printTree(struct Node* node) {
    if (node == NULL) {
        return;
    }
    printf("%d ", node->data);
    printTree(node->left);
    printTree(node->right);
}

//中序
void printInorder(struct Node* node) {
    if (node == NULL) {
        return;
    }
    printInorder(node->left);
    printf("%d ", node->data);
    printInorder(node->right);
}

//後序
void printPostorder(struct Node* node) {
    if (node == NULL) {
        return;
    }
    printPostorder(node->left);
    printPostorder(node->right);
    printf("%d ", node->data);
}


int main() {
    // 建立二元樹
    struct Node* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);
    root->right->left = createNode(6);
    root->right->right = createNode(7);

    // 輸出二元樹的節點值
    printf("前序 Binary Tree: ");
    printTree(root);
    printf("\n");
    printf("中序 Binary Tree: ");
    printInorder(root);
    printf("\n");
    printf("後序 Binary Tree: ");
    printPostorder(root);
    printf("\n");

    return 0;
}

```
範例中 Binary Tree 的樣貌為
<blockquote class="imgur-embed-pub" lang="en" data-id="a/1zsrayK"  ><a href="//imgur.com/a/1zsrayK">Data structure</a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

結果為：
```
前序 Binary Tree: 1 2 4 5 3 6 7 
中序 Binary Tree: 4 2 5 1 6 3 7 
後序 Binary Tree: 4 5 2 6 7 3 1 
```

# Reference
1. Leetcode 程式解題基礎：linked list 和 binary tree
   https://www.mropengate.com/2017/12/leetcode-linked-list-binary-tree.html
2. 二元樹(Binary Tree)基礎
   https://kopu.chat/%E4%BA%8C%E5%85%83%E6%A8%B9/


# Extension

## mallos
malloc 是一個 C 語言的標準函式庫，用於**動態分配記憶體**。在上面的程式碼中，malloc 用於動態分配連結串列的節點結構，因為在建立連結串列時，我們不知道需要多少個節點。因此，我們使用 malloc 函式來動態分配節點的記憶體空間。

malloc 函式會返回一個指向已分配的記憶體空間的指標。在上面的程式碼中，我們使用 (struct Node*)malloc(sizeof(struct Node)) 來分配一個大小為 struct Node 結構的記憶體空間，並將其轉換為 struct Node* 型別的指標。

需要注意的是，當使用 malloc 函式動態分配記憶體時，必須在使用完畢後釋放它，以避免記憶體洩漏。在上面的程式碼中，我們沒有釋放已分配的記憶體空間，這是不好的程式習慣。通常，我們可以使用 free 函式來釋放已分配的記憶體空間。例如，釋放一個已分配的節點記憶體可以使用以下程式碼：
```
free(new_node);
```
建議在使用 malloc 和 free 函式時要注意記憶體管理，以避免發生記憶體洩漏或記憶體錯誤等問題。