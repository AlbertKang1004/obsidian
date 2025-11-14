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
	n = len(L)
	if n >= 2:
		L0 = L[0:n//2]
		L1 = L[n//2:n]
		MS(L0)
		MS(L1)
		Merge(L, L0, L1)
		# assuming a suitable helper Merge that merges L0 and L1 back into L
```

### Trace for `len(L) = 8`
![[Pasted image 20251114161400.png]]



Divide-and-conquer algorithm has simplified runtime recurrence
$$
T(n)=
\begin{cases}
n + 4\cdot\,T\!\left(\dfrac{n}{2}\right), & n \ge 2,\\[6pt]
T(1)=T_1, & n=1.
\end{cases}
$$


Runtime tree

--------
<span style="color:rgb(0, 176, 240)">"One-and-a-half" unrolling</span>
Here, last term $=4^k=$ \# of leaves

|             size             |        # nodes         |      times       |
| :--------------------------: | :--------------------: | :--------------: |
| $2\cdot2\cdots2\cdot2\cdot2$ |          $4$           |       $1$        |
|    $2\cdot2\cdots2\cdot2$    |       $4\cdot4$        |       $4$        |
|           $\vdots$           |        $\vdots$        |     $\vdots$     |
|             $2$              |    $4\cdots4\cdot4$    |    $4\cdots4$    |
|             $1$              | $4\cdots4\cdot4\cdot4$ | $4\cdots4\cdot4$ |
|                              |                        |                  |
 $\therefore T(n)\in \theta(\mathrm{last\ term})$
 
 