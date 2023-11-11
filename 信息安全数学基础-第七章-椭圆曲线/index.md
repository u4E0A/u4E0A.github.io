# 信息安全数学基础 第七章 椭圆曲线


# 第七章 椭圆曲线

1. $GF(p)$ 上的椭圆曲线
   $$
   E=\{(x,y)\in GF(p) \times GF(p)|y^2=x^3+ax+b \ (mod \ p),4a^3+27b^2 \not\equiv 0 \ (mod  \ p) \} \cup \{O\}
   $$

   - 椭圆曲线约束方程 $4a^3+27b^2 \not\equiv 0 \ (mod  \ p)$
   - 单位元，无穷远点 $O$
   - 逆元，$(x,-y)$

2. $GF(p)$ 上椭圆曲线几何加法

   - $P+O=P,O+P=P$

   - $O=-O$

   - $P=(x_1,y_1) \neq O \implies -P=(x_1,-y_1)$

   - $Q=-P \implies P+Q=O$

   - $P \neq O,Q \neq O,P \neq Q \implies P+Q+R^\prime =O, P+Q=R$

     <img src="\post\info_sec\信息安全数学基础-第七章-椭圆曲线\image-椭圆曲线.png" alt="image-椭圆曲线"  />

3. 域 $K$ 上的椭圆曲线 $E$ ，$(E(K),+)$ 是商群 $(E/K,+)$ 的子群

4. 椭圆曲线 $E_1/K$ 和 $E_2/K$ 同构 $\implies$ 群到群是同构的

5. $GF(p)$ 上椭圆曲线 $y^2=x^3+ax+b \ (mod \ p)$ 代数加法 $P=(x_1,y_1),Q=(x_2,y_2),R=(x_3,y_3),P+Q=R$

   - 斜率 $\lambda$
     $$
     \lambda =\left\{ \begin{align}
     &\frac{y_2-y_1}{x_2-x_1}(P \neq Q,P \neq -Q)
     \\
     &\frac{3x_1^2+a}{2y_1}(P=Q)
     \end{align} \right.
     $$

   - 性质
     $$
     \left\{ \begin{align}
     &x_1+x_2+x_3= \lambda
     \\
     &y_3=-(\lambda(x_3-x_1)+y_1)=-(\lambda(x_3-x_2)+y_2)
     \end{align} \right.
     $$

   - $R=(\lambda-x_1-x_2, \lambda(x_1-x_3)-y_1)$

6. 标量乘法

   - $nP=P+P+ \cdots + P$
   - $2P=P+P,4P=2P+2P,8P=4P+4P \implies 5P=4P+P$

7. $GF(p^m)$ 上椭圆曲线加法群的阶 $\#E(K)$

   - $\#E(K) \leq 2p^m+1,\#E(k) \approx p^m$
   - 存在 $\#E(K)=q+1-t$ 的充分必要条件
     - $t \not\equiv 0 \ (mod \ p),t^2 \leq 4p^m$
     - $m$ 是奇数，且下面任意条件成立
       - $t=0$
       - $t^2=2p^m,p=2$
       - $t^2=3p^m,p=3$
     - $m$ 是偶数，且下面任意条件成立
       - $t^2=4p^m$
       - $t^2=p^m,p \not\equiv1 \ (mod \ 3)$
       - $t^2=p^m,p \not\equiv1 \ (mod \ 4)$

8. $p>3,a,b \in GF(p)\implies \#E_p(a,b)=1+\sum^{p-1}_{x=0}[(\frac{x^3+ax+b}{p})+1]$

   - Legendre符号 $\left(\frac{a}{p}\right)=a^{\frac{p-1}{2}}\ mod p$

9. $p>3,p \equiv 3 \ mod \ 4,\forall a \in GF(p)^* \implies \#E_p(a,0)=p+1$

10. $p>3,p \equiv 2 \ mod \ 3,\forall a \in GF(p)^* \implies \#E_p(0,b)=p+1$

## Elgamal公钥加密

1. 密钥生成
   - $P \in E_p(a,b),o(P)=n$
   - $x,1 < x<n$
   - $Q=xP$
2. 加密
   - $k,1<k<n$
   - $C=(C_1=kP,C_2=P_m+kQ)$
3. 解密
   - $C_2-xC_1=P_m+kQ-xkP=P_m$
