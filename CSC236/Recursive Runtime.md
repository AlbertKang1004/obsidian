---
share_link: https://share.note.sx/1gf01uai#dhdFmI/QiFIpMZTC/qq+Gu2YImj3hYtkc57NJzltN3k
share_updated: 2025-11-19T21:05:22-05:00
---
## Example 1: Factorial

```python
def fact(n):
	if n == 0: return 1
	else: return n * fact(n-1)
	# runtime inside is θ(1)
```
### Call Tree

|   Call    | Steps per node |
| :-------: | :------------: |
| `fact(3)` |       1        |
| `fact(2)` |       1        |
| `fact(1)` |       1        |
| `fact(0)` |       1        |
| **Total** |   $T(3) = 4$   |
$T(n)$ is a **runtime function**.
### Notation
- $T(n)$ = runtime function for input size $n$ (total)
- $t(n)$ = runtime of all *non-recursive* steps for input size $n$
### Notes
In code: 
```python
def T(n):
	if n == 0: return 1
	else: return T(n - 1)
```
In mathematical notation: 
$$
T(n)=\begin{cases}
1, &n=0 \\[6pt]
1+T(n-1), &n\geq 1
\end{cases}
$$
But we want a closed-form notation for $T(n)$.
We call it "unrolling" / tracing / repeated substitution.
$$\begin{align}
T(3)&= 1+T(2) \\[3pt]
&= 1+(1+T(1)) \\[3pt]
&= 1+ 1+(1+T(0)) \\[3pt]
&= 1+1+1+1=4
\end{align}$$
Generally: 
$$\begin{align}
T(n)&=(1+T(n-1)) \\[3pt]
&= 1+(1+T(n-2)) \\[3pt]
&=1+1+(1+T(n-3)) \\[3pt]
&=\cdots  \\[3pt]
\mathrm{k\;subtitutions}&= \underbrace{1+1+\cdots +1}_{k}+T(n-k) \\[3pt]

\end{align}$$
reach base case when $n-k=0\equiv k=n$
$$
\begin{align}
&=n+T(n-n)=n+T(0) \\[3pt]
&=n+1
\end{align}
$$
>$T(n)=n-1$ is just a guess — needs proof!

----
## Example 2: Merge Sort

```python
def MS(L):
	n = len(L) # Θ(1)
	if n >= 2: # 
		L0 = L[0:n//2] # Θ(n)
		L1 = L[n//2:n] #
		MS(L0) # len(L0) = floor(n/2)
		MS(L1) # len(L1) = ceil(n/2)
		Merge(L, L0, L1) # Θ(n)
		# assuming a suitable helper Merge that merges L0 and L1 back into L
		# t(n) = Θ(1) + Θ(n) + Θ(n) = Θ(n)
```

### Trace for `len(L) = 8`

![[mergesort_diagram]]
### Analysis
$$\begin{align}
T(8)&=1\cdot 8+2\cdot 4+4\cdot 2+8\cdot 1 \\[3pt]
T(8)&=8\cdot 4=32
\end{align}$$
![[mergesort_runtime]]
In mathematical notation:
$$
T(n)=
\begin{cases}
1, & n=0,1\\[6pt]
n+T\left( \left\lfloor   \frac{n}{2} \right\rfloor   \right)+T\left( \left\lceil  \frac{n}{2}  \right\rceil  \right), & n\geq 2.
\end{cases}
$$
Unroll (top - down):
$$
\begin{align}
T(n)&=n+T\left( \left\lfloor   \frac{n}{2} \right\rfloor   \right)+T\left( \left\lceil  \frac{n}{2}  \right\rceil  \right) \\[3pt]
&=n+\left( \left\lfloor  \frac{n}{2}  \right\rfloor T\left( \left\lfloor  \left\lfloor  \frac{n}{2}  \right\rfloor /2  \right\rfloor  \right) +T\left( \left\lceil  \left\lfloor  \frac{n}{2}  \right\rfloor /2  \right\rceil  \right)\right) \\[3pt]
&= \cdots
\end{align}

