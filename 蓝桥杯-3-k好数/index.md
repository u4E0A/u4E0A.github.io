# 蓝桥杯 3 K好数

# K好数

## 题目

> **问题描述**
>
> 如果一个自然数N的K进制表示中任意的相邻的两位都不是相邻的数字，那么我们就说这个数是K好数。求L位K进制数中K好数的数目。例如K = 4，L = 2的时候，所有K好数为11、13、20、22、30、31、33 共7个。由于这个数目很大，请你输出它对1000000007取模后的值。
>
> **输入格式**
>
> 输入包含两个正整数，K和L。
>
> **输出格式**
>
> 输出一个整数，表示答案对1000000007取模后的值。
>
> **样例输入**
>
> 4 2
>
> **样例输出**
>
> 7
>
> **数据规模与约定**
>
> 对于30%的数据，KL <= 106；
>
> 对于50%的数据，K <= 16， L <= 10；
>
> 对于100%的数据，1 <= K,L <= 100。

## 题解

该题可以使用动态规划。使用二维数组dp\[L\]\[K\]保存计算过程，其中dp\[i\]\[j\]表示i位K进制数（从第0位开始计）以j开头符合K好数规则的数的个数。

状态转移方程为：

$$
dp[i][j]=\sum ^{k-1}_{k=0} dp[i-1][k]-dp[i-1][j-1]-dp[i-1][j+1]
$$
由样例可知对四进制数01、02、03不看作K好数，即有效的数不能以0开头，所以需要对dp\[i\]\[0\]做特殊处理。

## 代码

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer stringTokenizer = new StringTokenizer(bufferedReader.readLine());
        int K = Integer.parseInt(stringTokenizer.nextToken());
        int L = Integer.parseInt(stringTokenizer.nextToken());
        int[][] dp = new int[L][K];
        for (int i = 0; i < K; i++) {
            dp[0][i] = 1;
        }
        for (int i = 1; i < L; i++) {
            for (int j = 0; j < K; j++) {

                for (int k = 0; k < K; k++) {
                    if (Math.abs(j - k) != 1)
                        dp[i][j] = (dp[i][j] + dp[i - 1][k]) % 1000000007;
                }
            }
        }

        int out = 0;
        for (int i = 1; i < K; i++) {
            out = (out + dp[L - 1][i]) % 1000000007;
        }
        System.out.println(out);
    }
}
```

## 注意

1. 注意循环的起始条件，dp\[i\]\[0\]不能因为数<font color=Silver>0ABCDEF……</font>无效就简单赋值为0，因为dp\[i+1\]\[2\]包含dp\[i\]\[0\]，此时这个i+1位数是有效的。正确的做法是在计算结果时从dp\[L-1\]\[1\]开始。
