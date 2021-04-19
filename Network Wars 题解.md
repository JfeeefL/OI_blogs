# Network Wars 题解

> 题意：
>
> 给你一个无向图$G(V,E)$， 每一条边$<u,v>\in E$ 有一个权值$w[u,v]$，现在你要在图中找一个割集把1号点和n号点分开，并且这个割集中的边平均权值最小。

> 割集定义：去掉割集中的边，S到T不连通。

形式化：

$Minimize$
$$
f(E') = \frac{\sum_{<i,j>\in E'} w[i,j]}{\sum_{<i,j>\in E'} 1}
$$
其中$E'\subset E$，$E'$是$G$的一个割集

接下来我们希望找到$E'$和答案的关系。

---



接下来我们讨论一下分数规划的普遍解法：

分数规划的形式：

$Minimize$
$$
\lambda = f(x) = \frac{a(x)}{b(x)}
$$
其中$x\in S,b(x)>0$

假设最小的$\lambda=\lambda^*=f(x^*) = \frac{a(x^*)}{b(x^*)}$ ，然后移项：
$$
a(x^*) -\lambda b(x^*) =0
$$
借助上式的形式，设
$$
g(\lambda) = \min_{x\in S}\{a(x)-\lambda b(x)\}
$$

---

证明：$g(\lambda)$是随着$\lambda$的增长严格下降的单调函数。

设$\lambda'>\lambda$，且$x'$满足$g(\lambda) = \min_{x\in S}\{a(x)-\lambda b(x)\}=a(x')-\lambda b(x')$
$$
g(\lambda)=a(x')-\lambda b(x')>a(x')-\lambda'b(x')\ge g(\lambda')
$$



---

下面证明$g(\lambda)=0$当且仅当$\lambda=\lambda^*$

$$
\lambda = \lambda^* \Rightarrow g(\lambda)=0
$$
$$
\lambda^* = \frac{a(x^*)}{b(x^*)}\le \frac{a(x)}{b(x)}
$$

$$
a(x)-\lambda b(x)\ge0
$$

所以$g(\lambda)=\min\{a(x)-\lambda b(x)\}=0$
$$
g(\lambda)=0 \Rightarrow  \lambda = \lambda^*
$$
假设$\lambda^*<\lambda$ ，则$\frac{a(x^*)}{b(x^*)}<\lambda$

则
$$
{a(x^*)}-\lambda{b(x^*)}<0
$$
则$g(\lambda)<0$， 与$g(\lambda)=0$矛盾

---

所以我们可以通过二分$g(\lambda)$来找解决这个问题。

---

看原题：



假设$x$为一个01向量，表示每条边是否存在。

向量$c$是一个全部是1的向量，表示边权全部为单位边权

向量$w$对应图中的点权。

则原式表示为：

$Minimize$
$$
f(x)=\frac{w\cdot x}{c\cdot x}
$$
设

$$
\lambda=f(x)=\frac{w\cdot x}{c\cdot x}
$$

则
$$
({w}-\lambda c)\cdot x=0
$$

借用上面的形式，设
$$
g(\lambda)=\min\{({w}-\lambda c)\cdot x\}
$$
即新建图，原边权为$w$变成$w-\lambda$，$g(\lambda)$即是新图中的最小割。

而$g(\lambda)$有二分性质，所以我们可以二分答案。