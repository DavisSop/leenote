# 50 Pow(x, n)

[leetcode链接](https://leetcode-cn.com/problems/powx-n/)

## 题目

实现 pow(x, n) ，即计算 x 的 n 次幂函数。

示例 1:

```txt
输入: 2.00000, 10
输出: 1024.00000
```

示例 2:

```txt
输入: 2.10000, 3
输出: 9.26100
```

示例 3:

```txt
输入: 2.00000, -2
输出: 0.25000
解释: 2^2 = 1/2^2 = 1/4 = 0.25
```

说明:

- -100.0 < x < 100.0
- n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。

## 解题思路

这个题常用解法可以有：

- 暴力解法，即循环一直乘即可，时间复杂度是O(n)
- 快速幂 + 递归，即x^n = (x^n/2) * (x^n/2)，时间复杂度是O(log(n))

注意点：

1. 当n是负数的时候，需要一些数学知识，进行以下计算，比如 x^-2 = (1/x)^2，即x=1/x，n = -n
2. 不需要考虑溢出
3. 注意边界条件

### 暴力解法

```java
public double myPow(double x, int n) {
    if (n == 0) {
        return 1.0;
    }
    if (n < 0) {
        x = 1 / x;
        n = -n;
    }
    double pow = 1.0;
    for (int i = 0; i < n; i ++) {
        pow = pow * x;
    }
    return pow;
}
```

这个使用测试用例得到的结果是对的，但是超出了时间限制

### 快速幂 + 递归

```java
public double myPow(double x, int n) {
    if (n < 0) {
        x = 1 / x;
        n = -n;
    }
    return fastPow(x, n);
}

public double fastPow(double x, int n) {
    if (n == 0) {
        return 1.0;
    }
    double halfPow = fastPow(x, n / 2);
    if(n % 2 == 0) {
        // 偶数
        return halfPow * halfPow;
    }else {
        // 奇数
        return halfPow * halfPow * x;
    }
}
```

### 其他解法

1. 快速幂 + 迭代，这个比较难理解，可以参考[官方题解](https://leetcode-cn.com/problems/powx-n/solution/powx-n-by-leetcode-solution/)
2. 牛顿迭代法，纯数学方法，有空的时候了解即可
