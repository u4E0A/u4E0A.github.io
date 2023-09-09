# 算法 ALGO 835 盾神与格子游戏

# 试题 算法训练 盾神与格子游戏

## 题目

> **问题描述**
>
> 　　在盾神很小很小还不会怎样编程的时候，他迷上了一款风靡一时的双人游戏！游戏双方在地上画n个格子，然后在最后一格放上一颗石头。每人每轮可以把石头向前移动1到3格，最后谁把石头移出第一格就赢了。盾神那时候很傻很天真，每次都是随便乱玩，结果每次都会输。。。
> 　　盾神今天回想起来，那时候的自己真是弱暴了！！！今天的盾神不仅一眼把这个游戏的必胜方法秒解，还提出了一个进化版：每人每轮不是把石头向前移动1到3格那么简单，而是有m种选择：第i种可以向前移动ai格。其他规则还是和以前一样。那么聪明的你，能告诉盾神，如果双方都采取最优策略，先手第一步该怎样做才可以保证必胜？
>
> **输入格式**
>
> 　　第一行为两个数n，m。
> 　　第二行m个数，表示ai。
>
> **输出格式**
>
> 　　如果先手必败，输出“poor dun”，否则输出先手第一步应该向前移动多少格，如果有多种方案，选择移动距离最少的那个。
>
> **样例输入**
>
> 6 3
> 1 10 100
>
> **样例输出**
>
> 10
>
> **样例输入**
>
> 6 3
> 1 2 3
>
> **样例输出**
>
> 2
>
> **样例输入**
>
> 6 3
> 1 1 1
>
> **样例输出**
>
> poor dun
>
> **数据规模和约定**
>
> 　　对于20％的数据，ai为从1到m的连续整数。
> 　　对于另外30％的数据，n<=20,m<=3。
> 　　对于100％的数据，n<=100000,m<=100,0<ai<=100000。

## 题解

## 代码

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
    public static int[] choices;
    public static int[] sgArray;

    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer stringTokenizer = new StringTokenizer(bufferedReader.readLine());
        int n = Integer.parseInt(stringTokenizer.nextToken());
        int m = Integer.parseInt(stringTokenizer.nextToken());
        stringTokenizer = new StringTokenizer(bufferedReader.readLine());

        sgArray = new int[n + 1];
        choices = new int[m];
        for (int i = 0; i < m; i++) {
            choices[i] = Integer.parseInt(stringTokenizer.nextToken());
        }
        Arrays.sort(choices);

        sgArray[choices[0]] = choices[0];
        for (int i = 1; i < n + 1; i++) {
            for (int j = 0; j < m; j++) {
                if (i - choices[j] < 0 || sgArray[i - choices[j]] == 0) {
                    sgArray[i] = 1;
                    break;
                }
            }
        }

        for (int firstStep : choices) {
            if (n - firstStep < 0 || sgArray[n - firstStep] == 0) {
                System.out.println(firstStep);
                return;
            }
        }
        System.out.println("poor dun");
    }
}
```

