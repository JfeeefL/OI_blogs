# FFT 复习补全计划

## 基本算法

### 快速傅里叶变换

**多项式**
$$
A_{[a_0,a_1\cdots,a_n]}(x) =a_0+a_1x+a_2x^2...a_nx^n
$$
**多项式乘法**
$$
A(x) = \sum a_i x^i\\
B(x) = \sum b_i x^i\\
C(x)=A(x)B(x)\\
C(x)=\sum c_i x^i\\
c_i=\sum_{j+k=i} a_j b_k
$$
**求值**
$$
y_k=A_{[a_0,a_1\cdots a_n]}(\omega ^k_n) =a_0+a_1\omega_n^k+a_2\omega_n^{2k}...a_n\omega_n^{nk}\\
A=\begin{bmatrix}
\omega_{n}^{0}&\omega_{n}^{0}&\cdots& \omega_{n}^{0}\\
\omega_{n}^{0}&\omega_{n}^{1}&\cdots& \omega_{n}^{n-1}\\
\vdots&\ddots & &\vdots\\
\omega_{n}^{0}&\omega_{n}^{n-1}&\cdots& \omega_{n}^{(n-1)\times (n-1)}\\
\end{bmatrix}\\

A
\begin{bmatrix}
a_0\\
a_1\\
\vdots\\
a_{n-1}
\end{bmatrix}
=
\begin{bmatrix}
y_0\\
y_1\\
\vdots\\
y_{n-1}
\end{bmatrix}
$$

```c++
Complex wn(cos(2*pi/n),sin(2*pi/n))//单位复数根 w_n
```

**插值**
$$
A^{-1}=\begin{bmatrix}
\frac{1}{n}\omega_{n}^{-0}&\frac{1}{n}\omega_{n}^{-0}&\cdots& \frac{1}{n}\omega_{n}^{-0}\\
\frac{1}{n}\omega_{n}^{-0}&\frac{1}{n}\omega_{n}^{-1}&\cdots& \frac{1}{n}\omega_{n}^{-(n-1)}\\
\vdots&\ddots & &\vdots\\
\frac{1}{n}\omega_{n}^{-0}&\frac{1}{n}\omega_{n}^{-(n-1)}&\cdots& \frac{1}{n}\omega_{n}^{-(n-1)\times (n-1)}\\
\end{bmatrix}\\

A^{-1}A

=
\begin{bmatrix}
1&0&\cdots& 0\\
0&1&\cdots& 0\\
\vdots&\ddots & &\vdots\\
0&0&\cdots& 1\\
\end{bmatrix}\\

A^{-1}
\begin{bmatrix}
y_0\\
y_1\\
\vdots\\
y_{n-1}
\end{bmatrix}
=
\begin{bmatrix}
a_0\\
a_1\\
\vdots\\
a_{n-1}
\end{bmatrix}
$$

```c++
Complex wn(cos(2*pi/n),f*sin(2*pi/n)) //单位复数根 w_n^{-1}

for (int i = 0; i < n; i ++) a[i] /= n;
```

**分治算法**
$$
A_{[a_0,a_1\cdots a_n]}(\omega ^{k}_n) = A_{[a_0,a_2\cdots]}(\omega ^{k}_{n/2})+\omega^k _nA_{[a_1,a_3\cdots]}(\omega ^{k}_{n/2})
$$

```c++
for (int i = 1; i < n; i <<= 1) { // 逆向枚举分治层数
    Complex wn(cos(pi/i),f*sin(pi/i)); // w_{i*2}
    for (int j = 0; j < n; j += (i<<1)) { //枚举合并块
        Complex w(1,0);
        for (int k = 0; k < i; k ++, w = w*wn) { //枚举块元素
            Complex x = a[j+k], y = w*a[i+j+k];
            a[j+k] = x+y;
            a[i+j+k] = x-y;
        }
    }
}
```

**系数映射**
$$
**0,**1\\
*00,*10,*01,*11\\
000,100,010,110,001,101,011,111\\
$$

```c++
R[0] = 0; //n 是 2^L
for (int i = 1; i < n; i ++) R[i] = (R[i>>1]>>1)|((i&1)<<(L-1));
```

**卷积**
$$
A\otimes B=C\\
c_i = \sum_{j+k=i} a_j\cdot b_k\\
a\otimes b=\mathrm{DFT^{-1}}(\mathrm{DFT}(a)\cdot\mathrm{DFT}(b))
$$

