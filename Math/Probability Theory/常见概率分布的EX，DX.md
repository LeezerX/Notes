# 速查表

|    X   |  (0,1) |  B(n,p) |       P($\lambda$)      |        U(a,b)        |       E($\lambda$)       |                                   N                                   |       超几何      |
|:------:|:------:|:-------:|:-----------------------:|:--------------------:|:------------------------:|:---------------------------------------------------------------------:|:-----------------:|
|  **P** |   1-p  |    p    | $C_n^k p^k (1-p)^{n-k}$ |    $\frac{1}{b-a}$   | $\lambda e^{-\lambda x}$ | $\frac{1}{\sqrt{2 \pi} \sigma} e^{-\frac{(x-\mu)^{2}}{2 \sigma^{2}}}$ |   $(1-p)^{k-1}p$  |
| **EX** |    p   |    np   |        $\lambda$        |    $\frac{a+b}{2}$   |    $\frac{1}{\lambda}$   |                                 $\mu$                                 |   $\frac{1}{p}$   |
| **DX** | p(1-p) | np(1-p) |        $\lambda$        | $\frac{(b-a)^2}{12}$ |  $\frac{1}{\lambda ^2}$  |                              $\sigma ^2$                              | $\frac{1-p}{p^2}$ |

---

# EX和DX的一些性质

## EX

1. $E[C] = C, \qquad C \equiv const$

2. $E[k\cdot X] = k\cdot EX$

3. $E[X+Y] = EX + EY$

4. $E[X\cdot Y] = EX \cdot EY, \qquad 当X和Y相互独立$

## DX

1. $D[C] = 0, \qquad C \equiv const$

2. $D[k\cdot X] = k^2 \cdot DX$

3. $D[X+C]=DX, \qquad C \equiv const$

4. $D[X+Y]=DX+DY+2Cov(X,Y)$,特别地,当X和Y相互独立时,$D[X+Y]=DX+DY$,更一般的:对于n个相互独立的变量$X_i$,有$D[\sum_{i=1}^{n} k_i X_i] = \sum_{k=1}^{n} k_i^2 DX_i$

5. $D[X\cdot Y] = DX^2\cdot DY^2 + (DX \cdot EY)^2 + (DY \cdot EX)^2$

---

# 简单分布的EX,DX的计算过程

## 通用公式

- **EX:**
  - *离散型随机变量:* $\bm{EX}=\sum_{i=1}^{n}x_ip_i$ 当$n=\infty$时,该级数收敛,期望才存在.

  - *连续型随机变量:* $\bm{EX}=\int_{-\infty}^{+\infty}xf_X(x)dx$

- **DX:**

   *定义:*$\bm{DX}=E[(X-EX)^2]$,表示r.v.的离散程度.

   常用计算公式:$\bm{DX}=E[X^2]-[EX]^2$

  - *离散型随机变量:* $\bm{DX}=\sum_{i=1}^{n} (x_i-EX)^2 p_i$,同样,当该级数收敛,方差才存在.

  - *连续型随机变量:* $\bm{DX} = \int_{-\infty}^{+\infty} (x - EX)^2 f_X(x)dx$

## 0-1分布

如果*r.v.X*服从*0-1*分布,则其分布列为

|X |0|1|
|:--:|:-:|:--:|
|**P**|1-p|p|

则
$$\begin{align*}
\bm{EX} &= 0 \times (1-p) + 1 \times p =p \\
\bm{DX} &= E[X^2] - [EX]^2 = 0 \times (1-p) + 1 \times
p - p^2=p(1-p)
\end{align*}$$

## 二项分布

$\bm{X\sim B(n,p)}$,则其分布列为

$$
\bm{P\{X=k\}}=\sum_{i=0}^{n}C_{n}^{k}p^k (1-p)^{n-k}
$$

下面求其EX和DX:

$$\begin{align*}
\bm{EX} &= \sum_{k=0}^{n} k C_{n}^{k} p^k (1-p)^k\\
  &= \sum_{k=0}^{n} k \cdot \frac{n!}{k!(n-k)!}
    p^k (1-p)^{n}\\
  &= \sum_{k=1}^{n} \frac{n!}{(k-1)![(n-1)-(k-1)]!}p^k (1-p)^{(n-1)-(k-1)}\\
令m=k-1,则&\\
  &= np \sum_{m=0}^{n}\frac{(n-1)!}{m![(n-1)-m]!}p^{k-1}(1-p)^{(n-1)-m} \\
