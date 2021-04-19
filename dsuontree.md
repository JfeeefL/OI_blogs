#dsu on tree

英寸思婷的一种trick，方法是先树剖，再dfs计算答案；dfs时，先递归轻儿子，再递归重儿子，在递归重儿子时保留子树信息。

**复杂度分析** 考虑每一个点x的信息计算上传次数：观察x的每个祖先，只有每遇到一条轻边，他才会被重新遍历一次。根据树剖的复杂度分析，我们可以得知：每个点到根最多有$\log N$条轻边，所以计算每个点的时间复杂度是$O(\log N)$，总时间复杂度$O(N\log N)$ 。

灵感应该是从树剖本身来的吧，也就是多考虑了一下每个点和祖先的关系。

---

代码的话，，他们都是这样写的？

```c++
void upd( int u, int fa, int keep ) {
	if( keep ) {
		// 我要保留重子树信息！w(ﾟДﾟ)w
	} else {
		// 这棵子树，，我就暂时不要了_(:з」∠)_
	}
	for( auto& i: g[u] ) {
		if( i == fa || big[i] ) continue;
		upd(i,u,keep);
	}
}

void dfs( int u, int fa, int keep ) {
	for( auto& i: g[u] ) {
		if( i == fa || i == son[u] ) continue;
		dfs( i, u, 0 );
	}
	if( son[u] ) dfs( son[u], u, 1 );
	big[son[u]] = true; upd( u, fa, 1 ); big[son[u]] = false;
  
	//回答子树询问⁄(⁄ ⁄•⁄ω⁄•⁄ ⁄)⁄
  
	if( keep == 0 ) upd( u, fa, 0 );
}
```

---

发现之前**dfs序分治**的题很多也可以用这种方法诶。。