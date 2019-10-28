## 队列

### 什么是队列

队列（Queue）：具有一定操作约束的线性表

插入和删除操作：只能在一端插入，而在另一端删除。FIFO

### 队列的顺序存储实现

队列的顺序存储结构通常由一个一维数组和一个记录队列头元素位置的变量`front`以及一个记录队列尾元素位置的变量`rear`组成。

```c
#define MaxSize <储存数据元素的最大个数>
struct QNode{
    ElementType Data[MaxSize];
    int rear;
    int front;
};
typedef struct QNode *Queue;
```

### 顺环队列

略

### 队列的链式存储实现

队列的链式存储结构也可以用一个单链表实现。插入和删除操作分别在链表的两头进行。

```c
struct Node{
    ElementType Data;
    struct Node *Next;
};
struct QNode{
    struct Node *rear;            //指向队尾结点
    struct Node *front;           //指向队头结点
};
typedef struct QNode *Queue;
Queue PtrQ;
```

不带头结点的链式队列出队操作的一个实例

```c
ElementType DeleteQ(Queue PtrQ){
    struct Node *FrontCell;
    ElementType FrontElem;
    if(PtrQ->front == NULL){
            printf("队列空");
            return ERROR;
        }
        FrontCell = PtrQ->rear;
        if(PtrQ->front == PtrQ->rear)
            PtrQ->front = PtrQ->rear = NULL;
        else
            PtrQ->front = PtrQ->front->Next;
        FrontElem = FrontCell->Data;
        free(FrontCell);
        return FrontElem;
}
```