$$
However, this is not clean.
Start from Picking $n=2^k$.
$$\begin{align}
T(2^k)&=2^k+T\left( \left\lfloor  \frac{2^k}{2}  \right\rfloor  \right)+T\left( \left\lceil  \frac{2^k}{2}  \right\rceil  \right) \\[3pt]
&=2^{k}+2\cdot T(2^{k-1}) \\[3pt]
&= 2^k+2(2^{k-1}+2\cdot T(2^{k-2})) \\[3pt]
&= 2^k+2^k+2^2\cdot T(2^{k-2}) \\[3pt]
&=\cdots \mathrm{after \: \textit{i}\: substitutions}\cdots\\[3pt]
&=i\cdot2^k+2^{i}\cdot T(2^{k-i}) \\[3pt]
&= \cdots \mathrm{when} \: i=k\cdots \\[3pt]
&= 2^k(k+1)
\end{align}$$
$\therefore T(2^{k)}= 2^k(k+1)$.

How about $T(n)$?

![[mergesort_graph]]

### Claim: T is non-decreasing. 
>$(\forall m\leq n,T(m)\leq T(n))$, Can be proved by *induction*

(1) $\forall k \in \mathbb{N}, T(2^{k})= 2^k\cdot(k+1)$
$$\begin{align}
n&=2^{k} \\[3pt]
\equiv \mathrm{lg}\; n&=k \\[3pt]
 [\mathrm{lg}\ n&=\log_{2}n]
\end{align}$$
(2) $\forall m\leq n,T(m)\leq T(n)$

**WTP**: $T(n)\in\Theta(n \mathrm{lg}\;n)$ from definition of $\Theta$.
Let $n\in\mathbb{N}$. Assume $n\geq\cancel{1}\cancel{2}4$.
- case 1: Assume $\exists k, n=2^k$.
	- Then $T(n)=2^k(k+1)=n(\mathrm{\lg}\;n+1)$ (by (1))
		- $\therefore T(n) \geq n\mathrm{lg}\;n$
		- $\therefore T(n) \leq n(\mathrm{lg}\;n+\mathrm{lg}\;n)=2n\mathrm{lg}\;n$, as long as $\mathrm{lg}\;n \geq 1\equiv n\geq 2$
- case 2: Assume $n$ is **not** a power of $2$.
	- Then $\exists k\in\mathtt{N}, 2^k<n<2$.
	- $\therefore  Ⓐ\;2^k(k+1)=T(2^{k})\leq T(n)\leq T(2^{k+1})=Ⓑ\;2^{k+1}(k+2)$ (by (2))
		- Ⓐ $n<2^{k+1}\equiv \frac{n}{2}<2^k$
			- also $\equiv \mathrm{lg}\;n\leq k+1$
			- multiply both, we get $\displaystyle\frac{1}{2}n\mathrm{lg}\;n<2^k(k+1)$.
			- $\displaystyle\therefore \frac{1}{2}n\mathrm{lg}\;n\leq T(n)$
		- Ⓑ $2^k<n\equiv k<\mathrm{lg}\;n$
			- also $\equiv 2^{k+1}<2n$
			- multiply both, we get
			- $2^{k+1}k<2n\mathrm{lg}\;n$
			- $2^{k+1}(k+2)<2n(\mathrm{lg}\;n+2) \leq 2n(\mathrm{lg}\;n+\mathrm{lg}\;n)$(when $n\leq 4$)
			- $\therefore T(n)\leq 4n\mathrm{lg}\;n$
Combine case 1 and 2, 
- $\displaystyle\frac{1}{2}n\mathrm{lg}\;n \leq T(n)\leq 4n\mathrm{lg}\;n$
- $\therefore T(n)\in \Theta(n\mathrm{lg}\;n)$

**Better solution**: Start with arbitrary $n\geq 4$ and the unique $k$ such that $2^{k}\leq n < 2^{k+1}$.

----
## Example 3: Divide-and-Conquer

> Question: How much time does it take to multiply two **large** integers ($n$ digits each)?

Divide-and-conquer algorithm has simplified runtime recurrence
$$
T(n)=
\begin{cases}
n + 4\cdot\,T\!\left(\dfrac{n}{2}\right), & n \ge 2,\\[6pt]
1, & n=1.
\end{cases}
$$
-  $n$ is non-recursive time $\Theta (n)$.
- $4$ is number of recursive calls, with $\displaystyle\frac{n}{2}$ input size for each recursive call 

