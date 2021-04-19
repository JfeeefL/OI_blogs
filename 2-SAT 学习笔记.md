# 2-SAT 学习笔记

## 适定性问题 Satisfiability

---

设有限布尔变量集
$$
B = \{ b_1,b_2\dots,b_n\}
$$
设另一个有限布尔变量集
$$
\hat{B} = \{b_1,b_2\dots ,b_n\} \cup \{\lnot b_1,\lnot b_2\dots,\lnot b_n \}
$$
再设$B'\subseteq \hat{B}$且$B'\ne \emptyset$。 定义$\lor B' = \bigvee_{b\in B'}b$

---

给定
$$
B'_1,B'_2\dots,B'_m\subseteq \hat{B}
$$
求集合$B$满足：
$$
\bigwedge_{i=1}^m \lor B'_i = 1
$$
这样的问题叫做**适定性问题(Satisfiability)**，简称**SAT**。

---

对于特定问题中的$\{B'_m\}$，如果$\max\{|B'_i|\}=k$，则称之为 **k-适定性问题**，简称**k-SAT**

$k>2$时，该问题为NP-C问题。而$k=2$时，可以根据特殊性质，在线性时间内解决该问题。

---

## 2-适定性问题 2-SAT

对于$B$