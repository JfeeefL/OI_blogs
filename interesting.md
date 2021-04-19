# interesting

Problem 1.
$$
\sum_{i=1}^n \sigma_0(i^2)
$$

---

$$
f(n) = \sigma_0(n^2)\\
g(n) = 2^{\omega(n)}\\
\omega(n)=\sum_{d=\mathrm {prime}}[d|n]
$$

Lemma 1.
$$
f(n) = g(n)*1\\
$$

Lemma 2.
$$
\sum_{i=1}^n f(n)=\sum_{i=1}^n g(i)\lfloor\frac ni \rfloor
$$
Lemma 3.
$$
g(n)=\mu^2(n)*1
$$
Lemma 4.
$$
\sum_{i=1}^ng(i)=\sum_{i=1}^n\mu^2(i)\lfloor\frac ni\rfloor
$$
Lemma 5.
$$
\sum_{i=1}^n\mu^2(i)=\sum_{i=1}^\sqrt n\mu(i)\lfloor\frac n {i^2}\rfloor
$$
proof.
$$
A_k=\{m\in \mathbb{N} |m\le n,\exists d\in N,k^2\cdot d= m\}\\
n-\sum_{i=1}^n\mu^2(i)=|\bigcup_{p}^n A_p|\\=\sum_{k=1}(-1)^{k+1}\sum_{p_1,p_2\cdots,p_k}|\bigcap_{j=1}^kA_{p_j}|\\
=\sum_{i=2}^\sqrt n-\mu(i)\lfloor\frac n {i^2}\rfloor\\
\sum_{i=1}^n\mu^2(i)=\sum_{i=1}^\sqrt n\mu(i)\lfloor\frac n {i^2}\rfloor\\
$$

$$
\sum_{i=1}^n f(i)=\sum_{i=1}^{n}\mu^2(i)*1*1
$$

---

$$
\sum_{i=1}^n f(n)=\sum_{i=1}^n g(i)\lfloor\frac ni \rfloor\\
\sum_{i=1}^ng(i)=\sum_{i=1}^n\mu^2(i)\lfloor\frac ni\rfloor\\
\sum_{i=1}^n\mu^2(i)=\sum_{i=1}^\sqrt n\mu(i)\lfloor\frac n {i^2}\rfloor\\
$$

