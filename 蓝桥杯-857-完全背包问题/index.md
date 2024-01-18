# 蓝桥杯 857 完全背包问题


# 完全背包问题

## 题目

> **问题描述**
>
> 　　有一個背包，容量為M。有N種物品，每種物品有其體積Wi與價值Vi。將這些物品的一部分放入背包，每種物品可以放任意多個，要求總體積不超過容量，且總價值最大。
>
> **输入格式**
>
> 　　第一行為N, M。
> 　　之後N行，每行為Wi, Vi。
>
> **输出格式**
>
> 　　一個數，為最大價值。
>
> **样例输入**
>
> 3 20
> 15 16
> 6 6
> 7 5
>
> **样例输出**
>
> 18
>
> **数据规模和约定**
>
> 　　N, M<=1000。

## 题解

可以与01背包问题比较，区别在于01背包每件物品只能放一次，完全背包每件物品可以放多次。

解题思路：通过动态规划，求解局部最优的同时记录，在增加一个物品后更新最优解。

设第i个物品体积为w[i]，价值为v[i]， f\[i\]\[j\]表示选择前i个物品，背包剩余体积为j时的最优方案，即所选物品的最大权重和。

**解法一：**

状态转移方程

$$
f[i][j]=max(f[i-1][j-v[i]]+w[i],f[i-1][j])
$$

```java
for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                f[i][j] = f[i - 1][j];
                if (v[i] > j) {                             // 防止数组越界
                    continue;
                }
                for (int k = 0; k * v[i] <= j; k++) {
                    f[i][j] = max(f[i][j], f[i - 1][j - k * v[i]] + k * w[i]);
                }
            }
        }
```

**解法二：**

状态转移方程

$$
f[i][j]=max(f[i-1][j-v[i]]+w[i],f[i-1][j])
$$

```java
for (int i = 1; i <= n; i++) {
            for (int j = 0; j <= m; j++) {
                if (j - w[i] < 0)                                       //剩余容量为j条件下无法再加第i个了
                    continue;
                dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - w[i]] + v[i]);
            }
        }
```

**解法三：**

状态转移方程

$$
f[i][j]=max(f[i-1][j-v[i]]+w[i],f[i-1][j])
$$

```
        for(int i = 1 ; i <= n ; i++){
            for(int v = w[i]; v <= V ; v++){        // 正向枚举v
                dp[v] = max(dp[v],dp[v-w[i]] + c[i]);
            }
        }
```

写成一维形式之后和01背包完全相同，唯一的区别在于这里v的枚举顺序是**正向枚举**，而01背包的一维形式中v必须是逆向枚举。

## 代码

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader=new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer stringTokenizer=new StringTokenizer(bufferedReader.readLine());
        int N= Integer.parseInt(stringTokenizer.nextToken());
        int M= Integer.parseInt(stringTokenizer.nextToken());
        int[][] dp=new int[N+1][M+1];
        int[] w=new int[N+1];
        int[] v=new int[N+1];
        for (int i = 1; i < N+1; i++) {
            stringTokenizer=new StringTokenizer(bufferedReader.readLine());
            w[i]= Integer.parseInt(stringTokenizer.nextToken());
            v[i]= Integer.parseInt(stringTokenizer.nextToken());
        }

        for (int i = 1; i < N+1; i++) {
            for (int j = 0; j < M+1; j++) {
                if (j-w[i]<0)                                       //剩余容量为j条件下无法再加第i个了
                    continue;
                dp[i][j]=Math.max(dp[i-1][j],dp[i][j-w[i]]+v[i]);   //比较不放(dp[i-1][j])和放(dp[i][j-w[i]]+v[i])哪一个更优
            }
        }

        System.out.print(dp[N][M]);
    }
}
```

## 注意

1. 三种解法依次优化。

2. if (v[i] > j) 可以优化到 for (int j = 1; j <= m; j ++ ) 中，优化后为：

   ```java
    for (int j = v[i]; j <= m; j ++ )  {
    }
   ```

3. w[] 和 v[]可以优化掉。代码中的v和w数组使用仅限于i状态下，因此，可以定义两个变量，v和w，在for (int i = 1; i <= n; i ++ )中输入即可，优化后：

   ```java
   for (int i = 1; i <= n; i++) {
               int v, w;
               Scanner scanner = new Scanner(System.in);
               v = scanner.nextInt();
               w = scanner.nextInt();
               scanner.nextLine();
           }
   ```

4. 参考资料

   [第二讲 完全背包问题](https://www.kancloud.cn/kancloud/pack/70126)

