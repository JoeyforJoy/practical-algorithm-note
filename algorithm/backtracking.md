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

### N皇后问题
> 问题：设计一种算法，打印 N 皇后在 N × N 棋盘上的各种摆法，其中每个皇后都不同行、不同列，也不在对角线上。这里的“对角线”指的是所有的对角线，不只是平分整个棋盘的那两条对角线。

> 示例：
```
输入：4
 输出：[[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
 解释: 4 皇后问题存在如下两个不同的解法。
[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
```
> 解法：
```c++
vector<vector<string>> solveNQueens(int n) {
    vector<vector<string>> res;
    vector<string> board(n,string(n,'.'));
    backtrack(res,board,0);
    return res;
}

void backtrack(vector<vector<string>> &res,
               vector<string> &board,int row){
    if(board.size() == row){//棋盘满了
        res.push_back(board);
        return;
    }

    int n = board.size();
    for(int col = 0; col < n; col++){
        if(!isValid(board,row,col)){//落子无效
            continue;
        }
        //选择
        board[row][col] = 'Q';
        backtrack(res,board,row+1);//进入下一决策
        //撤销选择
        board[row][col] = '.';
    }
}

bool isValid(const vector<string> &board, int row, int col){
    int n = board.size();
    int cl = col-1;
    int cr = col+1;
    //同一列，左上，右上有没有
    for(int r = row-1; r >= 0; r--){
        if(board[r][col] == 'Q'){
            return false;//同一列没有
        }
        if(cl >= 0 && board[r][cl] == 'Q'){
            return false;//左上没有
        }
        if(cr < n && board[r][cr] == 'Q'){
            return false;//右上没有
        }
        cl--;cr++;
    }
    return true;
}
```

### 字母大小写全排列(Leetcode784)
> 问题： 给定一个字符串S，通过将字符串S中的每个字母转变大小写，我们可以获得一个新的字符串。返回所有可能得到的字符串集合。

> 示例：
```
输入: S = "a1b2"
输出: ["a1b2", "a1B2", "A1b2", "A1B2"]

输入: S = "3z4"
输出: ["3z4", "3Z4"]

输入: S = "12345"
输出: ["12345"]

```
> 解法：
```c++
class Solution {
public:
    vector<string> letterCasePermutation(string S) {
        vector<string> res;
        // S 的长度不超过12
        if(S.size() > 12) return res;
        // S 仅由数字和字母组成
        for(auto c: S){
            if(!isalnum(c)) return res;
        }
        //回溯算法
        backtrace(res, S, S.begin());
        return res;
    }
    void backtrace(vector<string> &res, string &S, string::iterator begin){
        if(begin == S.end()){
            res.push_back(S);
            return;
        }

        *begin = tolower(*begin);
        backtrace(res, S, begin + 1);
        *begin = toupper(*begin);
        if(isalpha(*begin)){
            backtrace(res, S, begin + 1);
            *begin = tolower(*begin);
        }
    }
};
```
