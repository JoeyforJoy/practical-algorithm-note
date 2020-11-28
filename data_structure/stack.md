# 栈的基本操作
## c++ 实现
```c++
#include <stack>
stack<int> s;
s.push(a);// 入栈
int res = s.top();// 返回栈顶元素
s.pop();// 删除栈顶元素，但不返回该元素值
```

## 例题
### 有效括号(Leetcode20)
> 问题：给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。
有效字符串需满足：
  左括号必须用相同类型的右括号闭合。
  左括号必须以正确的顺序闭合。
  注意空字符串可被认为是有效字符串。

> 解法：
```c++
#include <unordered_map>
class Solution {
public:
    bool isValid(string s) {
        //哈希表
        unordered_map<char,char> right_map = {{')','('},  {'}','{'}, {']','['}};
        stack<char> stk;
        for(auto c: s){
            if(right_map.find(c) == right_map.end()) stk.push(c);
            else{
                if(!stk.empty() && right_map[c] == stk.top())
                    stk.pop();
                else
                    return false;
            }
        }
        return stk.empty();
    }
};
```

### 用栈来实现队列(Leetcode232)
