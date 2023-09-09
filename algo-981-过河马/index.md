# 算法 ALGO 981 过河马


# 试题 算法训练 过河马

## 题目

> **问题描述**
>
> 　　在那个过河卒逃过了马的控制以超级超级多的走法走到了终点之后，这匹马表示它不开心了……
> 　　于是，终于有一天，它也过河了！
> 　　由于过河马积累了许多的怨念，所以这次它过了河之后，再也没有什么东西可以限制它，它可以自由自在的在棋盘上驰骋。一开始，它是在一个n行m列棋盘的左下角（1,1）的位置，它想要走到终点右上角（n，m）的位置。而众所周知，马是要走日子格的。可是这匹马在积累了这么多怨念之后，它再也不想走回头路——也就是说，它只会朝向上的方向跳，不会朝向下的方向跳。
> 　　那么，这匹马它也想知道，它想从起点跳到终点，一共有多少种走法呢？
>
> **输入格式**
>
> 　　第一行两个数n，m，表示一个n行m列的棋盘，马最初是在左下角（1,1）的位置，终点在右上角（n，m）的位置。
>
> **输出格式**
>
> 　　输出有一行，一个数表示走法数。由于答案可能很大，所以输出答案除以1000000007所得的余数即可。
>
> **样例输入**
>
> 4 4
>
> **样例输出**
>
> 2
>
> **数据规模和约定**
>
> 　　n<=100,m<=100

## 题解

由于题目规定马只能朝上跳，所以不会存在循环的情况，且棋盘第1行易知不可到达。可用动态规划，即棋盘的某一位置(i,j)只能由其下面的四个位置到达。通过二维数组来记录每个位置的走法数，设\[i\]\[j\]的值为走法数，有如下递推关系：

$$
[i][j]=[i-1][j-2]+[i-1][j+2]+[i-2][j-1]+[i-2][j+1]
$$
只要在程序中判断来源的四个位置是否合法即可。

## 代码

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {

    public static void main(String[] args) {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer stringTokenizer = null;
        int n, m;
        try {
            stringTokenizer = new StringTokenizer(bufferedReader.readLine());
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        n = Integer.parseInt(stringTokenizer.nextToken());
        m = Integer.parseInt(stringTokenizer.nextToken());
        long[][] dp = new long[n][m];
        dp[0][0] = 1;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (i - 1 > -1 && j - 2 > -1)                               //i-1<n&&i-1>-1&&j-2>-1&&j-2<m
                    dp[i][j] = (dp[i][j] + dp[i - 1][j - 2]) % 1000000007;
                if (i - 1 > -1 && j + 2 > -1 && j + 2 < m)                  //i-1<n&&i-1>-1&&j+2>-1&&j+2<m
                    dp[i][j] = (dp[i][j] + dp[i - 1][j + 2]) % 1000000007;
                if (i - 2 > -1 && j - 1 > -1)                               //i-2<n&&i-2>-1&&j-1>-1&&j-1<m
                    dp[i][j] = (dp[i][j] + dp[i - 2][j - 1]) % 1000000007;
                if (i - 2 > -1 && j + 1 < m)                                //i-2<n&&i-2>-1&&j+1>-1&&j+1<m
                    dp[i][j] = (dp[i][j] + dp[i - 2][j + 1]) % 1000000007;
            }
        }
        System.out.println(dp[n - 1][m - 1] % 1000000007);
    }
}
```

## 注意

由于n<=100,m<=100，输入较大时结果用int类型会溢出，建议使用long类型，且在运算过程中取余。

## 拓展

同样是马走日，如果没有限定只能朝上跳，那么无法计算出所有走法了。

算法-ALGO-1001-跳马

