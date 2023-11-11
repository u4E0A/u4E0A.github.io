# 信息安全数学基础 第二章 同余


# 第二章 同余

1. $a\equiv b(mod \ m) \iff \exist k \in Z ,a=km+b$

2. $a=k_1m+r_1,b=k_2m+r_2,0\leq r_1 <m,0\leq r_2 <m,a\equiv b(mod \ m ) \iff r_1=r_2$

3. $\exist a,b,c,m \in Z^+$

   - 自反性：$a\equiv a (mod \ m)$
   - 对称性：$a\equiv b(mod \ m)\implies b\equiv a (mod \ m)$
   - 传递性：$a\equiv b(mod \ m),b\equiv c(mod \ m)\implies a\equiv c (mod \ m)$

4. $\exist a,b,d,a_1,a_2,b_1,b_2,m \in Z^+$

   - $a_1 \equiv a_2 (mod \ m),b_1 \equiv b_2 (mod \ m)\implies a_1+b_1 \equiv a_2+b_2 (mod \ m)$
   - $a_1 \equiv a_2 (mod \ m),b_1 \equiv b_2 (mod \ m)\implies a_1-b_1 \equiv a_2-b_2 (mod \ m)$
   - $a_1 \equiv a_2 (mod \ m),b_1 \equiv b_2 (mod \ m)\implies a_1a_2 \equiv b_1b_2 (mod \ m)$
   - $ad\equiv bd (mod \ m) ,(d,m)=1\implies a \equiv b(mod \ m )$
   - $a \equiv b(mod \ m)$，$d$ 是 $a,b,m$ 的任意公因数 $\implies \frac ad \equiv \frac bd (mod \ \frac md)$
   - $a \equiv b (mod \ m ),d|m \implies a\equiv b(mod \ d)$
   - $a \equiv b(mod \ m_i),i=1,2,\cdots ,k\implies a \equiv b (mod \ lcm [m_1,m_2,\cdots ,m_k])$

5. 对于给定的正整数 $m$ ，有且恰有 $m$ 个不同的模 $m$ 的剩余类。

6. $\exist m \in Z^+ ,\exist a \in Z,\forall b \in Z ,gcd(a,m)=1$，若 $x$ 遍历模 $m$ 的一个完全剩余系，则 $ax+b$ 也 遍历模 $m$ 的一个完全剩余系

7. $\exist m_1,m_2 \in Z^+，gcd(m_1,m_2)=1$，若 $x$ 遍历模 $m_1$ 的一个完全剩余系，$y$ 遍历模 $m_2$ 的一个完全剩余系，则 $m_1y+m_2x$ 也遍历模 $m_1m_2$ 的一个完全剩余系

8. 在模 $m$ 的一个剩余类当中，如果有一个数与 $m$ 互素，则该剩余类中所有的数均与 $m$ 互素，这时称该剩余类与 $m$ 互素。

9. 与 $m$ 互素的剩余类的个数称为欧拉函数，记为 $\varphi(m)$ 等于 $Z_m$ 当中与 $m$ 互素的数的个数。对于任意一个素数 $p$ ，$\varphi(m)=p-1$ 。

10. $\exist m \in Z^+ ,\exist a \in Z,gcd(a,m)=1$，若 $x$ 遍历模 $m$ 的一个既约剩余系，则 $ax$ 也遍历模 $m$ 的一个既约剩余系

11. $\exist m_1,m_2 \in Z^+，gcd(m_1,m_2)=1$，若 $x$ 遍历模 $m_1$ 的一个既约剩余系，$y$ 遍历模 $m_2$ 的一个既约剩余系，则 $m_1y+m_2x$ 也遍历模 $m_1m_2$ 的一个既约剩余系

12. $\exist m,n\in Z,gcd(m,n)=1 \implies \varphi(mn)=\varphi (m)\varphi(n)$

13. $\exist p_i \in P,\exist m=p_1^{e_1}p_2^{e_2}\cdots p_k^{e_k} \implies \varphi(m)=m \prod^k_{i=1}(1-\frac1{p_i})$

14. $\exist m \in Z^+,r \in Z_m,gcd(r,m)=1 \implies \exist s \in Z_m , rs \equiv 1(mod \ m)$

15. **欧拉定理**

    $\exist m \in Z^+,r\in Z_m ,gcd(r,m)=1 \implies r^{\varphi(m)}\equiv 1(mod \ m)$

16. **费马小定理**

    $\forall p\in P,a\in Z \implies a^p \equiv a(mod \ p)$

17. Miller–Rabin概率素数测试

    - $p$ 为素数时，费马小定理成立；$p$ 为合数时，费马小定理不一定成立（不成立则必为合数）
    - $p$ 为奇素数，$x^2 \equiv 1 (mod \ p)$ 的解只有 $x\equiv \pm 1 (mod \ p)$

18. $\forall p \in P,r_1,r_2,\cdots ,r_{p-1} \in Z^*_p \implies \prod ^{p-1}_{i=1}r_i \equiv -1\equiv p-1(mod \ p)$

## 同余方程

1. 一次同余方程 $ax \equiv b (mod \ m )$ 有解的充要条件是 $gcd(a,m)|b$ ，而且当其有解时，其解数为 $gcd(a,m)$

