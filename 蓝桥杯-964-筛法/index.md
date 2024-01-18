# 蓝桥杯 964 筛法


# 筛法

## 题目

> **问题描述**
>
> 　　炫炫学了筛法之后，很想用筛法求欧拉函数。他决定求1到N的所有数的欧拉函数值。
>
> **输入格式**
>
> 　　输入的第一行包含1个整数n,。
>
> **输出格式**
>
> 　　输出若干行，每行包含一个整数，第i行表示i的欧拉函数值
>
> **样例输入**
>
> 2
>
> **样例输出**
>
> 1
> 1
>
> **数据规模和约定**
>
> 　　n<=500000

## 题解

该题考查素数筛。素数筛有埃氏筛（the Sieve of Eratosthenes，埃拉托色尼筛）和欧拉筛（the Sieve of Euler，也叫线性筛）。可以通过筛出1~N的所有素数来求解欧拉函数。

求欧拉函数数值有公式：

$$
\phi(n)=\prod^r_{i=1}(\frac{p_i-1}{p_i})
$$
其中任何一个大于1的自然数n,如果n不为质数，那么n可以唯一分解成有限个质数的乘积

$$
n=p_1^{k_1}p_2^{k_2}\dots p_r^{k_r}
$$
根据线性筛同时求解欧拉函数值，可以根据三条性质来求解

$$
设p为素数，有如下关系：\\
\phi(p)=p-1\\
p与i互素 \ \phi(p \cdot i)=\phi(p)\cdot \phi(i)\\
p为i的质因数 \  \phi(p \cdot i)=p \cdot \phi(i)
$$


## 代码

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    public static int[] eulerSet;                   //eulerSet[i]对应i的欧拉函数值
    public static boolean[] isComposite;            //如果i为合数，isComposite[i]为true
    public static int[] primeSet;                   //存储算出的素数
    public static int cnt = 0;                      //算出的素数个数

    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(bufferedReader.readLine());
        eulerSet = new int[n + 1];
        primeSet = new int[n];
        isComposite = new boolean[n + 1];
        getPrime(n);
        for (int i = 1; i < n + 1; i++) {
            System.out.println(eulerSet[i]);
        }
    }

    public static void getPrime(int n) {            //欧拉筛（线性筛）判断是否为素数，同时记录欧拉函数值
        eulerSet[1] = 1;
        for (int i = 2; i <= n; i++) {
            if (!isComposite[i]) {                  //若i为质数
                primeSet[cnt] = i;                  //将质数i记录
                cnt++;
                eulerSet[i] = i - 1;                //欧拉函数为i-1
            }

            for (int j = 0; primeSet[j] * i <= n; j++) {
                isComposite[primeSet[j] * i] = true;
                if (i % primeSet[j] == 0) {                                     //primeSet[j]为i的最小质因数，同时也为primeSet[j]*i的最小质因数
                    eulerSet[primeSet[j] * i] = eulerSet[i] * primeSet[j];
                    break;                                                      //算完最小的质因数，后面再算会产生重复
                }
                eulerSet[primeSet[j] * i] = eulerSet[i] * (primeSet[j] - 1);    //primeSet[j]不为i的最小质因数，primeSet[j]与i互素
            }
        }
    }
}
```

## 注意

1. 考虑到时间复杂度，需要使用欧拉筛。
2. 我一开始的思路是先求解1~n的所有素数，再对每一个数做质因数分解，根据公式求每一个数的欧拉函数值，然而超时。故转为在筛选素数的同时计算每一个数的欧拉函数值。

