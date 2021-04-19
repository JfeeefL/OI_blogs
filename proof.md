**命题:** 

若存在向量整数$x$ ，满足$a\cdot x=1$ ：当且仅当$\nexists d>1,\forall d|a_i$。

**证明:**

1. $\exists x,a\cdot x=1\Rightarrow \nexists d,\forall d|x_i$

反证法：

对于有整数向量解的$a$ 。假设$ \exists d>1,\forall d|a_i$

则对于每个$a_i$可以拆分成$dk_i$

则 $a\cdot x=\sum dk_ix_i=d\sum k_ix_i$

所以$a\cdot x$ 一定是$d$的倍数

所以$a\cdot b\ne 1$

2. $\nexists d,\forall d|x_i\Rightarrow \exists x,a\cdot x=1$

$lemma\ 1.$ 一定可以把向量$a$分成两个不相交的集合$S,T$，$\exists S'\subset S,T'\subset T \Rightarrow (\sum_{x\in S'}x)\perp(\sum_{x\in T'}x )$

这个引理你试着自己证一下



然后拓展欧几里得