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

### 判断链表是否有换
```c++
// 经典解法，龟兔赛跑法
class Solution {
public:
bool hasCycle(ListNode * head) {
    ListNode * fast = head, * slow = head;
    while(slow && fast && fast->next){
        slow = slow->next;
        fast = fast->next->next;
        if(slow == fast){
            return true;
        }
    }
    return false;
}
```

### 判断链表是否有环，并返回环的入口
常规解法：蚂蚁探路法
```c++
class Solution {
public:
  //蚂蚁探路法
  ListNode * detectCycle(ListNode * head) {
      unordered_set<ListNode * > passed_node;//储存经过的节点
      ListNode * node = head;
      while(node){
          if(passed_node.find(node) != passed_node.end())
              return node;
          passed_node.insert(node);
          node = node->next;
      }
      return nullptr;
  };
```

经典解法：龟兔赛跑法
```c++
class Solution {
public:
  // 经典解法
  ListNode * detectCycle(ListNode * head){
      ListNode * ptr1 = findIntersection(head);
      if(!ptr1)
          return nullptr;
      ListNode * ptr2 = head;
      while(ptr2 != ptr1){
          ptr1 = ptr1->next;
          ptr2 = ptr2->next;
      }
      return ptr1;
  }

  ListNode *findIntersection(ListNode *head){
      ListNode * slow = head, * fast = head;
      while(slow && fast && fast->next){
          slow = slow->next;
          fast = fast->next->next;
          if(slow == fast){
              return slow;
          }
      }
      return nullptr;
  }
};
```
