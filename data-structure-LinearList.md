#### ���Ա�

##### 1. ����
> ���Ա����߼��ṹ, ˳���������Ǵ洢�ṹ, �����ǲ�ͬ��ĸ���,�����

���Ա�: �Ǿ�����ͬ�������͵�n(n >= 0)������Ԫ�ص���������.
һ���ʾ:
    L = (a0, a1, a2, a3, ...ai, a(i+1), ..., an);

���Ա���������:   
    - ���Ա��е�Ԫ��������ͬ  
    - �����޸�Ԫ�ع���  
    - Ԫ����λ���й�, ÿ��Ԫ�ض���һ����Ӧ�����    
    

##### 2. ���Ա�Ļ�������
һ�����ݻ����Ļ��������������������Ĳ���, �������Ӳ��������ɻ���������ʵ�ֵ�.
���Ա�Ļ�����������:

```
//��ʼ����
InitList(&L)

//����
Length(L)

//���ұ�L�йؼ���e��Ӧ��Ԫ��λ��
LocateElem(L, e)

//�������, �ڱ�L�е�iλ�ò���Ԫ��e
ListInsert(&L, i, e)

//ɾ������
ListDelete(&L, i, &e)

//��ȡԪ��
GetElem(L, i)

PrintList(L)

Empty(L)

DestroyList(&L);
```
##### 3. ���Ա��˳��洢�ṹ�Լ�ʵ��

- ���Ա��˳��洢ʵ��,�ֳ�Ϊ˳���, �߼�����Ԫ������������洢��Ԫ��
Ҳ����.  

- ˳���Ԫ��λ���1��ʼ, �����е�Ԫ���±��0��ʼ

- ˳�����ص�: 
���Խ��������ȡ, ��ͨ���׵�ַ�Լ�Ԫ����ſ�����O(1)��ʱ�����ҵ�ָ����Ԫ��
, ˳���Ĵ洢�ܶȸ�, ÿ���ڵ�ֻ�洢����Ԫ��, ����, ˳����߼������ڵ�����������
��Ҳ�����ڵ�,���Բ���, ɾ��������Ҫ�ƶ�����Ԫ��.

- ���Ա�Ĵ洢������������:

�̶����鳤�ȵ�˳���ṹ:
```dtd
# define MaxSize = 50;           //˳������󳤶�
typedef struct { 
    ElemType data[MaxSize];      //˳����Ԫ��
    Int length;                  //˳���ĵ�ǰ����
} SqList;                        //˳�������Ͷ���

```

��̬����洢��˳���ṹ:

```dtd
#define InitSize = 100
typedef struct {
    ElemType *data;
    init MaxSize,length;
} SeqList;

```
��ʼ��̬�������Ϊ:
```dtd
L.data=(ElemType*)malloc(sizeof(ElemType)*InitSize);
```

##### 4. ˳���Ļ�������

- �������

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
��õ�����ڱ�β����(i = n + 1), Ԫ�غ�����佫��ִ��,ʱ�临�Ӷ�ΪO(1);  
���������ڱ�ͷ����(i = 1), Ԫ�غ�����佫ִ��n��, ʱ�临�Ӷ�ΪO(n);  
ƽ�����ʱ���ƶ�ÿ���ڵ�ĸ�����ͬ, n/2��, ʱ�临�Ӷ�Ҳ��O(n)

- ɾ������

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

ɾ��������Ͳ�������һ��,ʱ�临�Ӷȷ�Ϊ����, ƽ����O(n)

- ��ֵ����

```dtd
int locateElem(SqList &L, ElemType e) {
    int j;
    for(j = 0; j < L.length; j ++)
        if(L.data[j] == e) 
               return j + 1;
        return 0;        
    
}
```
��ֵ���ҵ�ʱ�临�Ӷ�ΪO(n)

##### 5. ���Ա����ʽ�洢�����Լ�ʵ��

����˳���Ĳ���,ɾ��������Ҫ�ƶ�����Ԫ��,Ӱ��Ч��.
��ʽ�洢��Ҫ���߼������ڵ�����Ԫ��������λ����Ҳ����.����ͨ��"��"
����������Ԫ��֮����߼���ϵ,���, �����Ա�Ĳ���, ɾ������Ҫ�ƶ�Ԫ��, ֻ��Ҫ
�޸�ָ��.

- ������

ÿ���ڵ�, ���˴��Ԫ���������Ϣ֮��, ����Ҫ���һ��ָ�����̵�ָ��.

������ڵ�������������:

```dtd
typedef struct LNode {
    ElemType data;
    struct LNode *next;
}LNode, *LinkList;
```

��������Ҫ�����������洢�ռ�, ���ǵ�������Ҫ����洢ָ����.
���ڵ�����Ľڵ�����ɢ�ֲ��ڴ洢�ռ��е�, ���Ե������Ƿ������ȡ��.
ֻ�ܴӱ�ͷ��ʼ����,���β���.

- ������Ļ�������
����͸�巨����������

```dtd
LinkList createList(LinkList &L) {
    LNode *s; int x;
    L = (LinkList)malloc(sizeof(LNode)); //ͷ���
    L->next = NULL;                     //��ʼ��ͷ���
    scanf("%d", &x);
    while(x != 9999) {
        s = (LNode*)malloc(sizeof(LNode)); //�����½ڵ�
        s->data = x;
        s-> next = L-> next;
        L ->next = s;
        scanf("%d", &x);
    }
    return L;
    
}
```



