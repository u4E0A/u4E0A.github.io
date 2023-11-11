# 信息安全数学基础 第五章 多项式环


# 第五章 多项式环

1. $F$ 是一个域，我们称 $f(x)=a_nx^n+a_{n-1}x^{n-1}+ \cdots+a_1x+a_0(a_i \in F,n \in N)$ 是 $F$ 上的一元多项式

   - $x$ 未定元
   - $a_n \neq 0,a_nx^n$ 为 $f(x)$ 首项
   - $deg(f(x))=n$ 为 $f(x)$ 次数
   - 首一多项式 $f(x)=1 \cdot x^n+a_{n-1}x^{n-1}+ \cdots+a_1x+a_0(a_i \in F,n \in N)$
   - $f(x)=a_0 \neq 0 \implies deg(f(x))=0$ 零次多项式
   - 多项式环 $F[x]$

2. 多项式环运算

   - 加法满足封闭性、结合律、交换律
   - 乘法满足封闭性、结合律、交换律
   - 乘法对加法满足分配律

   - $f(x)=a_nx^n+a_{n-1}x^{n-1}+ \cdots+a_1x+a_0(a_i \in F,n \in N)$
   - $g(x)=b_nx^n+b_{n-1}x^{n-1}+ \cdots+b_1x+b_0(b_i \in F,n \in N)$
   - $f(x)+g(x)=(a_n+b_n)x^n+(a_{n-1}+b_{n-1})x^{n-1}+\cdots + (a_1+b_1)x+(a_0+b_0)$
   - $f(x)g(x)=\sum^{m+n}_{s=0}(\sum_{i+j=s}a_ib_j)x^s$

3. 整环 $F$ ，多项式环 $F[x]\implies F[x]$ 是整环

   - 零元素 $f(x)=0$
   - $f(x)=a_nx^n+a_{n-1}x^{n-1}+ \cdots+a_1x+a_0(a_i \in F,n \in N)$ 负元 $-f(x)=-a_nx^n-a_{n-1}x^{n-1}- \cdots-a_1x-a_0(a_i \in F,n \in N)$
   - 单位元 $f(x)=1$
   - $F[x]$ 无零因子（由 $F$ 无零因子）

4. 如果 $(f(x))^k|g(x)$ 但 $(f(x))^{k+1}$ 不能整除 $g(x)$ ，则称 $f(x)$ 是 $g(x)$ 的 $k$ 重因式

5. 多项式整除性质，$c \neq 0 \in F$

   - $f(x)|0$
   - $c|f(x) \because f(x)=c(c^{-1}f(x))$
   - $f(x)|g(x) \implies cf(x)|g(x)$
   - $f(x)|g(x),g(x)|h(x) \implies f(x)|h(x)$
   - $f(x)|g(x),f(x)|h(x) \implies \forall u(x),v(x) \in F[x],f(x)|u(x)g(x)+v(x)h(x)$
   - $f(x)|g(x),g(x)|f(x) \implies f(x)=cg(x)$

6. 首一多项式 $p(x) \in F[x],deg(p(x)) \geq 1$，如果 $p(x)$ 在 $F[x]$ 内因式仅有零次多项式 $f(x)=c$ 及 $cp(x)$ ，则称 $p(x)$ 是 $F(x)$ 内的一个不可约多项式，否则称为可约多项式

7. $GF(2)[x]$ 五次以内的不可约多项式

   | 次数 | 不可约多项式                                                 |
   | ---- | ------------------------------------------------------------ |
   | 0    | $1$                                                          |
   | 1    | $x,x+1$                                                      |
   | 2    | $x^2+x+1$                                                    |
   | 3    | $x^3+x^2+1,x^3+x+1$                                          |
   | 4    | $x^4+x^3+x^2+x+1,x^4+x^3+1,x^4+x+1$                          |
   | 5    | $x^5+x^3+x^2+x+1,x^5+x^4+x^2+x+1,x^5+x^4+x^3+x+1,$$x^5+x^4+x^3+x^2+1,x^5+x^3+1,x^5+x^2+1$ |

8. 因式分解唯一定理

   $F[x]$ 上的多项式
   $$
   f(x)=a_nx^n+a_{n-1}x^{n-1}+ \cdots+a_1x+a_0(a_i \in F,n \in N)
   $$
   可唯一分解为
   $$
   f(x)=a_n\cdot(p_1(x))^{k_1}\cdot(p_2(x))^{k_2}\cdot\  \cdots\ \cdot (p_r(x))^{k_r},(k_1,k_2,\cdots,k_r>0)
   $$
   其中 $p_1(x),p_2(x),\cdots$ 是两两不同的首一不可约多项式。除 $p_1(x),p_2(x),\cdots$ 的排列次序外，上述分解是唯一的

9. 一个多项式 $f(x)\in F[x]$ 含有因式 $x-a,a\in F \iff f(a)=0$

10. 首一多项式 $f(x) \in F[x],a(x),b(x) \in F[x],a(x)=q_1(x)f(x)+r(x),b(x)=q_2(x)f(x)+r(x) \iff a(x) \equiv b(x) \ mod \ f(x)$

    - $a(x) \equiv b(x)\  mod \ f(x) \iff a(x)-b(x)=g(x)f(x),g(x)\in F[x]$
    - $a(x) \equiv b(x)\  mod \ f(x) \iff f(x)|a(x)-b(x)$

11. 首一多项式 $f(x) \in F[x],deg(f(x)) \geq0 \implies F[x] \ mod \ f(x)$ 构成有单位元交换环，称为多项
    式剩余类环

    - $\overline{a(x)}+\overline{b(x)}=\overline{a(x)+b(x)}$
    - $\overline{a(x)}\overline{b(x)}=\overline{a(x)b(x)}$
    - $F[x]$ 的理想为 $I=\{g(x)f(x)|g(x)\in F[x]\}$
    - $F[x] \ mod \ f(x)$ 是环，是 $F[x]$ 关于 $I$ 构成的商环 $F[x]/f(x)F[x]$ 
    - $GF(2)[x]\ mod\ (x^2+1)=\{\overline0,\overline1,\overline{x},\overline{x+1}\}$
      - 零因子 $x+1$

12. 首一**不可约**多项式 $f(x) \in F[x],deg(f(x)) \geq0 \implies F[x] \ mod \ f(x)$ 构成域

13. 域 $F$ 上的多项式 $F[x]$ 是主理想整环
