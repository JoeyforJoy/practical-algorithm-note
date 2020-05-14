# 回溯法

## 基本原理
- 遍历所有可能的决策，暴力搜索
- 三要素：路径、选择列表、结束条件
- [详细介绍](https://github.com/labuladong/fucking-algorithm/blob/master/%E7%AE%97%E6%B3%95%E6%80%9D%E7%BB%B4%E7%B3%BB%E5%88%97/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95%E8%AF%A6%E8%A7%A3%E4%BF%AE%E8%AE%A2%E7%89%88.md)
![](https://github.com/labuladong/fucking-algorithm/blob/master/pictures/backtracking/5.jpg)
- 类似算法：递归、树的遍历、图的遍历

## 算法框架
```python
result = []
def backtrack(路径, 选择列表):
    if 满足结束条件:
        result.add(路径)
        return

    for 选择 in 选择列表:
        //选择前还可剪枝，
        做选择
        backtrack(路径, 选择列表)
        撤销选择
```

## 实例

### 全排列问题：以字符串排列为例(《剑指offer》面试题38)
> 问题：输入一个字符串，打印出该字符串中字符的所有排列。你可以以任意顺序返回这个字符串数组，>但里面不能有重复元素。

>示例:
```
输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
```

> 解法:
```c++
class Solution {
public:
    vector<string> permutation(string s) {
        vector<string> res;
        if(s.size() == 0){
            return res;
        }
        permutation(res,s,s.begin());

        return res;
    }

private:
    void permutation(vector<string> &res, string &s, string::iterator begin){
        //终止条件
        if(begin == s.end()){
            res.push_back(s);
        }
        for(auto cur = begin; cur != s.end(); cur++){
            //剪枝条件,如果当前节点已经遍历过，则不遍历
            if(judge(s,begin,cur)){
                continue;
            }
            //选择
            //s的[begin,end)为当前的选择列表,[0,begin)为当前节点的路径
            //其中,begin为当前节点的选择列表的首元素，下一节点路径的尾元素
            //交换cur和begin,则便可在将当前节点加入下一个节点的路径
            swap(*cur,*begin);
            permutation(res,s,begin+1);//遍历子节点
            //撤销选择
            swap(*cur,*begin);
        }
    }

    bool judge(string &s,string::iterator b, string::iterator e){
        for(auto it = b; it != e; it++){
            if((*it) == (*e)) return true;
        }
        return false;
    }
};
```

### 八皇后问题
> 问题：

> 示例：

> 解法：
