# 算法 ALGO 999 数的潜能


# 试题 算法训练 数的潜能

## 题目

> **问题描述**
>
> 　　将一个数N分为多个正整数之和，即N=a1+a2+a3+…+ak，定义M=a1*a2*a3*…*ak为N的潜能。
> 　　给定N，求它的潜能M。
> 　　由于M可能过大，只需求M对5218取模的余数。
>
> **输入格式**
>
> 　　输入共一行，为一个正整数N。
>
> **输出格式**
>
> 　　输出共一行，为N的潜能M对5218取模的余数。
>
> **样例输入**
>
> 10
>
> **样例输出**
>
> 36
>
> **数据规模和约定**
>
> 　　1<=N<10^18

## 题解

该题为找规律题。

先尝试从比较小的数开始分解，得到其最大的分解方法：

| N    | 最大的分解方法       |
| ---- | -------------------- |
| 1    | 就是1本身            |
| 2    | 就是2本身            |
| 3    | 就是3本身            |
| 4    | 就是4本身，或者是2+2 |
| 5    | 2+3                  |
| 6    | 3+3                  |
| 7    | 4+3=2+2+3            |
| 8    | 2+3+3                |
| 9    | 3+3+3                |
| 10   | 2+2+3+3              |
| 11   | 2+3+3+3              |
| 12   | 3+3+3+3              |
| 13   | 2+2+3+3+3            |
| 14   | 2+3+3+3+3            |

可以发现除去1以后，分解具有如下规律：

1. 尽量3进行分解
2. 如果3分解有余，则用剩余部分用2分解

同时发现若分解成9+9的形式可以减少计算，计算时间更长，但实现更简单，原理同快速幂算法。

可以使用快速幂算法进行幂运算，此处不赘述。

## 代码

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    public static void main(String[] args) {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        long N;
        try {
            N = Long.parseLong(bufferedReader.readLine());
        } catch (IOException e) {
            throw new RuntimeException(e);
        }

        if (N < 4) {
            System.out.println(N);
            return;
        }

        int rest = (int) (N % 3);
        int result = 0;
        if (rest == 0) {
            N /= 3;
            result = qpow(3, N, 5218);
        } else if (rest == 1) {
            N = (N - 4) / 3;
            result = (qpow(3, N, 5218) * 4) % 5218;
        } else {
            N = (N - 2) / 3;
            result = (qpow(3, N, 5218) * 2) % 5218;
        }

        System.out.println(result);
    }

    public static int qpow(long b, long e, int mod) {	\\快速幂
        int result = 1;
        while (e != 0) {
            if ((e & 1) == 1)
                result = (int) ((result * (b % mod)) % mod);
            b = (b * b) % mod;
            e >>= 1;
        }
        return result;
    }
}
```

## 注意

1. 对1~3需要进行特判。
2. 由于输入的数可能比较大，所以应该使用long关键字。
3. 分解后进行累乘时，由于指数可能比较大，推荐使用快速幂，或将数分解为9+9的形式，结果相同。
4. 快速幂函数中推荐每一步都取余，防止数溢出。

