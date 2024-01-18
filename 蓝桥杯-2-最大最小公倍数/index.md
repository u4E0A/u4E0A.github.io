# 蓝桥杯 2 最大最小公倍数


# 最大最小公倍数

## 题目

> **问题描述**
>
> 已知一个正整数N，问从1~N中任选出三个数，他们的最小公倍数最大可以为多少。
>
> **输入格式**
>
> 输入一个正整数N。
>
> **输出格式**
>
> 输出一个整数，表示你找到的最小公倍数。
>
> **样例输入**
>
> 9
>
> **样例输出**
>
> 504
>
> **数据规模与约定**
>
> 1 <= N <= 106。

## 题解

该题考查的是贪心算法。首先考虑何种情况下可以构造一个比较大的最小公倍数，容易想到当三数互素或其最大公约数较小的时候最小公倍数较大。

考虑N、N-1、N-2，当N为奇数时，三者显然互素。因为三者的因数最大为N-(N-2)=2，而由于N和N-2均为奇数，故其最小公约数为1。

当N为偶数时，比较N\*(N-1)\*(N-2)/2和N\*(N-1)\*(N-3)，显然后者较大，但可能存在gcd(N,N-3)=3。

当N有因数3时，比较N\*(N-1)\*(N-3)/3和(N-1)\*(N-2)\*(N-3)，显然后者较大，即存在三种情况：

1. N为奇数

   ```java
   out = (long) N * (N - 1) * (N - 2);
   ```

2. N为偶数且被3整除

   ```java
   out = (long) (N - 1) * (N - 2) * (N - 3);
   ```

3. N为偶数且不被3整除

   ```java
   out = (long) N * (N - 1) * (N - 3);
   ```

## 代码

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(bufferedReader.readLine());
        long out = 0;
        if (N % 2 == 1) {
            out = (long) N * (N - 1) * (N - 2);
        } else {
            if (N % 3 == 0)
                out = (long) (N - 1) * (N - 2) * (N - 3);
            else
                out = (long) N * (N - 1) * (N - 3);
        }
        System.out.println(out);
    }
}
```

