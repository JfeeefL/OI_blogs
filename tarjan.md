# 考场上没写出来的Tarjan题

### COCI 2007 Set 1 # T6

> 题意： 在一个无向的仙人掌图中，找一个从1号节点出发的边不重复的最长路径，输出最长的长度。

由于起始点是确定的，那么能到的环的拓扑顺序是一定的（请利用仙人掌图的特点自行思考）。那么可以考虑按拓扑序DP。目标计算值是Path(1)，表示从节点1到其他任意节点的最长路。

但是在计算环上节点时，发现最长路可能绕过很多与其相交的环，并且每次可以回到原节点；没有办法按拓扑序继承。于是可以多记录一个值Circle(x)，表示从x点出发，并回到x点的最长路。

接下来重新组织一下语言。

$Circle(x)$ 表示：起点在x点，终点也在x点，途经DFS序比x大的点的最长路。

$Path(x)$表示：起点在x点，终点任意，途经DFS序比x大的点的最长路。



转移方程：
$$
Circle(x) = |edge\ on\ circle| + \sum_{y\in circle\ on\ x} Circle(y)
$$

$$
Path(x) = \max \begin{cases}Circle(x) + \max\{Path(bridge)\} +1\\
Circle(x)+\max\{Path(y)-\sum_{z\in side\ of\ the\ circle}(circle(z)+1)\}&y\in a\ circle\ below\ x
\end{cases}
$$



我来解释一下上面的式子：

Circle(x) ：从节点x出发，可以一次性走过所有DFN比它大的，并和x相交的环。而走到x的环上的每个节点y的时候，同样可以走从y出发并回到y第一条路，长度就是Circle(y)。

Path(x) ：

1. 从节点x出发，可以先绕过所有的环。这时，如果这个点有向外连的桥，那么在绕完所有环之后，就可能从这个点出去。
2. 路径绕过若干环后，有可能从某一个环的上某个节点出去。





---



贴代码

```c++
#include <cstdio>
#include <assert.h>
#include <algorithm>
const int N = 10010;
const int M = N << 1;
int Head[N], To[M << 1], Next[M << 1], ecnt = 1;
void addedge(int u,int v) {
	Next[++ecnt] = Head[u]; Head[u] = ecnt;
	To[ecnt] = v;
}
bool sel[M], vis[N];
int circle[M], path[M], stack[M], top;
int cir[N];

int dfs(int u) {
	vis[u] = true; int ret = u, bg = 0, mx = 0, block = u;
	stack[top++] = u;
	for(int i = Head[u];i;i = Next[i]) {
		if(sel[i>>1]) continue; sel[i>>1] = true;
		int v = To[i];
		if(vis[v]) {
			ret = v;
		} else {
			int w = dfs(v);
			if(w == u) {
				int blank = 0, size = 0;
				while (stack[top-1] != block) {
					int t = stack[top-1]; circle[u] += circle[t];
					blank -= circle[t]+1; mx = std::max(mx,blank+path[t]);
					cir[size++] = t; top--;
				}
				circle[u] += size + 1; blank = 0;
				for(int i = size-1;~i;i --) {
					int t = cir[i]; blank -= circle[t]+1; 
					mx = std::max(mx,blank+path[t]);
				}
			}
			else if(w == v){ bg = std::max(bg,path[v] + 1); }
			else { ret = w; block = stack[top-1]; }
		}
	}
	path[u] = circle[u] + std::max(bg,mx);
	if(ret == u) {
		do {top --;} 
		while (stack[top]!=u);
	}
	return ret;
}

int n, m;
int main() {
	scanf("%d%d",&n,&m);
	for(int i = 0;i < m;i ++) {
		int u, v; scanf("%d%d",&u,&v);
		addedge(u,v); addedge(v,u);
	}
	dfs(1);

	printf("%d\n",path[1]);
	return 0;
}
```



---

关键词：非树特殊图的拓扑关系。