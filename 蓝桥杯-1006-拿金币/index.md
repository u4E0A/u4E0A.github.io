# 蓝桥杯 1006 拿金币


# 拿金币

## 题目

> **问题描述**
>
> 　　有一个N x N的方格,每一个格子都有一些金币,只要站在格子里就能拿到里面的金币。你站在最左上角的格子里,每次可以从一个格子走到它右边或下边的格子里。请问如何走才能拿到最多的金币。
>
> **输入格式**
>
> ​		第一行输入一个正整数n。
> ​		以下n行描述该方格。金币数保证是不超过1000的正整数。
>
> **输出格式**
>
> 最多能拿金币数量。
>
> **样例输入**
>
> 3
> 1 3 3
> 2 2 2
> 3 1 2
>
> **样例输出**
>
> 11
>
> **数据规模和约定**
>
> ​		n<=1000

## 题解

可以判断此题属于动态规划题。用一个二维数组存储输入，并加以处理即可。由于只能向左或向右，通过计算得到一个新的二维数组，其中a\[i\]\[j\]表示在此位置的最优路径的各节点权重之和。**可以通过按行从左往右依次遍历原数组，比较每一个元素的左元素和上元素，取二者权重较大的和该元素生成新元素的值。**即

```java
array[i][j] += Math.max(array[i][j - 1], array[i - 1][j])
```

最终右下角元素的值就是答案。

## 代码

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        int n=Integer.parseInt(bufferedReader.readLine());
        int[][] array=new int[n+1][n+1];
        for (int i = 1; i < n+1; i++) {
            String s =bufferedReader.readLine();
            StringTokenizer stringTokenizer = new StringTokenizer(s);
            for (int j = 1; j < n + 1; j++){
                array[i][j]=Integer.parseInt(stringTokenizer.nextToken());
            }
        }

        for (int i = 1; i < n+1; i++) {
            for (int j = 1; j < n + 1; j++) {
                array[i][j] += Math.max(array[i][j - 1], array[i - 1][j]);
            }
        }
        System.out.println(array[n][n]);
    }
}
```

## 注意

1. 小技巧：**使用BufferedReader类**。一开始我使用Scanner类输入数据，提交显示**内存超限**。通过查询，发现BufferedReader类在内存使用方面消耗更少，于是用BufferedReader类代替了Scanner类。

2. Scanner类和BufferedReader类不能混用，猜测是由于缓冲区的原因。一旦使用Scanner类读取输入（我这里是使用Scanner类读取了n的值，BufferedReader类尝试读取其它数据），则BufferedReader类只能读取到新输入的字符串（即无法读取其它数据），导致结果报错。

