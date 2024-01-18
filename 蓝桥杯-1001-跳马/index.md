# 蓝桥杯 1001 跳马

# 跳马

## 题目

> **问题描述**
>
> 　　一个8×8的棋盘上有一个马初始位置为(a,b)，他想跳到(c,d)，问是否可以？如果可以，最少要跳几步？
>
> **输入格式**
>
> 　　一行四个数字a,b,c,d。
>
> **输出格式**
>
> 　　如果跳不到，输出-1；否则输出最少跳到的步数。
>
> **样例输入**
>
> 1 1 2 3
>
> **样例输出**
>
> 1
>
> **数据规模和约定**
>
> 　　0<a,b,c,d≤8且都是整数。

## 题解

使用DFS搜索，退出条件为：

1. 搜索步数大于目前的最小步数
2. 调到目标位置，记录步数
3. 遍历所有结果，每一个可到达位置都走过了（最坏，即不可到达）

可以将一些变量保存为静态变量，而不是在递归函数中声明，也不是通过形参传入，目的是减少内存消耗，同时使方法间可以共享信息。

## 代码

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    public static int result = -1;
    public static int x0, y0, x1, y1;
    public static int[][] array = new int[9][9];
    public static int[][] horse = {% raw %} {{2, 1}, {1, 2}, {-1, 2}, {-2, 1}, {1, -2}, {2, -1}, {-1, -2}, {-2, -1}}; {% endraw %}

    public static void main(String[] args) {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        try {
            StringTokenizer stringTokenizer = new StringTokenizer(bufferedReader.readLine());
            x0 = Integer.parseInt(stringTokenizer.nextToken());
            y0 = Integer.parseInt(stringTokenizer.nextToken());
            x1 = Integer.parseInt(stringTokenizer.nextToken());
            y1 = Integer.parseInt(stringTokenizer.nextToken());
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        array[x0][y0] = 1;
        dfs(x0, y0, 0);
        System.out.println(result);
    }

    public static void dfs(int x, int y, int step) {
        if (result != -1)
            if (step >= result)
                return;
        if (x == x1 && y == y1) {
            result = step;
            return;
        }
        int xTemp, yTemp;
        for (int i = 0; i < 8; i++) {
            xTemp = x + horse[i][0];
            yTemp = y + horse[i][1];
            if (xTemp > 0 && xTemp <= 8 && yTemp > 0 && yTemp <= 8) {
                if (array[xTemp][yTemp] == 0) {
                    array[xTemp][yTemp] = 1;
                    dfs(xTemp, yTemp, step + 1);
                    array[xTemp][yTemp] = 0;
                } else return;
            }
        }
    }
}
```

## 注意

1. 需要一个二维数组保存DFS中走过的位置，在递归后恢复为走过的状态。**其中起始位置一定是走过的**。
2. **一定要剪枝**，否则无论输入为何，计算过程中都会将所有可能路径完整计算一遍，**肯定超时**。
3. **注意该题的棋盘是有范围的**，一开始想通过不定方程组来求解，理论上不存在不能到达的位置。但由于该题棋盘有限，该方法不建议使用。

## 拓展

算法-ALGO-981-过河马
