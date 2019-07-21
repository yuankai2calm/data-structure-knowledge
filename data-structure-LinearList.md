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



