# 信息安全数学基础 第四章 环与域


# 第四章 环与域

1. 环

   - 对 $+$ 交换群
   - 对 $\cdot$ 满足结合律 $(a\cdot b)\cdot c=a\cdot (b\cdot c)$
   - $\cdot$ 对 $+$ 满足左右分配律 $a\cdot (b+c)=a\cdot b+a\cdot c,(b+c)\cdot a=b\cdot a+c\cdot a$

2. 环 $R$ 性质，$a,b \in R ,m,n \in Z^+,ma=a+a+\cdots+a,a^m=a \cdot a\cdot \ \cdots \ \cdot a$

   - $a\cdot 0=0\cdot a=0$
   - $a \cdot (-b)=(-a)\cdot b=-(ab)$
   - $n(a+b)=na+nb$
   - $m(ab)=(ma)b=a(mb)$
   - $a^ma^n=a^{(m+n)}$
   - $(a^m)^n=a^{mn}$
   - 环中一定有零元素（加法群单位元）

3. $\forall a \in R,1_R \cdot a=a \cdot 1_R \implies$ 有单位元环

   - $1_R$ 单位元
   - $0_R$ 零元素
   - $-a$ 负元
   - $\exist b \in R,ab=ba=1,a$ 可逆元
   - $0_R$ 无逆元
   - 环中并不一定所有的非零元都有逆元，如 $Z$
   - 乘法可逆元一定不是左、右零因子

4. $\forall a,b \in R, a\cdot b=b\cdot a \implies$ 交换环

5. 全体整数关于数的普通加法和乘法构成一个环，称为**整数**环 $Z$

6. 全体有理数（实数、复数）关于数的普通加法和乘法构成一个环，称为有理数环 $Q$

7. $\forall [a],[b] \in Z/mZ,[a]+[b]=[a+b],[a][b]=[ab],Z/mZ$ 为模 $m$ 的剩余类环

8. $\exist a,b \in R,a\neq 0,b\neq 0,ab=0 \implies$ 有零因子环，反之无零因子环

   - $a$ 左零因子
   - $b$ 右零因子
   - $Z,Q,R,C$ 无零因子环
   - 合数 $n,Z_n$ 有零因子环

9. 无零因子环 $R,a,b,c \in R ,a\neq 0$

   - $ab=ac \implies b=c$
   - $ba=ca \implies b=c$
   - 若一个环里消去律成立 $\implies$ 无零因子环
   - $R$ 中非零元的加法阶相等，这个加法阶或者是 $\infin$ ，或者是个素数 $p$。

10. 环 $R$ 的加法阶称为特征 $CharR$。当 $R$ 中非零元的加法阶为无穷大时 $CharR=0$ ，当 $R$ 中非零元的加 法阶为某个素数 $p$ 时 $CharR=p$

11. 有单位元、无零因子、交换环 $\implies$ 整环

12. 有单位元、至少包含一个不等于零的元、每一个不等于零的元有一个逆元 $\implies$ 除环

    - 无零因子环
    - 非零环 $R,R^*=\{a\in R | a \neq 0\},R$ 是除环 $\iff(R,\cdot)$ 是群
    - 除环 $R,\forall a ,b \in R,a\neq 0,ax=b,ya=b$ 都有唯一解

13. 至少含有两个元素、无零因子、有限环 $\implies $ 除环

14. 有单位元、至少包含一个不等于零的元、每一个不等于零的元有一个逆元、交换环 $\implies$ 域

    - 有限整环是域
    - $p\in P \iff Z_p=Z/pZ$ 是域

15. | 环   | 加法$+$ | 乘法$\cdot$                                            |
    | ---- | ------- | ------------------------------------------------------ |
    | 环   | 交换群  | 结合律                                                 |
    | 整环 | 交换群  | 结合律、单位元、无零因子、交换律                       |
    | 除环 | 交换群  | 群：结合律、单位元、非零有逆（必无零因子）             |
    | 域   | 交换群  | 交换群：结合律、单位元、非零有逆（必无零因子）、交换律 |

16. 环 $R$ ，非空子集 $S$

    - $\forall a,b \in S,a-b \in S,ab\in S \iff S$ 是 $R$ 的子环
    - $\forall b \neq 0 ,a \in S,a-b \in S,ab^{-1} \in S \iff S$ 是 $R$ 子除环

