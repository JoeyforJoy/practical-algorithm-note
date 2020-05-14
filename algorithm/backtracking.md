# 回溯法

## 基本原理
- 遍历所有可能的决策，暴力搜索
- [详细介绍](https://github.com/labuladong/fucking-algorithm/blob/master/%E7%AE%97%E6%B3%95%E6%80%9D%E7%BB%B4%E7%B3%BB%E5%88%97/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95%E8%AF%A6%E8%A7%A3%E4%BF%AE%E8%AE%A2%E7%89%88.md)
![](https://github.com/labuladong/fucking-algorithm/blob/master/pictures/backtracking/5.jpg)

## 算法框架
```python
for 选择 in 选择列表:
    # 做选择
    将该选择从选择列表移除
    路径.add(选择)
    backtrack(路径, 选择列表)
    # 撤销选择
    路径.remove(选择)
    将该选择再加入选择列表
```

## 实例
### 全排列问题
> 问题：输入一个字符串，打印出该字符串中字符的所有排列。你可以以任意顺序返回这个字符串数组，>但里面不能有重复元素。

>实例:
```
输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
```

> 解法
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
        if(begin == s.end()){
            res.push_back(s);
        }
        for(auto cur = begin; cur != s.end(); cur++){
            if(judge(s,begin,cur)){
                continue;
            }

            swap(*cur,*begin);
            permutation(res,s,begin+1);
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
