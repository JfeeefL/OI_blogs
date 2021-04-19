# Some Interesting Properties of Mean

Mean ( or say *expected value* ), is a value which describes the average value of random variables. There's the definition:
$$
\mathrm E X = \sum_{\omega\in\Omega} \mathrm {Pr}(\omega)\mathrm X(\omega)
$$
in another form:
$$
\mathrm E X = \sum_{x\in\mathrm X(\Omega)}x \mathrm {Pr}(\mathrm X = x)
$$
like integral, mean is a linear operation:
$$
\begin{align*}
\mathrm E (X+Y)& = \sum_{\omega\in\Omega} \mathrm {Pr}(\omega)(\mathrm X(\omega)+\mathrm Y(\omega))\\
&= \mathrm E X+\mathrm E Y
\end{align*}
$$
this property tells us: linear distribution addition can be calculated separately.

in another form:
$$
\begin{align*}
\mathrm E (X+Y)& = \sum_{x\in\mathrm X(\Omega)}x \mathrm {Pr}(\mathrm X = x)+\sum_{y\in\mathrm Y(\Omega)}y \mathrm {Pr}(\mathrm Y = y)\\
\end{align*}
$$
so in calculation, separation often simplify our process.

---

look at this problem:

> A sequence $C_1,\cdots ,C_n$ is given. In $f(H)$ which $H_1\cdots H_n$  is a permutation of $1,2,\cdots,n$. $f(H) = \sum_{i=1}^nC_i[H_i>H_{i-1}\mathrm{and}H_i>H_{i+1}]$.
>
> Suppose any permutation $H$ could be has the same probability to appear. 
>
> Calculate the mean of $f(H)$.

To calculate every situation $H$ can be is too dummy. We calculate the mean of each $C_i$ separately. For $C_1$ and $C_n$, there is $\mathrm{Pr}(H_1>H_2)=\mathrm{Pr}(H_n>H_{n-1})=\frac{1}{2}$. For other $C_i$, 