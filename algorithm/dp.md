# <center> DP 题目汇总 </center>

记录一些遇到过的dp问题



DP(Dynamic Programming) 一种解决最优化问题的算法思想。

要求： **重叠子问题** && **最优子结构**



- 递归： 记忆化搜索

- 递推： 自底向上





[toc]



#### 最大连续子序和

```c
dp[i] = max{A[i], dp[i-1] + A[i]}
```



#### 最长不下降子序列

```c
dp[i] = max{1, dp[j] + 1}  (贪心也可以)
```



#### 最长公共子序列（LCS）

```c
dp[i][j] = dp[i-1][j-1] + 1, A[i] == B[j]
    		max{dp[i-1][j], dp[i][j-1], A[i] != B[j]}
```



#### 最长回文子串

```c
dp[i][j] = dp[i+1][j-1], S[i] == S[j]
    		0, S[i] != S[j]
```



#### 01 背包问题

```c
d[i][v] = max{dp[i-1][v], dp[i-1][v-w[i]] + c[i]}
```



#### 完全背包问题

```c
dp[i][v] = max{dp[i-1], dp[i][v - w[i]] + c[i]}
```



#### 非相连最大和

```c
sum(k) = max(sum(k – 2) + A[k], sum(k – 1))
```

##### leetcode 打家劫舍