#### 线性表

##### 1. 定义
> 线性表是逻辑结构, 顺序表和链表是存储结构, 两者是不同层的概念,勿混淆

线性表: 是具有相同数据类型的n(n >= 0)个数据元素的有限序列.
一般表示:
    L = (a0, a1, a2, a3, ...ai, a(i+1), ..., an);

线性表三个特征:   
    - 线性表中的元素类型相同  
    - 由有限个元素构成  
    - 元素与位置有关, 每个元素都有一个对应的序号    
    

##### 2. 线性表的基本操作
一个数据机构的基本操作是最核心最基础的操作, 其他复杂操作都是由基本操作来实现的.
线性表的基本操作如下:

```
//初始化表
InitList(&L)

//表长度
Length(L)

//查找表L中关键字e对应的元素位置
LocateElem(L, e)

//插入操作, 在表L中的i位置插入元素e
ListInsert(&L, i, e)

//删除操作
ListDelete(&L, i, &e)

//获取元素
GetElem(L, i)

PrintList(L)

Empty(L)

DestroyList(&L);
```
##### 3. 线性表的顺序存储结构以及实现

- 线性表的顺序存储实现,又称为顺序表, 逻辑数据元素相邻在物理存储单元上
也相邻.  

- 顺序表元素位序从1开始, 数组中的元素下标从0开始

- 顺序表的特点: 
可以进行随机存取, 即通过首地址以及元素序号可以在O(1)的时间内找到指定的元素
, 顺序表的存储密度高, 每个节点只存储数据元素, 但是, 顺序表逻辑上相邻的数据在物理
上也是相邻的,所以插入, 删除操作需要移动大量元素.

- 线性表的存储类型描述如下:

固定数组长度的顺序表结构:
```dtd
# define MaxSize = 50;           //顺序表的最大长度
typedef struct { 
    ElemType data[MaxSize];      //顺序表的元素
    Int length;                  //顺序表的当前长度
} SqList;                        //顺序表的类型定义

```

动态分配存储的顺序表结构:

```dtd
#define InitSize = 100
typedef struct {
    ElemType *data;
    init MaxSize,length;
} SeqList;

```
初始动态分配语句为:
```dtd
L.data=(ElemType*)malloc(sizeof(ElemType)*InitSize);
```

##### 4. 顺序表的基本操作

- 插入操作

```dtd
bool ListInsert(SqList &L, int i, ElemType e) {
    if(i < 1 || i > L.length + 1)
        return false;
    if(L.length >= MaxSize)
        return false;
    for(int j=L.length; j >= i; j--)
        L.data[j] = L.data[j - 1];
        L.data[i -1] = e;
        L.length++;
        return true;     
}
```
最好的情况在表尾插入(i = n + 1), 元素后移语句将不执行,时间复杂度为O(1);  
最坏的情况是在表头插入(i = 1), 元素后移语句将执行n次, 时间复杂度为O(n);  
平均情况时间移动每个节点的概率相同, n/2次, 时间复杂度也是O(n)

- 删除操作

```dtd
bool ListDelete(SqList &L, int i, ElemType e) {
    if(i < 1 || i > L.length + 1)
        return false;
    e = L.data[i - 1];
    for(int j=i; j < L.length; j++)
        L.data[j - 1] = L.data[j];
    L.length--;
    return true;        
}
```

删除的情况和插入的情况一样,时间复杂度分为最好最坏, 平均是O(n)

- 按值查找

```dtd
int locateElem(SqList &L, ElemType e) {
    int j;
    for(j = 0; j < L.length; j ++)
        if(L.data[j] == e) 
               return j + 1;
        return 0;        
    
}
```
按值查找的时间复杂度为O(n)

##### 5. 线性表的链式存储机构以及实现

由于顺序表的插入,删除操作需要移动大量元素,影响效率.
链式存储不要求逻辑上相邻的两个元素在物理位置上也相邻.而是通过"链"
建立起数据元素之间的逻辑关系,因此, 对线性表的插入, 删除不需要移动元素, 只需要
修改指针.

- 单链表

每个节点, 除了存放元素自身的信息之外, 还需要存放一个指向其后继的指针.

单链表节点类型描述如下:

```dtd
typedef struct LNode {
    ElemType data;
    struct LNode *next;
}LNode, *LinkList;
```

单链表不需要大量的连续存储空间, 但是单链表需要额外存储指针域.
由于单链表的节点是离散分布在存储空间中的, 所以单链表是非随机存取的.
只能从表头开始遍历,依次查找.

- 单链表的基本操作
采用透插法来创建链表

```dtd
LinkList createList(LinkList &L) {
    LNode *s; int x;
    L = (LinkList)malloc(sizeof(LNode)); //头结点
    L->next = NULL;                     //初始化头结点
    scanf("%d", &x);
    while(x != 9999) {
        s = (LNode*)malloc(sizeof(LNode)); //创建新节点
        s->data = x;
        s-> next = L-> next;
        L ->next = s;
        scanf("%d", &x);
    }
    return L;
    
}
```
- 采用尾插法创建链表

