# 类欧几里得算法总结

---

## Main Chapter

本篇内容和[WerKeyTom_FTD](http://blog.csdn.net/werkeytom_ftd/article/details/53812718) 这篇差不多，而且没有什么新东西。可以视为转载。

### f(a,b,c,n)

$$
f(a,b,c,n)=\sum_{i=0}^{n}\lfloor \frac{ai+b}{c}\rfloor
$$


$$
a = \lfloor \frac{a}{c}\rfloor*c+a\%c
$$

$$
b = \lfloor \frac{b}{c}\rfloor*c+b\%c
$$

$$
f(a,b,c,n)=\sum_{i=0}^{n}\lfloor \frac{\lfloor \frac{a}{c}\rfloor*c*i+(a\%c)i+\lfloor \frac{b}{c}\rfloor*c+b\%c}{c}\rfloor\\=\sum_{i=0}^{n}(\lfloor \frac{a}{c}\rfloor*i+\lfloor \frac{b}{c}\rfloor+\lfloor \frac{(a\%c)i+b\%c}{c}\rfloor)\\=\lfloor \frac{a}{c}\rfloor*\frac{(n+1)*n}{2}+\lfloor \frac{b}{c}\rfloor*(n+1)+\sum_{i=0}^{n}\lfloor \frac{(a\%c)i+b\%c}{c}\rfloor\\=\lfloor \frac{a}{c}\rfloor*\frac{(n+1)*n}{2}+\lfloor \frac{b}{c}\rfloor*(n+1)+f(a\%c,b\%c,c,n)
$$



$$
m = an+b
$$

$$
f(a,b,c,n)=\sum_{i=0}^n\sum_{j=0}^{m-1}[j+1\le \frac{ai+b}{c}]\\=\sum_{i=0}^n\sum_{j=0}^{m-1}[i>\frac{c*j+c-b-1}{a}]\\=\sum_{j=0}^{m-1}n- \lfloor\frac{c*j+c-b-1}{a}\rfloor\\=nm- \sum_{j=0}^{m-1}\lfloor\frac{c*j+c-b-1}{a}\rfloor\\=nm- f(c,c-b-1,a,m-1)
$$


$$
a,b,c\Rightarrow \begin{cases} a\%c,b\%c,c&a\ge c,b\ge c \\ c,c-b-1,a&a<b,b<c\end{cases}
$$

### g(a,b,c,n)

$$
g(a,b,c,n) = \sum_{i=0}^ni*\lfloor \frac{ai+b}{c}\rfloor
$$




$$
g(a,b,c,n) =\sum_{i=0}^{n}i*(\lfloor \frac{a}{c}\rfloor*i+\lfloor \frac{b}{c}\rfloor+\lfloor \frac{(a\%c)i+b\%c}{c}\rfloor)\\= \frac{(2n+1)*(n+1)*n}{6}*\lfloor \frac{a}{c}\rfloor+\frac{(n+1)*n}{2}*\lfloor \frac{b}{c}\rfloor+g(a\%c,a\%c,c,n)
$$



$$
g(a,b,c,n) = \sum_{i=0}^n\sum_{j=0}^{m-1}i*[i>\frac{c*j+c-b-1}{a}]\\= \frac{1}{2}*[m*n*(n+1)-\sum_{j=0}^{m-1}\lfloor\frac{c*j+c-b-1}{a}\rfloor^2-\sum_{j=0}^{m-1}\lfloor\frac{c*j+c-b-1}{a}\rfloor]
$$

$$
h(a,b,c,n) = \sum_{i=0}^n\lfloor \frac{ai+b}{c}\rfloor^2
$$

$$
g(a,b,c,n) = \frac{1}{2}*[m*n*(n+1)-h(c,c-b-1,a,m-1)-g(c,c-b-1,a,m-1)]
$$

### h(a,b,c,n)

$$
h(a,b,c,n) = \sum_{i=0}^n\lfloor \frac{ai+b}{c}\rfloor^2
$$




$$
h(a,b,c,n)=\sum_{i=0}^{n}(\lfloor \frac{a}{c}\rfloor*i+\lfloor \frac{b}{c}\rfloor+\lfloor \frac{(a\%c)i+b\%c}{c}\rfloor)*(\lfloor \frac{a}{c}\rfloor*i+\lfloor \frac{b}{c}\rfloor+\lfloor \frac{(a\%c)i+b\%c}{c}\rfloor)\\=\lfloor\frac{a}{c}\rfloor^2*\frac{n*(n+1)*(2n+1)}{2}+\lfloor\frac{b}{c}\rfloor^2*(n+1)+\lfloor\frac{a}{c}\rfloor*\lfloor\frac{b}{c}\rfloor*n*(n+1)\\+2*\lfloor\frac{a}{c}\rfloor *g(a\%c,b\%c,c,n)+2*\lfloor\frac{b}{c}\rfloor *f(a\%c,b\%c,c,n)
$$

$$
N^2=2\sum_{i=0}^Ni-n
$$

$$
h(a,b,c,n)=2\sum_{i=0}^n\sum_{j=0}^{\lfloor\frac{ai+b}{c}\rfloor}j-f(a,b,c,n)\\=2\sum_{i=0}^n\sum_{j=1}^mj[j\le \frac{ai+b}{c}]-f(a,b,c,n)\\=2\sum_{i=0}^n\sum_{j=0}^{m-1}(j+1)[i>\frac{cj+c-b-1}{a}]- 
f(a,b,c,n)\\=2\sum_{j=0}^{m-1}(j+1)\sum_{i=0}^n[i>\frac{cj+c-b-1}{a}]-
f(a,b,c,n)\\=2\sum_{j=0}^{m-1}(j+1)(n-\lfloor\frac{cj+c-b-1}{a}\rfloor)-
f(a,b,c,n)\\=2\sum_{j=0}^{m-1}(jn-j\lfloor\frac{cj+c-b-1}{a}\rfloor+n-\lfloor\frac{cj+c-b-1}{a}\rfloor)+
f(a,b,c,n)\\=m*(m+1)*n-2g(c,c-b-1,a,m-1)-2f(c,c-b-1,a,m-1)+f(a,b,c,n)
$$



---

## Special Chapter


$$
F(a,b,c,n)=\sum_{i=1}^n\lfloor (\frac{a\sqrt r+b}{c})\cdot i\rfloor
$$

$$
F(a,b,c,n) = \sum_{i=1}^n\lfloor (\frac{a\sqrt r+b}{c}-\lfloor\frac{a\sqrt r+b}{c}\rfloor)\cdot i+\lfloor\frac{a\sqrt r+b}{c}\rfloor\cdot i\rfloor\\
=\sum_{i=1}^n\lfloor (\frac{a\sqrt r+b}{c}-\lfloor\frac{a\sqrt r+b}{c}\rfloor)\cdot i\rfloor+\lfloor\frac{a\sqrt r+b}{c}\rfloor\cdot \frac{(n+1)n}{2}\\
=\sum_{i=1}^n\lfloor (\frac{a\sqrt r+b-c\cdot\lfloor\frac{a\sqrt r+b}{c}\rfloor}{c})\cdot i\rfloor+\lfloor\frac{a\sqrt r+b}{c}\rfloor\cdot \frac{(n+1)n}{2}
$$

设$t = b-c\cdot\lfloor\frac{a\sqrt r+b}{c}\rfloor$
$$
=\sum_{i=1}^n\lfloor (\frac{a\sqrt r+t}{c})\cdot i\rfloor+\lfloor\frac{a\sqrt r+b}{c}\rfloor\cdot \frac{(n+1)n}{2}
$$
//然后我们要缩小n的规模了

设$M = \frac{a\sqrt r+t}{c}\cdot n$
$$
\sum_{i=1}^n\lfloor (\frac{a\sqrt r+t}{c})\cdot i\rfloor\\
=\sum_{i=1}^n\sum_{j=1}^{M}[j\le\frac{a\sqrt r+t}{c}\cdot i]\\
=\sum_{i=1}^n\sum_{j=1}^{M}[i\ge\frac{cj(a\sqrt r-t)}{a^2r-t^2}]\\
=\sum_{j=1}^{M}n-\lfloor\frac{cj(a\sqrt r-t)}{a^2r-t^2}\rfloor+[\lfloor\frac{cj(a\sqrt r-t)}{a^2r-t^2}\rfloor==\frac{cj(a\sqrt r-t)}{a^2r-t^2}]\\
=Mn-\sum_{j=1}^{M}\lfloor\frac{cj(a\sqrt r-t)}{a^2r-t^2}\rfloor+\sum_{j=1}^M[\lfloor\frac{cj(a\sqrt r-t)}{a^2r-t^2}\rfloor==\frac{cj(a\sqrt r-t)}{a^2r-t^2}]\\
$$

$$
F(a,b,c,n)=Mn+\lfloor\frac{a\sqrt r+b}{c}\rfloor\cdot \frac{(n+1)n}{2}\\
+\sum_{j=1}^M[\lfloor\frac{cj(a\sqrt r-t)}{a^2r-t^2}\rfloor==\frac{cj(a\sqrt r-t)}{a^2r-t^2}]\\
-\sum_{j=1}^{M}\lfloor\frac{cj(a\sqrt r-t)}{a^2r-t^2}\rfloor
$$
对于$\sum_{j=1}^M[\lfloor\frac{cj(a\sqrt r-t)}{a^2r-t^2}\rfloor==\frac{cj(a\sqrt r-t)}{a^2r-t^2}]$，只有r是完全平方数才有可能有非零值。

而对于r是完全平方数的情况，就是上面求$f$函数的套路了。



参考资料（chao xi dui xiang）：[Sengxian's Blog](https://blog.sengxian.com/solutions/bzoj-3817)

---

## Additional Chapter 

例题

 **BZOJ 3817**
$$
\sum_{d=1}^n(-1)^{\lfloor d\sqrt r\rfloor}
$$
**solution**
$$
(-1)^{\lfloor a \rfloor}=\begin{cases}1&\lfloor a\rfloor\%2==0\\ -1&\lfloor a\rfloor\%2==1 \end{cases}
$$

$$
(-1)^{\lfloor a \rfloor}=1-2*[\lfloor a\rfloor\%2==1]
$$

当$\lfloor a \rfloor\%2==0$时，设$a=2k+r, r<1, k\in \mathbb{Z}$
$$
\lfloor a \rfloor = \lfloor 2k+r \rfloor=2k\\
\lfloor \frac{a}{2} \rfloor = \lfloor k+\frac{r}{2} \rfloor=k
$$
当$\lfloor a \rfloor\%2==1$时，设$a=2k+1+r, r<1, k\in \mathbb{Z}$
$$
\lfloor a \rfloor = \lfloor 2k+1+r \rfloor=2k+1\\
\lfloor \frac{a}{2} \rfloor = \lfloor k+\frac{1+r}{2} \rfloor=k
$$
联想到：$[\lfloor a\rfloor\%2==1]=\lfloor a\rfloor-2\lfloor \frac{a}{2}\rfloor$

设$\sqrt r = b$
$$
\sum_{d=1}^n(-1)^{\lfloor d\sqrt r\rfloor}=n-4\sum_{d=1}^{n}\lfloor \frac{bd}{2}\rfloor+2\sum_{d=1}^{n}\lfloor bd\rfloor
$$
然后按Special Chapter里面的方法套一套就OK。



 **BZOJ 2187**
$$
\frac{a}{b} < \frac{p}{q}<\frac{c}{d}
$$
先观察特殊情况下的答案：

如果$\frac{a}{b}$和$\frac{c}{d}$之间有一个整数，显然可以直接取到。形式化：
$$
\lfloor\frac{a}{b}\rfloor+1\le\lceil\frac{c}{d}\rceil-1
$$
此时，$q=1,p=\lfloor\frac{a}{b}\rfloor+1$最优

当一边的边界变成零，只有另一边的限制时（也就是a=0时），让p=1时q就可以最小了。
$$
\frac{p}{q}<\frac{c}{d}\Rightarrow q>\frac{dp}{c}
$$
除了这两种特殊情况，我们试图缩小a，b，c，d的规模，使得a为0。

由此联想到辗转相除法：当$a< b$时：（此时，一定有$c\le d$ ，不然就达到边界条件了）
$$
\frac{a}{b} < \frac{p}{q}<\frac{c}{d}\Rightarrow\frac{d}{c} < \frac{q}{p}< \frac{b}{a}
$$
否则：
$$
\frac{a}{b} < \frac{p}{q}<\frac{c}{d}\Rightarrow\frac{a\%b}{b}<\frac{p}{q}-\lfloor\frac{a}{b}\rfloor<\frac{c}{d}-\lfloor\frac{a}{b}\rfloor
$$

证明：

####1

$$\frac{a}{b}<\frac{p}{q}<\frac{c}{d}$$的最优解$$\frac{p_1}{q_1}$$

$$\frac{a\%b}{b}<\frac{p}{q}<\frac{c}{d}-\lfloor\frac{a}{b}\rfloor$$的最优解$$\frac{p_2}{q_2}$$

有：$$\frac{p_1}{q_1}=\frac{p_2}{q_2}+\lfloor\frac{a}{b}\rfloor$$

反证法：假设有$$\frac{a}{b}<\frac{p}{q}<\frac{c}{d}$$有$$\frac{p_3}{q_3}$$	更优，那么$$\frac{a\%b}{b}<\frac{p}{q}<\frac{c}{d}-\lfloor\frac{a}{b}\rfloor$$有$$\frac{p_3}{q_3}-\lfloor\frac{a}{b}\rfloor$$更优。

#### 2

$$\frac{a}{b}<\frac{p}{q}<\frac{c}{d}$$的最优解$$\frac{p_1}{q_1}$$
$$\frac{d}{c} < \frac{p}{q}< \frac{b}{a}$$的最优解$$\frac{p_2}{q_2}$$

有：$$\frac{q_1}{p_1}=\frac{p_2}{q_2}$$

反证法：设$$\frac{a}{b}<\frac{p}{q}<\frac{c}{d}$$有$$\frac{p_3}{q_3}$$更优，则$$\frac{d}{c} < \frac{p}{q}< \frac{b}{a}$$有非最优解$$\frac{q_3}{p_3}$$ 。那么有：$$p_3>p_1,q_3<q_1$$ 。

$$\frac{p_1-1}{q_3}-\frac{p_1}{q_1}=\frac{p_1(q_1-q_3)-q_1}{q_1q_3}$$ ，因为$$p_1>q_1$$，有$$\frac{p_1(q_1-q_3)-q_1}{q_1q_3}>0$$。

$$\therefore\frac{p_3}{q_3}>\frac{p_1-1}{q_3}>\frac{p_1}{q_1} $$ ，所以$$\frac{d}{c} < \frac{p}{q}< \frac{b}{a}$$有更优解$$\frac{q3}{p_1-1}$$，矛盾。