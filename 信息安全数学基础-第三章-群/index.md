# 信息安全数学基础 第三章 群


# 第三章 群

1. 群

   - 满足结合律 $(a \circ b)\circ c=a \circ (b\circ c)$
   - 有单位元 $e$
   - 有逆元 $a^{-1}$
   - （运算封闭）

2. 群 $G$ 的性质

   - $a\in G,e \circ a=a \circ e =a$

   - $\forall a \in G,\exist_{=1} b \in G,ab=ba=e$

   - $\forall a,b,c,ab=ac \implies b=c$

   - $\forall a,b \in G$

     $ax=b$ 解唯一

     $xa=b$ 解唯一

   - $\forall a,b \in G , (ab)^{-1}=b^{-1}a^{-1}$

3. 集合 $G$ 非空，乘法封闭，满足结合律，$\forall a,b \in G,ax=b，ya=b$ 在 $G$ 中有解 $\implies G$ 是群

4. **有限**集合 $G$ ，乘法封闭，满足结合律，满足消去律 $\implies G$ 是群

5. 子群

   - 如果群 $G$ 的非空子集合 $H$ 对于 $G$ 中的运算也构成一个群，那么称 $H$ 为 $G$ 的子群，记为 $H \leq G$ 。
   - 在群 $G$ 中，仅有单位元素构成的子集合 $\{e\}$ 和 $G$ 本身显然都是 $G$ 的子群。（平凡子群）

6. 群 $G$ 和 子群 $H \leq G$

   -  $e_G=e_H$
   -  $\forall a,a^{-1} \in G,a\ \in H \implies a^{-1} \in H$
   -  $a^na^m=a^{m+n},(a^n)^m=a^{mn}$
   -  $na+ma=(n+m)a,(na)m=mna$

7. 群 $G,\forall a \in G$，由 $a$ 生成的子群$H=\langle a \rangle =\{a^i|i \in Z \} , H\leq G$

   - $a^k=e$，最小正整数 $k$ 为元素 $a$ 的阶 $o(a)$
   - $a^{|G|}=e$
   - 同时易得 $|\langle a \rangle|=o(a)$
   - $H$ 是循环群，$a$ 是生成元

8. 群 $G$，非空子集合 $H$

   $\forall a,b \in H,ab^{-1} \in H \iff H \leq G$

9. 群 $G$ ，子群 $H$ ，$\forall a \in G$，左陪集 $aH$ ，右陪集 $Ha$，等价关系 $R_H=\sim$

   - $aH=\{ah|h \in H\},a \in aH,|aH|=|H|$ （$Ha$同）
   - $aG=G,GG=\{ah|h\in G,a \in G\}=G$
   - $a\sim b \iff b^{-1}a \in H $
   - $[a]_{R_H}=aH$
   - $H$ 的任意两个陪集或者相等或者无公共元素
   - 群 $G$ 可以表示成 $H$ 的若干个不相交的陪集之并
   - $H$ 的左陪集的个数称为 $H$ 在 $G$ 中的指数，记为 $[G:H]$ 
   - $|G|=|H||G:H|$
   - $aH=Ha \iff H \lhd G$
   - 交换群的所有子群都是正规子群

10. 有限群 $G,\forall a \in G \implies o(a)\,|\, |G|$

11. **欧拉定理**

    $\exist m \in Z^+,r\in Z_m ,gcd(r,m)=1 \implies r^{\varphi(m)}\equiv 1(mod \ m)$

    - $gcd(r,m)=1 \implies r \in Z^*_m$
    - $Z^*_m$ 是群
    - $Z^*_m=\varphi(m)$

12. 群的中心是指群中所有与其他元素都满足交换律的元素组成的集合，用C(G)表示。群的中心是群的一个子群，也是一个正规子群

13. 群 $G$ ，子群$H\leq G,a^{-1}Ha=\{a^{-1}ha|h \in H\},\forall a \in G $

    - $\iff H \lhd G$
    - $\iff aH=Ha$
    - $\iff \forall h \in H,a^{-1}ha \in H$
    - $\iff a^{-1}Ha \subseteq H$
    - $\iff a^{-1}Ha = H$

14. 群 $G$ ，**正规子群** $H \lhd G$

    - 商群 $G/H=\{aH|a \in G\}$
    - $(aH)(bH)=(ab)H$
    - $G/H$ 同时也是群
    - 单位元 $H$
    - $aH$ 逆元 $a^{-1}H$

15. 群 $G,G^\prime,f:G\to G^\prime,\forall a,b\in G$ 映射满足
    $$
    f(a)f(b)=f(ab)
    $$
    则称 $f$ 是群 $G$ 到 $G^\prime$ 的一个同态映射。

    - $f$ 是满射，满同态映射，$e \to e^\prime,a^{-1} \to {a^{-1}}^\prime$
    - $f$ 是一一映射，同构映射 $G \cong G^\prime$，内自同构 $G \cong G$
    - $G$ 与 $G/H$ 同态 （自然同态）
    - 同态 $f$ 的象 $f(G)=\{f(a)|a \in G\}$
    - $\forall a^\prime \in G ,a^\prime$ 的完全逆象 $f^{-1}(a^\prime)=\{a \in G| f(a)=a^\prime \}$
    - 同态 $f$ 的核 $ker(f)=f^{-1}(e^\prime)$ 