17. 环 $R$ ，非空子集 $I,\forall r\in R, \forall a,b \in I,a-b\in I,ar \in I,ra \in I \iff I \lhd R,I$ 是 $R$ 的理想

    - 理想一定是子环，反之未必
    - $\{0\}$ 和 $R$ 都是理想，分别称之为零理想和单位理想，统称平凡理想
    - 除环仅有平凡理想

18. 环 $(R,+,\cdot),(R^\prime ,\oplus,\circ)$，映射 $f:R \to R^\prime,\forall a,b \in R$

    - $f(a+b)=f(a)\oplus f(b)$
    - $f(a \cdot b)=f(a)\circ f(b)$
    - $0_R \implies 0_{R^\prime}=f(0_R)$
    - $f(-a)=\ominus f(a)$
    - $\exist 1_R \implies 1_{R^\prime}=f(1_R)$
    - $S$ 是 $R$ 的子环 $\implies$ $f(S)$ 是 $R^\prime =f(R)$ 的子环
    - $S^\prime$ 是 $R^\prime$ 的子环 $\implies$ $S=f^{-1}(S^\prime)=\{a \in R|f(a)\in S^\prime\}$ 是 $R$ 的子环
    - $R$ 有单位元，$c \in R$ 可逆 $\implies c^\prime=f(c)$ 可逆，${c^\prime}^{-1}=f(c^{-1})$
    - $R$ 是交换环 $\implies R^\prime$ 是交换环
    - 同态 $f$ 的核 $ker(f)=f^{-1}(0_{R^\prime})$ 
    - $ker(f)$ 是 $R$ 加法群的子群
    - $ker(f)=\{0_R\} \iff f$ 是单同态
    - 乘法在 $ker(f)$ 封闭 $\iff ker(f)$ 是子环，是 $R$ 的理想

19. 环 $R,R^\prime,R \cong R^\prime$

    - $R$ 是整环 $\iff R^\prime$ 是整环
    - $R$ 是除环 $\iff R^\prime$ 是除环
    - $R$ 是域 $\iff R^\prime$ 是域

20. 非空子集 $T \subseteq R ,\lang T \rang= \underset{T \subseteq I,I\lhd R}{\cap}I$ 是 $R$ 中包含 $T$ 的最小理想

    - 特别地，若 $T=\{a\}$ ，则简记主理想 $\lang T \rang = \lang a \rang$ 称为由 $a$ 生成的主理想
    - $R$ 是交换环 $, \lang a \rang=\{sa+na| \forall s \in R,\forall n \in Z\}$
    - $R$ 有单位元 $, \lang a \rang=\{x_1ay_1+\cdots +x_may_m |\forall x_i,y_i \in R,\forall m \in N \}$
    - $R$ 是有单位元交换环 $, \lang a \rang=\{ra | \forall r \in R\}=aR=Ra$
    - $Z$ 的理想一定是主理想
    - $\lang n \rang$ 是 $\lang m \rang$ 的子理想 $\iff m|n$

21. 环 $R,I\lhd R,R/I=\{x+I|x\in R\},[A]=a+I$

    - $R/I$ 中乘法为 $[X][Y]=[XY]=xy+I$
    - $R/I$ 构成环，称为商环（剩余类环）
    - 存在满同态 $\pi:R \to R/I$

22. **环同态基本定理**

    环 $R,R^\prime $，同态映射$\varphi:R \to R^\prime,N=ker(\varphi) \implies N\lhd R,R^\prime \cong G/N$

23. $R$ 是有单位元交换环 $,a,b \in R,I \lhd R,\forall ab\in I,a\in I$ **或** $b \in I \implies I$ 是 $R$ 的素理想

24. 环 $R,M\lhd R,M \neq R,\forall I \lhd R,M \supseteq I \implies M$  是 $R$ 的极大理想

25. 有单位元交换环 $R$

    - $M$  是 $R$ 的极大理想 $\iff R/M$ 是域
    - $P$  是 $R$ 的素理想 $\iff R/P$ 是整环

26. 对于每一个整环 $R$ ，一定存在一个域 $Q$，使得 $R$ 是 $Q$ 的子环