```aidl
LinkList createList(LinkList &L) {
    LNode *s; *r = L: // r为表尾指针
    int x;
    L = (LinkList)malloc(sizeof(LNode));//头结点
    L -> next = NULL;
    scanf("%d", &x);
    while(x != 999) {
        s = (LNode*)malloc(sizeof(LNode));//创建新结点
        s->data = x;
        r->next = s;
        r = s;// r指向新的表尾结点
    
    }

}
```

- 按照序号查找结点

```aidl
LNode *GetElem(LinkList L, int i) {
    
    int j = 1;
    LNode *p=L->next;
    if(i == 0)
        return L; //如果i=0, 返回头结点
    if(i < 1)
        return NULL;
    while(p&&(j < i)) { //从第一个结点开始查找， 查找到第i个结点
        p = p->next;
        j++;
    }
    return p;        
}

```

- 按值查找

```
LNode *LocateElem(LinkList L, ElemType e) {
   LNode *p = L;
   while(p != NULL && p->data != e) {
        p = p -> next;
   }
   return p;

}
```

- 删除结点操作(删除位置为i的结点)

```aidl
p = GetElem(L, i - 1); //查找到要删除结点的前驱结点

q = p->next;

p->next = q->next; //将删除结点的下一个结点赋值为删除结点的上一个结点
free(q) 

```


- 双链表

双链表增加了一个直接指向前驱的prior指针。单链表只有一个指向其后继的指针， 这使得单链表只能从头结点
依次顺序地向后遍历。

双链表的结点类型描述:

```aidl
typedef struct DNode {
    ElemType data;
    struct DNode *prior, *next;

} DNode, *DLinkList;
```

- 双链表插入操作(将结点*s插入到结点*p之后)

```aidl
q = p->next;
q->prior = s;
s->next = q;
p->next = s;
s->prior = p;
```


- 双链表的删除操作(删除双链表中*p的后继结点*q)
```aidl
p->next = q -> next;
q->next->prior = q;
free(q);

```


- 循环链表
1. 循环单链表和单链表的区别在于， 表中最后一个结点的指针不是NULL, 而改为指向头结点， 从而整个
表形成一个环。
在循环单链表中， 表尾结点*r的next域指向L， 故表中没有指针域为NULL的结点。因此
循环单链表的判空条件不是头结点的指针是否为空， 而是它是否等于头指针。

2. 循环双链表

在带头结点的循环双链表L中， 某个结点*p为尾结点时， p->next==L； 当循环双链表为空表时， 其头结点
的prior域和next域都等于L;

- 静态链表

静态链表是借助数组来描述线性表的链式存储结构， 结点也有数据域data和指针域next, 与前面所讲的链表
中的指针不同的是， 这里的指针是结点的相对位置(数组下标)， 又成为游标。和顺序表一样， 静态链表需要预先分配
一块连续的内存空间。

```aidl
#define MaxSize 50
typedefine struct {
    ElemType data;
    int next;

} SLinkList[MaxSize];
```


##### 6. 顺序存储和链式存储的对比


- 存取方式:

   顺序表可以顺序存取， 随机存取， 而链表只能从表头依次存取。


- 逻辑结构和物理结构

  采用顺序存储时， 逻辑上相邻的元素， 在物理内存上也是相邻的。
而采用链式存储， 逻辑上相邻的元素， 在物理内存上则不一定相邻。


- 查找、插入和删除操作

 1. 查找
对于按值查找， 顺序表在无序状体下时间复杂度都是O(n);
顺序表有序时候， 可以采用折半查找，时间复杂度为O(log2n), 
顺序表有序情况， 按下标查找时间复杂度为O(1);
链表的事件复杂度为O(n)

 2. 删除和插入

    顺序表在插入或删除时候， 平均要移动半表的元素， 时间复杂度为O(n),
而链表只需要修改结点而指针即可。


- 空间分配

    顺序表：  
        1. 存储在静态分配的内存下， 一旦存储空间装满不能扩充， 如果再加入新元素， 将会出现内存溢出。  
        2. 预先分配的内存过大， 可能导致顺序表后部大量闲置。  
        3. 动态分配内存虽然可以扩充， 但是会导致大量元素移动，效率低下，而且若内存中没有更大块的连续空间，则会分配失败
        
    链表：  
        1. 链式存储的结点空间只在需要的时候申请分配， 只要内存有空间就可以分配， 操作灵活、高效。    



##### 7. 如何选择存储结构

- 基于存储的考虑

    对于线性表的长度或存储规模难以估计时， 不宜采用顺序表；链表不用事先估计存储规模， 但链表的存储密度较低， 显然链式存储结构
    的存储密度是小于1的。
    
- 基于运算的考虑

    插入和删除操作为， 链表的效率更高。
    按序号访问和随机访问， 顺序表的效率更高。
    
- 基于环境

    顺序表的实现， 比较容易， 任何高级语言都有数组。而链表的操作是基于指针的， 相对复杂。        