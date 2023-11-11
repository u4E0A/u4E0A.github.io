# 信息安全数学基础 第一章 整除


# 第一章 整除

1. $\forall a,b,c \in Z$

   - $a|b,b|c \implies a|c$
   - $a|b,a|c \iff \forall x,y \in Z ,a|bx+cy$
   - $m\neq 0 ,a|b \iff ma|mb$
   - $a|b,b|a \implies a=\pm b$

2. $\exist a,b \in Z,a\neq 0 \implies \exist_{=1} q,r\in Z ,0\le r < |a|,b=aq+r$

3. $\forall a,b,c \in Z$

   - $gcd(a,b)=gcd(b,a)=gcd(-a,b)=gcd(a,-b)$
   - $a|b \implies gcd(a,b)=a$
   - $\forall a,b\in Z,gcd (a,b)|ax+by$
   - $\forall a,b\in Z ,\exist x,y \in Z ,gcd(a,b)=xa+yb$
   - $\exist a,b,c,q\in Z ,a=bq+c\implies gcd (a,b)=gcd(b,c)$
   - $gcd \left ( \frac{a}{gcd(a,b)},\frac{b}{gcd(a,b)} \right)=1$
   - $\exist a,b,m \in Z,a|m,b|m \implies lcm[a,b]|m$

4. 辗转相除法

   - $\exist a,b,c,q\in Z ,a=bq+c\implies gcd (a,b)=gcd(b,c)$
   - 当 $a,b$中有负整数时，可将其中的负整数转变为正整数来求其最大公因数。

5. $\forall a,b\in Z ,\exist x,y \in Z ,gcd(a,b)=xa+yb$

   - 设 $a,b$ 是两个不全为 0 的整数，$gcd(a,b)=1\iff \exist u,v \in Z ,ua+vb=1$

6. $\exist a,b,c \in Z^+$

   - $c|ab,gcd(a,c)=1\implies c|b$
   - $a|c,b|c,gcd(a,b)=1 \implies ab|c$
   - $gcd(a,c)=1,gcd(b,c)=1 \implies gcd(ab,c)=1$

7. $\exist a,b \in Z^+$

   - 若 $a,b$ 互素 $\implies lcm[a,b]=ab$
   - $lcm[a,b]=\frac {ab}{gcd(a,b)}$

8. $\exist p \in P,\exist a,b \in Z$

   - $p \nmid a \implies $ $p$ 与 $a$ 互素
   - $p|a_1a_2\cdots a_k \implies \exist p|a_i$

9. **算数基本定理**

   $\forall n \in Z^+-\{0,1\} $可唯一表示为$n=p_1^{\alpha_1}p_2^{\alpha_2}\cdots p_k^{\alpha_k}$

10. 素数有无穷多个

11. Eratosthenes筛法

    - 设 $n$ 是一个正合数，$p$ 是 $n$ 的大于1的最小正因数，则 $p$ 是素数且 $p\leq \sqrt{n}$
    - 设 $n$ 是一个正整数。如果对于所有的素数 $p\leq \sqrt{n}$ ，都 有 $p\nmid n$ ，则 $n$ 是素数

12. Mersenne 素数

    - 设 $n\geq1$ 是一个正整数，若 $a^n-1$ 是素数，则 $a=2,n$ 是素数

13. 如果 $b\ge 2$ 为整数，那么任意正整数 $n$ 都可以**唯一**表示为
    $$
    a=a_nb^n+a_{n-1}b^{n-1}+\cdots + a_1b+a_0(b^0)
    $$
    其中 $a_i$ 是整数，$0\le a_i < b,0\leq i\le n,a_n\neq 0$。以 $b$ 为基，或 $b$ 进制。

    正整数 的以 为基的表示通常可写成
    $$
    a=(a_na_{n-1}\cdots a_1a_0)_b
    $$

