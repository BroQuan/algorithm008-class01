学习笔记
# 爬楼梯问题总结 
## 经典爬楼梯问题：
## [leetcode 70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/submissions/)
### 题目描述：
&emsp;&emsp;假设你正在爬楼梯。需要 n 阶你才能到达楼顶。每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

### 示例：
示例 1：

输入： 
```
2
```
输出： 
```
2
```
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶

示例 2：

输入：
```
3
```
输出： 
```
3
```
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
### 解题思路：
1. 傻递归
2. 记忆化递归
3. 动态规划
4. 数学通项公式

### 参考代码：
1. 傻递归
``` java
//傻递归    超出时间限制
class Solution {
    public int climbStairs(int n) {
        if (n == 1)
            return 1;
        if (n == 2)
            return 2;
        return climbStairs(n - 1) + climbStairs(n - 2);
    }
}
```
2. 记忆化递归
``` java
//记忆化递归
public class Solution {
    public int climbStairs(int n) {
        int []mem = new int[n + 1];
        return climbStairs(0, n, mem);
    }
    public int climbStairs(int i, int n, int mem[]) {
        if (i > n)
            return 0;
        if (i == n)
            return 1;
        if (mem[i] != 0)
            return mem[i];
        mem[i] =  climbStairs(i + 1, n, mem) + climbStairs(i + 2, n, mem);
        return mem[i];
    }
}
```
3. 动态规划
``` java
class Solution {
    public int climbStairs(int n) {
        int i, j;
        i = 1;
        j = 2;
        if (n == 1) {
            return i;
        }
        if (n == 2) {
            return j;
        }
        for (int k = 3; k <= n; ++k) {
            int sum = i + j;
            i = j;
            j = sum;
        }
        return j;
    }
}
```
4. 通项公式
``` java
//斐波那契通项公式
public class Solution {
    public int climbStairs(int n) {
        double sqr_5 = Math.sqrt(5);
        double res = (Math.pow((1 + sqr_5) / 2, n + 1) - Math.pow((1 - sqr_5) / 2, n + 1)) / sqr_5;
        return (int) res;
    }
}
```

## 爬楼梯变形
### 题目描述：
&emsp;&emsp;假如每次可以跨越1 - 3级台阶，且两次跨越台阶数不能相等，请问到n层共有几种方法？
### 解题思路：
&emsp;&emsp;i, j 表示从上次通过跨越 j + 1 步到达第 i 层

动态转移方程：   
&emsp;&emsp;dp[i][j] = 1    if (i == j + 1)   
&emsp;&emsp;dp[i][j] = sum(dp[i - j - 1][k])    others and k != j
每次步长不得与上次相同，最大取3
``` java
//leetcode上面，爬楼梯问题不符合常识，题目按照从第0层往上爬，那我们还是按照他题意来写
class Solution {
    private int sum(int []nums) {
        int ans = 0;
        for (int i : nums)
            ans += i;
        return ans;
    }
    public int climbStairs(int n) {
        if (n == 0) return 0;
        int[][] dp = new int[n + 1][3];
        for (int i = 1; i <= n; ++i) {
            for (int j = 0; j < 3 && j < i; ++j) {
                if (i == j + 1)
                    dp[i][j] = 1;
                else
                    dp[i][j] = sum(dp[i - j - 1]) - dp[i - j - 1][j];
            }
        }
        return sum(dp[n]);
    }
}
```

### 进阶
&emsp;&emsp;如果每次最大跨越台阶数为m，且两次跨越台阶数不能相等，则到达第n级台阶共有几种方法？   

动态转移方程：   
&emsp;&emsp;dp[i][j] = 1    if (i == j + 1)   
&emsp;&emsp;dp[i][j] = dp[i - j - 1][0] + dp[i - j - 1][1] + ··· + dp[i - j - 1][j - 1] + dp[i - j - 1][j + 1] + dp[i - j - 1][m - 1] 
``` java
class Solution {
    private int sum(int []nums) {
        int ans = 0;
        for (int i : nums)
            ans += i;
        return ans;
    }
    public int climbStairs(int n, int m) {
        if (n == 0) return 0;
        int[][] dp = new int[n + 1][m];
        for (int i = 1; i <= n; ++i) {
            for (int j = 0; j < m && j < i; ++j) {
                if (i == j + 1)
                    dp[i][j] = 1;
                else
                    dp[i][j] = sum(dp[i - j - 1]) - dp[i - j - 1][j];
            }
        }
        return sum(dp[n]);
    }
}
```