**快速傅里叶变换 模板**

```c++
typedef double db;
const db pi = acos(-1);
struct C {
	db r, i;
	C () {}
	C (db r, db i): r(r), i(i) {}
	C operator + (const C& rhs) const {return C(r+rhs.r, i+rhs.i);}
	C operator - (const C& rhs) const {return C(r-rhs.r, i-rhs.i);}
	C operator * (const C& rhs) const {return C(r*rhs.r-i*rhs.i, i*rhs.r+r*rhs.i);}
}A[N], B[N];
int R[N];
void fft (C *a, int n, int f) {
	for (int i = 0; i < n; i ++) if(i < R[i]) std::swap(a[i],a[R[i]]);
	for (int i = 1; i < n; i <<= 1) {
		C wn(cos(pi/i),f*sin(pi/i));
		for (int j = 0; j < n; j += (i<<1)) {
			C w(1,0);
			for (int k = 0; k < i; k ++, w = w*wn) {
				C x = a[j+k], y = a[i+j+k] * w;
				a[j+k] = x+y; a[i+j+k] = x-y;
			}
		}
	}
	if (f==-1) for (int i = 0; i < n; i ++) a[i].r /= n; 
}
void Convolution (double *a, int n, double *b, int m, double *c) {
	int h = n+m+1, L = 0; for(;(1<<L) < h; L++);
	R[0] = 0; h = 1<<L;
	for (int i = 1; i < h; i ++) R[i] = (R[i>>1]>>1) | ((i&1)<<(L-1));
	for (int i = 0; i < h; i ++) A[i] = i <= n? C(a[i],0): C(0,0);
	for (int i = 0; i < h; i ++) B[i] = i <= m? C(b[i],0): C(0,0);
	fft(A,h,1); fft(B,h,1);
	for (int i = 0; i < h; i ++) A[i] = A[i]*B[i];
	fft(A,h,-1);
	for (int i = 0; i <= n+m; i ++) c[i] = A[i].r;
}

```

### 快速数论变换

$$
ord_P(g)=P-1\\
\omega_n =g^\frac{P-1}{n}\\
\omega^{2k}_n= g^{\frac{P-1}{n}*2k}=\omega_{n/2}^k\\
\sum_{j=0}^{n-1} \omega_n^{-ij}\omega_n^{jk}=n[i==k]
$$

**快速数论变换 模板**

```c++
typedef long long ll;

const int N = 400005;
const int P = 998244353;
int R[N];
inline int qpow(int a, int b, int mod) {
	int ans = 1;
	while(b) {
		if(b&1) ans = (1ll * ans * a)%mod;
		b >>= 1; a = (1ll * a * a)%mod;
	}
	return ans;
}

inline int minus(int a, int b) { return (a-=b)<0?a+=P:a; }
inline int plus(int a, int b) { return (a+=b)>P?a-=P:a; }

void ntt (int *a, int n, int f) {
	for (int i = 0; i < n; i ++) if(i < R[i]) std::swap(a[i],a[R[i]]);
	for (int i = 1; i < n; i <<= 1) {
		int wn = qpow(3,f==1?(P-1)/(i<<1):(P-1-(P-1)/(i<<1)),P);
		for (int* p = a; p != a+n; p += (i<<1)) {
			int w = 1;
			for (int k = 0; k < i; k ++, w = 1ll*w*wn%P) {
				int y = 1ll * p[k+i] * w % P;
				p[k+i] = minus(p[k],y); p[k] = plus(p[k],y);
			}
		}
	}
	int v = qpow(n,P-2,P);
	if (f==-1) for (int i = 0; i < n; i ++) a[i] = 1ll*a[i]*v%P; 
}
void Convolution (int *a, int n, int *b, int m, int *c) {
	int h = n+m+1, L = 0; for(;(1<<L) < h; L++);
	R[0] = 0; h = 1<<L;
	for (int i = 1; i < h; i ++) R[i] = (R[i>>1]>>1) | ((i&1)<<(L-1));
	ntt(a,h,1); ntt(b,h,1);
	for (int i = 0; i < h; i ++) a[i] = 1ll*a[i]*b[i]%P;
	ntt(a,h,-1);
	for (int i = 0; i <= n+m; i ++) c[i] = a[i];
}
```



---

## 经典应用

### 卷积

### 任意数取模的傅里叶变换

### 分治+卷积

### 多项式求逆

### 多项式除法

### 多项式开根