上式中,求和部分&为[p+(1-p)]^{(n-1)}的二项式展开式,显然其等于1,代入上式易得: \\
 &= np
\end{align*}$$

为了计算方差,先计算其$\bm{E[X^2]}$

$$\begin{align*}
\bm{E[X^2]} &= \sum_{k=0}^{n} k^2 C_n^k p^k (1-p)^{n-k} \\
    &= \sum_{k=1}^{n} [k(k-1)+k] \frac{n!}{k!(n-k)!} p^k (1-p)^{n-k} \\
    &= \sum_{k=1}^{n} k(k-1) \frac{n!}{k!(n-k)!} p^k (1-p)^{n-k} + \sum_{k=1}^{n} k \frac{n!}{k!(n-k)!} p^k (1-p)^{n-k} \\
    &= n(n-1)p^2\sum_{k=2}^{n}\frac{(n-2)!}{(k-2)![n-2-(k-2)]!} p^{k-2} (1-p)^{n-2-(k-2)} + EX \\
    \\&令m=k-2\\\\
    &= n(n-1)p^2 \sum_{m=0}^{n-2} \frac{(n-2)!}{m!(n-2-m)!}p^m(1-p)^{n-2-m} + np \\
    &= n(n-1)p^2 [p+(1-p)]^{n-2} + np\\
    &= n(n-1)p^2 +np
\end{align*}$$

所以,可知:

$$\begin{align*}
\bm{DX} &= E[x^2] -[EX]^2 \\
  &= n(n-1)p^2 + np -(np)^2 \\
  &= np - np^2 \\
  &= np(1-p)
\end{align*}$$

另一种求解方法:

对于n次独立实验,假设每次实验发生的次数为$X_i$,易知$X_i$服从0-1分布,且概率为p,所以可知:

$$
E[X_i] = p\qquad D[X_i]=p(1-p)\qquad i=1,\cdots,n
$$

而由EX和DX的性质:
$$
E[X+Y] = EX+ EY\\
D[X+Y] = DX+DY\qquad (当XY独立)
$$

可知:
$$\begin{align*}
\bm{EX} &= E[\sum_{i=1}^{n}X_i]=\sum_{i=1}^{n}E[X_i]=np \\
\bm{DX} &= D[\sum_{i=1}^{n}X_i]=\sum_{i=1}^{n}D[X_i]=n\times p(1-p)=np(1-p)
\end{align*}$$

综上可知:

$$\begin{align*}
\bm{EX} &= np \\
\bm{DX} &= np(1-p)
\end{align*}$$

## 泊松分布

$\bm{X \sim P(\lambda)}$,则其分布列为
$$\bm{P(X=k)}=\frac{\lambda ^k}{k!} e^{-\lambda} \qquad k=0,1,2,\cdots$$

则其EX和DX计算如下:

$$\begin{align*}
\bm{EX} &= \sum_{k=0}^{\infty} k \cdot \frac{\lambda ^k}{k!} e^{-\lambda} \\
  &= \sum_{k=1}^{\infty} k \cdot \frac{\lambda ^k}{k!} e^{-\lambda} \\
  &= \lambda e^{-\lambda} \sum_{k=1}^{\infty} \frac{\lambda ^{k-1}}{(k-1)!} \\
  &令m=k-1 \\
  &= \lambda e^{-\lambda} \sum_{m=0}^{\infty} \frac{\lambda ^{m}}{m!} \\
  &= \lambda e^{-\lambda} \cdot e^{\lambda} \qquad (Taylor Series) \\
  &= \lambda
\end{align*}$$

$$\begin{align*}
\bm{E[x^2]} &= \sum_{k=0}^{\infty} k^2 \frac{\lambda ^k}{k!} e^{-\lambda} \\
    &= \sum_{k=1}^{\infty} [k(k-1)+k] \frac{\lambda ^k}{k!} e^{-\lambda} \\
    &= \sum_{k=1}^{\infty} k(k-1)\frac{\lambda ^k}{k!} e^{-\lambda} + \sum_{k=1}^{\infty} k \frac{\lambda ^k}{k!} e^{-\lambda} \\
    &= \sum_{k=2}^{\infty} k(k-1) \frac{\lambda ^k}{k!} e^{-\lambda} + EX \\
    &= \lambda ^2 e^{-\lambda}\sum_{k=2}^{\infty} \frac{\lambda ^{k-2}}{(k-2)!} + \lambda \\
    &令m=k-2 \\
    &= \lambda ^2 e^{-\lambda} \sum_{m=0}^{\infty} \frac{\lambda ^{m}}{m!} + \lambda \\
    &= \lambda ^2 e^{-\lambda} e^{\lambda} + \lambda \\
    &= \lambda ^2 + \lambda