16. **群同态基本定理**

    群 $G,G^\prime $，满同态映射$f:G \to G^\prime,N=ker(f) \implies N\lhd G,G^\prime \cong G/N$

17. $G=\langle a \rangle$ 是无限循环群 $\implies G$ 只有两个生成元 $a,a^{-1}$ 

18. 设 $G=\langle a \rangle$ 是 $n$ 阶循环群，显然 $o(a)=n$，则群 $G$ 中的元素都是 $a^k$ 的形式，其中 $gcd(k,n)=1$

    - $a^j$ 是 $G$ 的生成元 $\iff gcd(j,n)=1$
    - $\forall m \in Z^+ ,a^m=e \iff n|m$
    - $\forall k \in Z^+,o(a^k)=\frac {n}{gcd(k,n)}$

19. 设 $\alpha \in Z^*_m$ ，若 $o(\alpha)=\varphi(m)$  ，则 $\alpha$ 称为 $Z^*_m$ 的生成元或原根。

    - $Z^*_m$ 是循环群，$Z^*_m=\{\alpha ^i (mod \ m)|0 \leq i \leq \varphi(n)-1 \}$
    - $\beta \equiv \alpha ^i (mod \ m)$ 为 $Z^*_m$ 的生成元 $\iff gcd(i,\varphi (m))=1$
    - $Z^*_m$ 的生成元个数为 $\varphi(\varphi(m))$

20. $\forall p \in P/\{2\},k \in Z^+,m=2,4,p^k,2p^k \iff Z^*_m$ 有生成元

    - 如果 $p$ 为一素数， 则 $Z^*_p$ 有生成元

21. 循环群的子群是循环群。循环群的商群也是循环群

22. $G=\langle a \rangle $ 是循环群

    - $o(a)=\infin \implies G$与整数加群 $\langle Z,+ \rangle$ 同构
    - $o(a)=m \in Z^+ \implies G$与整数模 $m$ 的剩余类加群 $\langle Z_m,+ \rangle$ 同构

23. 循环群 $G=\langle a \rangle ,\exist k \in Z^+,h=a^k \in G$

     $k$ 称为 $h$ 相对于生成元的离散对数 $k=log_a h$

24. 确定元素 $a$ 的阶

    - 有限群 $G,\forall a \in G \implies o(a)\,|\, |G|$
    - $|G|=n=p_1^{\alpha_1}p_2^{\alpha_2}\cdots p_k^{\alpha_k}$
    - $o(a)=p_1^{e_1}p_2^{e_2}\cdots p_k^{e_k} |n,e_i \leq \alpha_i$

25. 求循环群 $G$ 生成元

    - 随机选择 $a \in G$
    - $|G|=n=p_1^{\alpha_1}p_2^{\alpha_2}\cdots p_k^{\alpha_k}$
    - $a^{p_1^{\alpha_1}\cdots p_2^{\alpha_i -w}\cdots p_k^{\alpha_k}} \equiv 1 \implies a^{p_1^{\alpha_1}\cdots p_2^{\alpha_i -w +1}\cdots p_k^{\alpha_k}} \equiv 1 \implies a^{p_1^{\alpha_1}\cdots p_2^{\alpha_i -1}\cdots p_k^{\alpha_k}} \equiv 1$ 只需要判断 $\alpha_i -1$即可
    - $a^{p_1^{\alpha_1}\cdots p_2^{\alpha_i -1}\cdots p_k^{\alpha_k}} \equiv 1 \implies a$ 不是循环群 $G$ 的生成元

26. 求解 $n$ 阶循环群 $G=\langle a \rangle$ 离散对数 $t=log_ah$ 的快速搜索算法

    - 提前计算，中途相遇

    - $t$  的带余除法在 $m$ 确定情况下有唯一表达式 $t=q_0m+r_0,t<n$

    - 遍历 $q,r$ ，直到 $a^{qm+r}=h$

    - 会反复计算 $a^r$ ，可作一张表 $L=\{a^r,r\},r=0,1,\cdots ,m-1$ 

      另一方面，可以计算 $h(a^{-m})^q$ ，再在表 $L$ 中查看（对 $L$ 按照 $a^r$ 大小排序，则可以直接索引，进一步减小计算量）是否存在 $a^{r_i}=h(a^{-m})^q$ 

    - 取特殊值 $m= \lceil \sqrt{n} \, \rceil$ （计算量最小的特殊解）

    - 这样最多尝试 $qr(0 \leq q \leq m ,0 \leq r \leq m)$ 次即可得到 $t$


## ElGamal公钥加密

1. 密钥生成
   - $p \in P$
   - $Z^*_p$ 生成元 $g$
   - $\alpha \in Z_{p-1},\beta=g^\alpha (mod \ p)$
2. 加密
   - $k \in Z_{p-1}$
   - $E(m,k)=(r=g^k \ mod \ p,s=m\beta^k \ mod \ p)$
3. 解密
   - $D(r,s)=s(r^\alpha)^{-1} \ mod \ p =mg^{ak}g^{-ak} \ mod \ p=m$
