# 动态规划

## 基本特点
1. 是最值问题
2. 具有"最优子结构": 即整体最优解依赖于子问题的最优解
- 具有这种结构的问题常常可以用递归来解决
3. 存在"重叠子问题": 即各个子问题间有重叠部分，会导致重复计算
- 递归算法也常常有此类问题
- 可通过将中间计算结果储存下来解决
4. 从上往下分析问题，从下往上求解问题

## 求解思路
1. 写出状态转移方程，即递推公式
2. 确定初始值

## 代码框架
```c++
// 定义dp数组
vector<int> dp(n,init_val);
// 确定初始状态
dp[0] = val1
dp[1] = val2
...
// 根据状态转移方程，给dp数组赋值
for(auto val: dp){
  //...
}

// 返回的是dp数组中储存额结果
```

## 实例
### 零钱兑换(leetcode322 )
> 问题：给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

>示例:
```
输入: coins = [1, 2, 5], amount = 11
输出: 3
解释: 11 = 5 + 5 + 1
```

>解法：
```c++
int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount+1,amount+1);
        dp[0] = 0;
        for(int i = 1; i <= amount; i++){
            for(auto coin: coins){
                if(i - coin < 0) continue;
                dp[i] = min(dp[i] , 1 + dp[i-coin]);
            }
        }
        return ( dp[amount] == amount+1) ? -1 : dp[amount];
    }
```
