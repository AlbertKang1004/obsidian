\[= Sets of `string`s\]
### Example 1: L-R Game

$$
\text{language} = \{s\in\{a, b\}^{*}: s\text{ ends with an even \# of } b\text{'s} \}

$$
Notation: $\{a, b\}^*$: set of all strings over $\{a,b\}$
- made up of a's and/or b's
- $\{a,b\}^{*}=\{\varepsilon, a, b, aa, ab, ba, bb, aaa, \dots\}$
- string = finite sequence of characters
- no quotes ($abb$ not "abb")
- "" is represented by $\varepsilon$
----
## Deterministic Finite Automata (DFA)
![[L-R]]
`L`, `R` are **states**.
◎: "accepting state" (`answer = True`)
◯ : non-accepting: (`answer = False`)

|     | a   | b   |
| --- | --- | --- |
| L   | L   | R   |
| R   | L   | L   |
- initial = `L`
- accepting = `{L}`

### Tracing DFA
![[L-R Trace]]

----
## Regular Expressions (`regex`, `RE`)
> Ends with even # of `b`'s

- Even number of `b`'s?
	- = 0 or more repetition of `bb`
	- `RE`: $(bb)^*$ 
		- $bb$ : matches bb
		- $*$ : 0 or more repetitions
$$
\begin{align}
\mathcal{L}\,((bb)^*) &= \text{language represented by expr. }(bb)^{*}\\[3pt]
&= {\text{all strings that match the pattern}} \\[3pt]
&= {\varepsilon, bb, bbbb, bbbbbb, \dots}
\end{align}

$$
- "ends with ..." ?
	- $\underline{(a+b)^*a}(bb) ^*$
	- **underlined part** : does not end with b!
	- $+$  : OR / Union / Alternation
$$\begin{align}
&\mathcal{L}\,((a,b)) = \{a,b\} \\[3pt]
&\mathcal{L} \,((a, b)^{*})=\{a,b\}^* 

\end{align}$$
Q: $(a+b)^*a^*(bb)^*$
False, as $b\varepsilon bb=bbb$
> Note: $bb$ and $\varepsilon$ does not match $(a+b)^*a(bb)^*$

$(a+b)^*a(bb)^*+(bb)^*$
$((a+b)^*a+\varepsilon)(bb)^*$
### Tracing `RE`s
![[RE Trace]]
### Example 2 : Designing DFA
We design a DFA for 
$$L_{2}=\{s\in\{a,b\}^{*}: |s|\geq 2\text{ and the 2nd-last char of }s \text{ is an }a\} $$
`RE`: 
$$\begin{align}
(a+b)&^*a(a+b)\\[3pt]
(a+b)&^*(aa+ab)
\end{align}
$$
in $q_{0}$: $\varepsilon$
after reading $a$: $a$
> Imagine all possible suffices (future characters) that we process

$$\begin{align}
\varepsilon :\:& \varepsilon a, \varepsilon b, \varepsilon aa, \varepsilon ab, \varepsilon ba, \varepsilon bb, \cdots \\[3pt]
a:\:& aa, ab, aaa, aab, \cdots
\end{align}$$
$\varepsilon , a$ are **distinguishable** with respect to $L_{2}$ because there is a common suffix (e.g. $b$) such that 
$$
\varepsilon \cdot b \notin L_{2}, \: a \cdot b \in L_{2}
$$
> **Consequence**: $\varepsilon$ and $a$ must end in different states!

![[DFA 0]]
$$\begin{align}
\varepsilon &: \varepsilon \cdot a, \varepsilon \cdot b, \varepsilon \cdot aa, \cdots \\[3pt]
b&: b \cdot a, b \cdot b, b \cdot aa, \cdots 
\end{align}$$
![[DFA 1]]
In $q_{1}$,  reading $a$?
current `str`: $a\notin L_{2}$
new `str`: $aa \in L_{2}$

![[DFA 2]]
$q_{1}$ read $b$
- $a \notin L_2$
- $ab \in L_{2}$
If $ab$ goes to 
- $q_{2}: aa \cdot a \in L_{2}$
- $q_{2}: ab \cdot a \notin L_{2}$
- Note $aa$ and $ab$ is **distinguishable**
$\therefore$ in $q_{1}$, reading $b$ needs new state

![[DFA 3]]
$\therefore a, aba$ are indistinguishable