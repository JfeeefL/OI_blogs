#Lucas定理证明及总结

​	本人数学功底差，于是不定期地开始补习数学。我的总结不一定是正确的，请萌新不要随意相信；也请看到的大佬及时指出错误。本人感激不尽！

*以下 $p$ 字母皆代表质数



​	*Lucas定理* 内容：
$$
\binom{n}{m} \equiv \prod_{i=0}^{k}\binom{n_i}{m_i} \mod p
$$
​	其中：
$$
n = \sum_{i=0}^k n_i*p^i \\ m = \sum_{i=0}^k m_i*p^i
$$


证明：

​	用递归（数学归纳法）证明，原命题等价于：
$$
\binom{n}{m} \equiv \binom{\lfloor n/p \rfloor}{\lfloor m/p \rfloor}\binom{n\mod p}{m\mod\ p} \mod p
$$
​	接下来有一个大概是技巧性的思路：我们希望借用二项式定理，通过证明某一项的系数相等，来证明该命题。不知道这种技巧常不常用，先学着。

​	我们看到式子内部数字的特点：$n=\lfloor n/p\rfloor*p+(n\mod p)$ ，因而我们希望通过类似的方法把n（或m）分成这样两部分。

​	尝试：
$$
(x+1)^m \equiv (x+1)^{p*\lfloor m/p\rfloor}(x+1)^{m\mod p}\mod p
$$
$Lemma$
$$
(x+1)^p \equiv x^p+1 \mod p
$$
证明：
$$
\because \forall x<p,\nexists kx=p,k\in Z \\ \therefore \binom{n}{p}=\frac{p!}{n!(p-n)!} \equiv 0\mod p,n\ne 0,n\ne p\\\therefore (x+1)^p = \sum_{i=0}^{p}\binom{i}{p}x^i \equiv x^p+1 \mod p
$$
有了这个引理，上式可以化作：
$$
(x+1)^m \equiv (x^p+1)^{\lfloor m/p\rfloor}(x+1)^{m\mod p}\mod p
$$
套二项式定理：
$$
\sum_{i=0}^m \binom{i}{m}x_i \equiv \sum_{i = 0}^{\lfloor m/p \rfloor} \binom{i}{\lfloor m/p \rfloor}x^{pi} * \sum_{i = 0}^{m \mod p} \binom{i}{m \mod p}x^{i}
$$
左边$x^n$项的系数为$\binom{n}{m}$，右边：

​	设右边为
$$
\sum_{i = 0}^{\lfloor m/p \rfloor} \binom{i}{\lfloor m/p \rfloor}x^{pi} * \sum_{j = 0}^{m \mod p} \binom{j}{m \mod p}x^{j}
$$
要使$p*i+j=n$，$i=\lfloor n/p\rfloor ,j=n\mod p$时显然成立；当$i<\lfloor n/p\rfloor$时，设$i=\lfloor n/p\rfloor -\Delta,\Delta\ge 1$ , 有$p*\lfloor n/p\rfloor -p*\Delta+j=n$，则$j\ge p$矛盾。反之亦然。



所以有：
$$
\binom{n}{m} \equiv \binom{\lfloor n/p \rfloor}{\lfloor m/p \rfloor}\binom{n\mod p}{m\mod\ p} \mod p
$$
