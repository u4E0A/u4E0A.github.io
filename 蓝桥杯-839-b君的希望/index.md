# 蓝桥杯 839 B君的希望


# B君的希望

## 题目

> **问题描述**
>
> 　　你有个同学叫B君，他早听闻祖国河山秀丽，列了一张所有可能爬的山的高度表，因“人往高处走”的说法，所以他希望要爬的山按照表上的顺序，并且爬的每一座山都要比前一座高，爬的山数最多，请贵系的你帮他解决这个问题。(cin,cout很坑)
>
> **输入格式**
>
> 　　输入第一行为num(1~1000)和maxHeight(1~8848)，代表山的个数和最大高度
> 　　输入第二行有num个整数，代表表上每座山的高度height(1~maxHeight)
>
> **输出格式**
>
> 　　输出只有一个数，为符合要求的最大爬山数
>
> **样例输入**
>
> 10 10
> 8 6 8 5 9 5 2 7 3 6 3 4
>
> **样例输出**
>
> 3
>
> **样例输入**
>
> 10 20
> 8 19 9 10 3 3 15 3 10 6
>
> **样例输出**
>
> 4
>
> **数据规模和约定**
>
> 　　num(1~1000)，maxHeight(1~8848)，height(1~maxHeight)，都是正整数

## 题解

观察代码注释。

思路是记录局部最佳方案的值，再比较是否能在已有的方案上进一步增长递增序列长度。

## 代码

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer stringTokenizer=new StringTokenizer(bufferedReader.readLine());
        int num= Integer.parseInt(stringTokenizer.nextToken());         //只需要num，不需要保留maxHeight
        stringTokenizer=new StringTokenizer(bufferedReader.readLine());
        int[] mounts=new int[num];
        int[] re=new int[num];                  //re[i]记录mounts[0]~mounts[i]的最长递增序列长度
        for (int i = 0; i < num; i++) mounts[i] = Integer.parseInt(stringTokenizer.nextToken());

        re[0]=1;                                //可以爬mount[0]本身
        int out=1;                              //目前全局最优为1
        for (int i = 1; i < num; i++) {
            int max=0;                          //最坏方案为0，同时也是目前的局部最优
            for (int j = 0; j < i; j++) {
                if(mounts[j]<mounts[i]){        //意味着到mounts[j]的方案还可能被优化，即加上mounts[i]
                    max=Math.max(max,re[j]);    //判断是否更新目前的最优方案
                }
            }
            re[i]=max+1;                        //re[i]包括mounts[i]本身，必然+1
            out=Math.max(out,re[i]);            //在计算过程中保留全局最优
        }

        System.out.print(out);
    }
}
```

## 注意

1. 可以在计算过程中保留全局最优。