\end{align*}$$

所以:

$$\begin{align*}
\bm{DX} &= E[x^2] - [EX]^2 \\
  &= \lambda ^2 + \lambda - \lambda ^2 \\
  &= \lambda
\end{align*}$$

综上,泊松分布的期望和方差如下:

$$
\bm{EX} = \lambda \qquad \bm{DX}=\lambda
$$

## 均与分布

$\bm{X \sim U(a,b)}$,则其概率密度为:

$$\begin{align*}
\bm{f_X(x)}=\left\{\begin{array}{l}
\frac{1}{b-a} \qquad &x \in (a,b) \\
0 \qquad &others
\end{array}\right.
\end{align*}$$

则其EX和DX计算如下:

$$\begin{align*}
\bm{EX} &= \int_{-\infty}^{+\infty} x \cdot \frac{1}{b-a} d x \\
  &= \int_{a}^b x \cdot \frac{1}{b-a} d x \\
  &= \frac{1}{b-a}\cdot \left.\frac{x^2}{2} \right|_{a}^{b} \\
  &= \frac{a+b}{2}
\end{align*}$$

然后计算$E[X^2]$:

$$\begin{align*}
\bm{E[X^2]} &= \int_{a}^{b} x^2 \cdot \frac{1}{b-a} dx \\
    &= \frac{1}{b-a} \cdot \left.\frac{x^3}{3} \right|_{a}^{b} \\
    &= \frac{1}{b-a} \cdot \frac{b^3-a^3}{3} \\
    &= \frac{1}{b-a} \cdot \frac{(b-a)(b^2+ab+a^2)}{3} \\
    &= \frac{b^2+ab+a^2}{3}
\end{align*}$$

所以可得:

$$\begin{align*}
\bm{DX} &= \frac{b^2+ab+a^2}{3} - (\frac{a+b}{2})^2 \\
    &= \frac{b^2+ab+a^2}{3} - \frac{a^2+2ab+b^2}{4} \\
    &= \frac{4b^2+4ab+4a^2-3a^2-6ab-3b^2}{12} \\
    &= \frac{b^2-2ab+a^2}{12} \\
    &= \frac{(b-a)^2}{12}
\end{align*}$$

综上:
$$\begin{align*}
\bm{EX} &= \frac{a+b}{2} \\
\bm{DX} &= \frac{(b-a)^2}{12}
\end{align*}$$

## 指数分布

$\bm{X \sim E(\lambda)}$,则其概率密度为:
$$
\bm{f_{x}(x)}=\left\{\begin{array}{l}
\lambda e^{-\lambda x} &  x>0 \\
0 &others
\end{array}\right.
$$

其**EX**和**DX**计算如下:

$$\begin{align*}
\bm{EX} &= \int_{0}^{\infty} x \cdot \lambda e^{-\lambda x} dx \\
     &= -\int_{0}^{\infty} x d e^{-\lambda x} \\
     &= - [ \left.xe^{-\lambda x}\right|_{0}^{+\infty}-\int_{0}^{+\infty} e^{-\lambda x}dx] \\
     &= -[ 0 - 0 - \left.(-\frac{1}{\lambda}e^{-\lambda x})\right|_0^{+\infty}] \\
     &= -(0-\frac{1}{\lambda}) \\
     &= \frac{1}{\lambda}
\end{align*}$$

为了计算**DX**,我们先计算$\bm{E[X^2]}$:

$$\begin{align*}
\bm{E[X^2]} &= \int_{0}^{+\infty} x^2 \cdot \lambda e^{-\lambda x} dx \\
    &= - \int_{0}^{+\infty} x^2 d e^{-\lambda x} \\
    &= - \left.x^2 e^{-\lambda x}\right|_{0}^{+\infty} + \int_{0}^{+\infty} e^{-\lambda x} d x^2 \\
    &= -(0-0) + \int_{0}^{+\infty} 2x \cdot e^{- \lambda x} dx \\
    &= \frac{2}{\lambda} \cdot \int_{0}^{+\infty} x \cdot \lambda e^{- \lambda x} dx \\
    &= \frac{2}{\lambda} \cdot \bm{EX} \\
    &= \frac{2}{\lambda ^2}
\end{align*}$$

所以可得:

$$\begin{align*}
\bm{DX} &= \frac{2}{\lambda ^2} - (\frac{1}{\lambda})^2 \\
    &= \frac{1}{\lambda ^2}
\end{align*}$$

综上:

$$\begin{align*}
\bm{EX} &= \frac{1}{\lambda} \\
\bm{DX} &= \frac{1}{\lambda ^2}
\end{align*}$$

## 正态分布

$\bm{X \sim N(\mu,\sigma ^2)}$,则其概率密度为

$$
\bm{f_X(x)} = \frac{1}{\sqrt{2 \pi} \sigma} \cdot e^{- \frac{(x-\mu)^2}{2\sigma ^2}}
$$

其**E[X]**和**D[X]**的计算如下:

首先,由概率密度的性质可知,对于$\bm{X\sim N(0,1})$,有:
$$
\int_{-\infty}^{+\infty} \frac{1}{\sqrt{2 \pi}} e^{-\frac{x^2}{2}} dx = 1 \tag{1}
$$

我们先计算**EX**

$$\begin{align*}
\bm{EX} &= \int_{-\infty}^{+\infty} x \cdot \frac{1}{\sqrt{2 \pi} \sigma} \cdot e^{- \frac{(x-\mu)^2}{2\sigma ^2}} \\
 我们对&积分变量进行正则化变换,令t=\frac{x-\mu}{\sigma},即x=\sigma t+\mu,dx=\sigma dt,\quad则原式可化为 \\
 &= \int_{-\infty}^{+\infty} (\sigma t+\mu) \frac{1}{\sqrt{2 \pi} \sigma} \cdot e^{-\frac{t^2}{2}}\cdot \sigma dt\\
 &= \sigma \cdot \int_{-\infty}^{+\infty} t \frac{1}{\sqrt{2 \pi}} \cdot e^{-\frac{t^2}{2}}\cdot dt + \mu \cdot \frac{1}{\sqrt{2 \pi}} \cdot e^{-\frac{t^2}{2}}\cdot dt\\
 &其中,左边进行积分函数为奇函数,在(-\infty,+\infty)上积分为0,右边的积分代入(1)可知为1 \\
 &= 0 + \mu \cdot 1 \\
 &= 1
\end{align*}$$

接着计算$\bm{E[X^2]}$:

$$\begin{align*}
\bm{E[X^2]} &= \int_{-\infty}^{+\infty} x^2 \cdot \frac{1}{\sqrt{2 \pi}\sigma} e^{-\frac{(x-\mu)^2}{2\sigma ^2}}dx\\
    同样地,对积分变量进行正则化:&令t=\frac{x-\mu}{\sigma},即x=\sigma t+\mu,dx=\sigma dt \qquad 则原式可化为:\\
    &= \int_{-\infty}^{+\infty} (\sigma t +\mu)^2 \frac{1}{\sqrt{2 \pi} \sigma} \cdot e^{-\frac{t^2}{2}}\cdot \sigma dt\\
    &= \int_{-\infty}^{+\infty} (\sigma ^2 t^2 + 2\sigma \mu t+\mu ^2)\cdot \frac{1}{\sqrt{2 \pi}} e^{-\frac{t^2}{2}} dt \\
    &= \sigma ^2 \int_{-\infty}^{+\infty} t^2 \cdot \frac{1}{\sqrt{2 \pi}} e^{-\frac{t^2}{2}} dt + 2\sigma \mu \int_{-\infty}^{+\infty} t \frac{1}{\sqrt{2 \pi}} e^{-\frac{t^2}{2}} dt + \mu ^2 \int_{-\infty}^{+\infty} \frac{1}{\sqrt{2 \pi}} e^{-\frac{t^2}{2}} dt \\
    我们分三项对上式进行计算:& \\
    对于第一项,&通过分部积分法可得:\\
    &\sigma ^2 \int_{-\infty}^{+\infty} t^2 \cdot \frac{1}{\sqrt{2 \pi}} e^{-\frac{t^2}{2}} dt =
        \frac{\sigma ^2}{\sqrt{2 \pi}} \int_{-\infty}^{+\infty} t^2 \cdot -\frac{1}{t} de^{-\frac{t^2}{2}} \\
        &= \frac{\sigma ^2}{\sqrt{2 \pi}}\cdot [\left.-t\cdot e^{-\frac{t^2}{2}}\right|_{-\infty}^{+\infty}-\int_{-\infty}^{+\infty} e^{-\frac{t^2}{2}}d(-t)] \\
        &= \frac{\sigma ^2}{\sqrt{2 \pi}}\cdot (0-0) + \sigma ^2 \int_{-\infty}^{+\infty} \frac{1}{\sqrt{2 \pi}} e^{-\frac{t^2}{2}} dt \\
        &代入(1)可知\\
        &= \sigma ^2\\
    对于第二项,&由于其被积函数为奇函数,在积分区间(-\infty,+\infty)上积分为0,所以第二项为0\\
    对于第三项,&代入(1)式可知:\\
        &\mu ^2 \int_{-\infty}^{+\infty} \frac{1}{\sqrt{2 \pi}} e^{-\frac{t^2}{2}} dt=\mu ^2 \\
    把这三项的计算结果代回上式可得:&
    \bm{E[X^2]} = \sigma^2+\mu^2
\end{align*}$$

**Triviall:**

$$\begin{align*}
\bm{DX} &= E[X^2]-(EX)^2 = \sigma^2+\mu^2-\mu^2 = \sigma^2
\end{align*}$$

综上:

$$\begin{align*}
\bm{EX} &= \mu \\
\bm{DX} &=\sigma^2
\end{align*}$$

## 超几何分布

**X服从超几何分布**[^1],则其分布列为:
$$
\bm{P\{X=k\}} = (1-p)^{k-1} p
$$

首先,我们先引用幂级数展开的知识,以方便后面的计算:

$$\begin{align*}
&\frac{1}{1-p} = \sum_{k=0}^{+\infty} p^k \\
&\frac{d\frac{1}{1-p}}{dp} = \frac{d{\sum_{k=0}^{+\infty} p^k}}{dp} \\
&\bm{\frac{1}{(1-p)^2} = \sum_{k=1}^{+\infty} kp^{k-1}} \tag{1} \\
&\frac{d\frac{1}{(1-p)^2}}{dp} = \frac{d\sum_{k=1}^{+\infty} kp^{k-1}}{dp} \\
&\bm{\frac{2}{(1-p)^3} = \sum_{k=2}^{+\infty} k(k-1)p^{k-2}} \tag{2} \\
\end{align*}$$

接着,我们开始计算其**EX**和**DX**:

$$\begin{align*}
\bm{EX} &= \sum_{k=1}^{+\infty}  k \cdot (1-p)^{k-1} p\\
 &= p \cdot \sum_{k=1}^{+\infty} k \cdot (1-p)^{k-1} \qquad 代入(1)可得\\
 &= p \cdot \frac{1}{[1-(1-p)]^2} \\
 &= \frac{1}{p}
\end{align*}$$

然后先计算$\bm{E[X^2]}$:

$$\begin{align*}
\bm{E[X^2]} &= \sum_{k=1}^{+\infty} k^2 \cdot (1-p)^{k-1} p \\
 &= \sum_{k=1}^{+\infty} [k(k-1)+k] \cdot (1-p)^{k-1} p \\
 &= \sum_{k=1}^{+\infty} k(k-1) \cdot (1-p)^{k-1} p + \sum_{k=1}^{+\infty} k \cdot (1-p)^{k-1} p \\
 &= p(1-p) \cdot \sum_{k=2}^{+\infty} k(k-1) (1-p)^{k-2} p + \bm{EX} \qquad 代入(2) \\
 &= p(1-p) \cdot \frac{2}{[1-(1-p)]^3} + \frac{1}{p} \\
 &= \frac{2(1-p)}{p^2} + \frac{1}{p} \\
 &= \frac{2-p}{p^2}
\end{align*}$$

由此可知:
$$\begin{align*}
\bm{DX} &= \frac{2-p}{p^2} - (\frac{1}{p})^2 \\
    &= \frac{1-p}{p^2}
\end{align*}$$

综上可知:
$$\begin{align*}
\bm{EX} &= \frac{1}{p} \\
\bm{DX} &= \frac{1-p}{p^2}
\end{align*}$$

[^1]: 例如:一个人掷硬币,正面朝上的概率为$\frac{1}{2}$.现在不断的掷硬币,直到出现硬币正面朝上后变停止.我们称第一次出现硬币正面朝上所需掷的次数服从超几何分布.
