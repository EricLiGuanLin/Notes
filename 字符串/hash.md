#! https://zhuanlan.zhihu.com/p/600710976
# 字符串哈希

## 哈希的基本介绍

字符串哈希的目的是把一个字符串映射到一个值上，通过比较值来判断字符串是否相等。

字符串哈希是基于Base和Mod两个素数，用多项式的方式计算的，所以我们可以使用类似快速幂的方法计算。

## 下文的约定

```c++
#define ull unsigned long long
 
ull Base;
ull hash[MAXN], p[MAXN];
 
hash[0] = 0;
p[0] = 1;
```

这里的hash数组表示子串$[0,i]$的哈希值，$p[i]$表示$Base^{i}$，所以我们把$hash[0]$初始化为0，$p[0]$初始化为1。

## 单哈希与双哈希

### 单哈希的方法

单哈希只对字符串做一次哈希，其递推公式为$hash[i] = (hash[i - 1] * Base + str[i]) \% MOD$，我们通过迭代的方式就可以算出每一个子串的哈希值了。

#### 避免冲突的方法

在这里，想要避免冲突，我们要尽量把MOD和Base取大。

常用的Base是131，模数是$1e9 + 7$、$1e9+9$、$19260817$、$998244353$

### 双哈希

双哈希就是用两个模数和两个素数对一个字符串算两次哈希，得到一个pair，用pair做比较，避免哈希碰撞。