### Runtime tree for $n=2^k$
![[Runtime Tree]]
$$T(n) = \underbrace{2^{k}\cdot4^0}_{n}+\dots+2^0\cdot 4^k$$
"One-and-a-half" unrolling
$$\begin{align}
T(n) &= n+4\cdot T\left( \frac{n}{2} \right) \\[3pt]
&= n+4\left( \frac{n}{2}+\cdots \right) \\[3pt]
&= n+\frac{4}{2}n+\cdots  \\[3pt]

\end{align} $$

$T(n)$ is **geometric**, with ratio $\displaystyle\frac{4}{2}=2$.
$\therefore T(n)\in \Theta (\text{last term})$
$\because \text{ratio}>1$
Here, last term $=4^k=$ \# of leaves

|             size             |        # nodes         |              time               |
| :--------------------------: | :--------------------: | :-----------------------------: |
| $2\cdot2\cdots2\cdot2\cdot2$ |          $4$           |  $2\cdot2\cdots2\cdot2\cdot2$   |
|    $2\cdot2\cdots2\cdot2$    |       $4\cdot4$        |  $2\cdot2\cdots2\cdot2\cdot4$   |
|           $\vdots$           |        $\vdots$        |            $\vdots$             |
|             $2$              |    $4\cdots4\cdot4$    | $2\cdot 4\cdots 4\cdot 4\cdot4$ |
|             $1$              | $4\cdots4\cdot4\cdot4$ | $4\cdot 4\cdots 4\cdot 4\cdot4$ |
$$\begin{align}
2^{k} & \to \;4^k \\[3pt]
n& \to\; ? \\[3pt]
(2^k) ^{\log_{2}4}& =4 \\[3pt]
n^{\log_{2}4} &= n^2 \\[3pt]
\text{\# of leaves} &= n^{\log_{2}4} 
\end{align}$$
$\therefore T(n)\in \Theta (\text{last term})$

----
### Karatsuba's Algorithm
Karatsuba's algorithm has runtime recurrence
$$T(n)=\displaystyle\begin{cases}\displaystyle
n+3T\left( \frac{n}{2} \right), &n\geq 2 \\[6pt]
1, &n=1
\end{cases}$$
$$\begin{align}
\therefore T(n)&\in \Theta(\text{last term}) \\[3pt]
&=\Theta (\text{\# of leaves})
\end{align}$$
$$\begin{align}\displaystyle
2\cdot 2 \cdots  2\longrightarrow 3\cdot 3\cdots 3 \\[3pt]
\text{input size }n\longrightarrow \underbrace{n^{\log_{2}3} \text{ leaves} }_{T(n)\in \Theta(n^{\log_{2}3})}
\end{align}$$
As $2^{\log_{2}3} =3$. ($1< \log_{2}{3}<2$)
### [[Recursive Runtime#Example 2 Merge Sort|Merge Sort]] Revisited
$$\begin{align}
T(n)&=n+2T\left( \frac{n}{2}\right) \\[3pt]
&= n+\frac{2}{2}n+\cdots \\[3pt]
&= n+n+\cdots 
\end{align}$$
- ratio = $1$
- all terms contribute $T(n) \in \Theta(n\log n)$
	- $n$ is one term in the sum
	- $\log n$ is number of levels

**Generally**:
$$
T(n)=\begin{cases}\displaystyle
n^{d}+aT(\frac{n}{b}), &n>1 \\[6pt]
1, &n=1
\end{cases}
$$
$$\begin{align}
T(n) &= n^d+aT\left( \frac{n}{b} \right) \\[3pt]
&= n^d+a\left( \left( \frac{n}{b} \right)^d+aT\left( \frac{n}{b^2} \right) \right) \\[3pt]
&= n^d+\frac{a}{b^d}n^{d}+\cdots
\end{align}$$
- ratio = $\displaystyle \frac{a}{b^d}$
	- $a>b^{d}:\text{ratio}> 1$
	- $\therefore T(n)\in \Theta(\text{last term})$

![[MergeSort Generalized]]