2. 对于一次同余方程 $ax \equiv b (mod \ m )$ 设 $a^\prime = \frac a {gcd(a,m)},m^\prime = \frac m {gcd(a,m)},b^\prime = \frac b {gcd(a,m)}$

   - 考虑 $a^\prime x \equiv 1 (mod \ m^\prime)$ 有唯一解 $x \equiv x_0 (mod \ m^\prime)$
   - $a^\prime x \equiv b^\prime (mod \ m^\prime)$  有解 $x \equiv x_0b^\prime +km^\prime (mod \ m^\prime),k=0,\pm1,\pm 2 ,\cdots$
   - $ax \equiv b (mod \ m )$解得 $x \equiv x_0b^\prime +wm^\prime(mod \ m),w=0,1,2,\cdots ,gcd(a,m)-1$

3. 设 $m$ 为正整数，若同余式
   $$
   x^2 \equiv a (mod \  m) ,gcd(a,m)=1
   $$
   有解，则称 $a$ 为模 $m$ 的二次剩余，否则称 $a$ 为模 $m$ 的二次非剩余。

   - 对于 $m=2$ ，判断某个数是否为模 $m$ 的二次剩余是平凡的（$x=[1]$）。
   - 在模奇素数 $p$ 的一个既约剩余系中，恰有 $\frac{p-1}2$ 个模 $p$ 的二次剩余，$\frac{p-1}2$ 个模 $p$ 的二次非剩余。

4. 设 $p$ 为一个奇素数，$gcd(a,p)=1$ ，$a$ 是模 $p$ 的二次剩余的充要条件是
   $$
   a^{\frac{p-1}2 \equiv 1(mod \ p)}
   $$
   $a$ 是模 $p$ 的二次非剩余的充要条件是
   $$
   a^{\frac{p-1}2 \equiv -1(mod \ p)}
   $$

## 中国剩余定理CRT

1. 如果 $m_1,m_2,\cdots ,m_k$ 是两两互素的正整数，则同余方程组
   $$
   \left\{
   \begin{align}
   x &\equiv a_1 (mod \ m_1)\\
   x &\equiv a_2 (mod \ m_2)\\
   &\cdots\\
   x &\equiv a_k (mod \ m_k)\\
   \end{align}
   \right.
   $$
   对模 $m=m_1m_2 \cdots m_k$ 有唯一解。

   - $M_i=\frac {m}{m_i}=m_1 \cdots m_{i-1}m_{i+1} \cdots m_k$
   - $M_i^ \prime=M_i^ {-1}(mod \ m_i)$
   - 解为 $x \equiv M_1^\prime M_1 a_1+M_2^\prime M_2 a_2+ \cdots +M_k^\prime M_k a_k(mod \ m)$

2. 如果 $m_1,m_2,\cdots ,m_k$ 是两两互素的正整数，则同余方程
   $$
   f(x) \equiv 0 (mod \ m)
   $$
   与同余方程组
   $$
   \left\{
   \begin{align}
   x &\equiv a_1 (mod \ m_1)\\
   x &\equiv a_2 (mod \ m_2)\\
   &\cdots\\
   x &\equiv a_k (mod \ m_k)\\
   \end{align}
   \right.
   $$
   同解

3. 群 $G,H,\forall g \in G,h \in H$

   - $G \times H$ 是群
   - $(g,h) \in G \times H,|G \times H|=|G||H|$ （两个维度）
   - 对于代数运算 $\circ_G,\circ_H,\circ_{G\times H},(g_1,h_1)\circ_{G \times H}(g_2,h_2)=(g_1 \circ_G g_2,h_1 \circ_H h_2)$

4. 设 $N=pq$ ，其中 $p$ 和 $q$ 互质 $\implies Z_N \cong Z_p \times Z_q,Z_N^* \cong Z_p^* \times Z_q^*$

   - $p_1 ,p_2 ,\cdots, p_k$  成对互质，即$\forall i \neq j ,gcd (p_i,p_j)=1,N=p_1 p_2 \cdots p_k$$\implies Z_N \cong Z_{p_1} \times Z_{p_2} \times \cdots \times Z_{p_k},Z_N^* \cong Z_{p_1}^* \times Z_{p_2}^* \times \cdots \times Z_{p_k}^*$
   - $x_N \to (x_p,x_q)$ 是简单的
   - 对于 $(x_p,x_q) \to x_N$
     - 已知 $(x_p,x_q)=x_p \cdot (e_p,0_q)+x_q \cdot (0_p,e_q),e_p,0_p \in Z_p,e_q,0_q \in Z_q$
     - 只要找到 $x_{N1} \leftrightarrow (e_p,0_q) , x_{N2} \leftrightarrow (0_p,e_q)$

## RSA公钥加密

1. 密钥生成

   - $p,q \in P$

   - $n=pq,\varphi(n)=\varphi(p)\varphi(q)=(p-1)(q-1)$

   - $e\in Z,gcd(e,\varphi(n))=1$

   - $d \in Z,1<d<\varphi(n),ed\equiv 1(mod \ \varphi(n))$

2. 加密

   - $c=m^e(mod \ n)$

3. 解密

   - $m=c^d(mod \ n)$

## 快速幂

计算 $g^A (mod \ N)$

1. 将 $A$ 以 $x$ 进制表示为 $A=A_0x^0+A_1x^1+\cdots +A_rx^r$ （比如二进制）
2. 通过不断的平方，得到 $g^{x^i}$
   - $a_0 \equiv g^{x^0} (mod \ N)$
   - $a_1 \equiv a_0^x \equiv g^{x^1} (mod \ N)$
   - $a_2 \equiv a_1^x \equiv g^{x^2} (mod \ N)$
   - $\cdots$
   - $a_r \equiv a_{r-1}^x \equiv g^{x^r} (mod \ N)$
3. $g^a \equiv a_0^{A_0}a_1^{A_1}\cdots a_r^{A_r} (mod \ N)$
