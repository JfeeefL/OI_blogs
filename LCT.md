# 自我易错点总结： Link/Cut Tree 相关

##与 splay 的不同

> 区别主要是isroot体现的，还有就是splay前pushdown翻转标记，因为splay完了可能紧接着就是在节点下接点，这时可能破坏树的形态。

```c++
const int N = 10010;

struct lct {
	int fa[N], ch[N][2]; bool s[N];
	
	void pushdown (int x) {
		if(s[x]) {
			s[x]^=1; s[ch[x][0]] ^= 1; s[ch[x][1]] ^= 1;
			std::swap(ch[x][0],ch[x][1]);
		}
	}
	bool isroot (int x) {
		int y = fa[x];
		return ch[y][0] != x && ch[y][1] != x;
	}
	void rotate(int x) {
		int y = fa[x], z = fa[y];
		pushdown(y); pushdown(x);
		int l = ch[y][1]==x, r = l^1;
		if(!isroot(y)) ch[z][ch[z][1]==y]=x;
		ch[y][l] = ch[x][r]; ch[x][r] = y;
		fa[x] = z; fa[y] = x; if(ch[y][l])fa[ch[y][l]] = y;
	}
	void splay(int x) {
		pushdown(x);
		while (!isroot(x)) {
			int y = fa[x], z = fa[y];
			if(!isroot(y)) {
				if((ch[y][0]==x)^(ch[z][0]==x)) rotate(x);
				else rotate(y);
			}
			rotate(x);
		}
	}
	void access (int x) {
		for(int pre = 0;x;pre = x, x = fa[x])
			splay(x),ch[x][1] = pre;
	}
	void makeroot (int x) {
		access(x); 
		splay(x); 
		s[x] ^= 1;
	}
	void link(int x,int y) {
		makeroot(x); fa[x] = y;
	}
	void cut(int x,int y) {
		makeroot(x); access(y); splay(y); 
		fa[x] = ch[y][0] = 0;
	}
	int find(int x) {
		access(x); 
		splay(x);
		while(ch[x][0])x=ch[x][0];
		return x;
	}
}T;
```