# 链表的基本操作
## 定义
```c++
typedef int elemtype;
struct ListNode{
  elemtype val;
  ListNode next;//也可用指针
  ListNode(elemtype v): val(v),next(nullptr){}
};
```
------
## 基本操作
### 插入
```c++
//在节点p 后面插入节点s
s->next = p->next;
p->next = s;
```
### 交换两个节点位置
```c++
//交换 p2 和 p3
// p1 -> p2 -> p3 -> p4 -> ... -> null
p1->next = p2->next;//让 p1 指向 p3
p2->next = p2->next->next;//让 p2 指向 p4
p2->next->next = p2;//让 p3 指向 p2
```
### 反转链表
```c++
while(cur){
  next= cur->next;//保留下一个节点
  cur->next = pre;//指向前一个节点
  pre = cur;//前一个节点往后挪
  cur = next;//后一个节点往后挪
}
```
### 递归遍历
```c++
void traverse(ListNode *head){
  if(!head)
    return;
  traverse(head->next);
}
```
