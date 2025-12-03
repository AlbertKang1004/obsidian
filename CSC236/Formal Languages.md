\[= Sets of `string`s\]
### Example: L-R Game

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
> **Consequence**: $\varepsilon$ and $a$ must end in different states! (so that a common suffix will lead to a different outcome)

![[DFA 0]]
Then, we can consider three cases which $b$ can have.
![[DFA 5|80%]]
$$\begin{align}
\varepsilon &: \varepsilon \cdot a, \varepsilon \cdot b, \varepsilon \cdot aa, \cdots \\[3pt]
b&: b \cdot a, b \cdot b, b \cdot aa, \cdots 
\end{align}$$
> $\varepsilon \cdot s$, $b \cdot s$ are both in $L_{2}$ or not in $L_{2}$, so they are **indistinguishable** with respect to $L_{2}$.

Which means $\varepsilon$ and $b$ will end up in the same state.
- First DFA is correct.
- Third DFA can work, but it will require more states then required.

![[DFA 1]]
In $q_{1}$,  reading $a$?
current `str`: $a\notin L_{2}$
new `str`: $aa \in L_{2}$
- New state is needed, and it should be an **accepting** state.

![[DFA 2]]
$q_{1}$ read $b$
- $a \notin L_2$
- $ab \in L_{2}$
If $ab$ goes to 
- $q_{2}: aa \cdot a \in L_{2}$
- $q_{2}: ab \cdot a \notin L_{2}$
Note $aa$ and $ab$ is **distinguishable**.
- $\therefore$ in $q_{1}$, reading $b$ needs new state

![[DFA 3]]
$\therefore a, aba$ are indistinguishable

## Distinguishability
$$L_{2} = \{s \in \{a,b\}^{*}: \text{2nd-last char of } s=a\}$$
> $ba, bb$ are **distinguishable** with respect to $L_{2}$ :
- $\exists$ suffix $a \in \{a, b\}^{*}$ s.t.
	- $ba \cdot a = baa \in L_{2}$
	- $bb\cdot a = bba \notin L_{2}$
>$a, ba$ are **indistinguishable** with respect to $L_{2}$ :
- $\forall$ suffixes $s \in \{a,b\}^*$,
	-  $a\cdot s, ba \cdot s$ are both in $L_{2}$, or both not in $L_{2}$
	- $\forall s \in \{a, b\}^{*},as \in L_{2} \iff bas \in L_{2}$
	- Let $s \in \{a,b\}^*$.
	- case $|s|\geq 2$ (e.g. $s=ababb$)
		- then 2nd-last char of $a \cdot s$
		- 2nd-last char of $ba \cdot s$
		- are both = 2nd-last char of s
		- (e.g. $aababb, baababb$)
	- case $|s|<2$:
		-  $a \cdot \varepsilon$, $ba \cdot \varepsilon\notin L_{2}$ 
		-   $a \cdot a$, $ba \cdot a\in L_{2}$ 
		-   $a \cdot b$, $ba \cdot b\in L_{2}$ 
----
> **Definition**: A set of strings $S \subseteq \Sigma^*$

($S=\{s_{1}, s_{2}, \cdots\}$) is **pairwise distinguishable** with respect to $L$ iff $\forall i \neq j, s_{i} , s_{j}$ are **distinguishable** w.r.t. $L$.
- Example: $\{ba,bb\}$ is pairwise distinguishable w.r.t. $L_{2}$.
- $\{ba,bb,aa\}$ is pairwise distinguishable w.r.t. $L_{2}$.
- Is $aa,ba$ distinguishable? Yes: suffix = $\varepsilon$
	- ($aa\in L_{2}, ba \notin L_{2}$)
- same for $aa, bb$
- Basically, **pairwise distinguishable** = every pair in the set is **distinguishable**.
> **Claim**: Every DFA for $L_{2}$ must have at least 3 states.

***Proof.***
Pick 2 strings 
$s_{1} \in \{aa,ba,bb\}, \quad s_{2} =\{aa,ba,bb\}, \quad s_{1}\neq s_{2}$
$s_{1}, s_{2}$ are distinguishable. Let $t$ witness this:
- $s_{1}t \in L_{2},$
- $s_{2}t \notin L_{2}$ (or other way around)
In DFA, 
	-  $s_{1}t$ ends in **accepting** state
	- $s_{2}t$ ends in **rejecting** state
	- $\therefore s_{1}, s_{2}$ must end at different states.
- $\therefore$ each DFA for $L_{2}$ needs at least as many states as there are strings in $\{aa,ba,bb\}$.
- Here, largest set of pairwise distinguishable strings is $\{aa,ab,ba,bb\}$.
---
### Myhill-Nerode Theorem (Simplified)
> For each language $L$, each set of pairwise distinguishable strings w.r.t. $L,$
> every DFA for $L$ has at least $|s|$ many states.

----
## Nondeterministic Finite Automata (NFA)
> **Idea**: NFA is allowed to be in any number (or any subset) of its states, at any point during its computation.

**Why?**
Easier to represent languages of `regular expressions`.
**Example**
$$(a+b)^{*}a(a+b)$$
![[DFA 4]]
deterministic: $\delta(r_{0}, b) = \{r_{0}\}$
non-deterministic:
- $\delta (r_{0},a) = \{r_{0},r_{1}\}$
- $\delta(r_{2}, a)=\{\}$
**Trace**
![[NFA 0|600]]

---
## DFA vs. NFA vs. RE?
### DFA  
>$A= (\Sigma, Q, q_{\text{start}}, F, \delta)$
-  $\Sigma$ is a set of **alphabet**
- $Q$ is a set of **states**
- $q_{\text{start}} \in Q$ is a **starting** **state**
- $F \subseteq Q$ is a set of **accepting** **states**
- $\delta :Q \times \Sigma \longrightarrow Q$ is a **transition function**.
- Language $\mathcal{L}(A)$ recognized by **DFA**  $A = \{\text{all strings accepted}\}$

![[DFA|300]]
- $\overline{L} = \Sigma^{*}-L$
### NFA 
>$A= (\Sigma, Q, Q_{\text{start}}, F, \delta)$
-  $\Sigma$ is a set of **alphabet**
- $Q$ is a set of **states**
- $Q_{\text{start}} \subseteq Q$ is a **set of starting states**
- $F \subseteq Q$ is a set of **accepting** **states**
- $\delta :Q \times \Sigma \longrightarrow \mathcal{P}( Q)$ is a **transition function**.
	- $\mathcal{P}(Q)$ : power set of $Q$ = {all subsets of $Q$}
- Like DFA, **NFA**  $A$ recognizes 
	- Language $\mathcal{L}(A)=\{\text{strings accepted}\}$
### RE
- over $\Sigma$ : 
	- $\varnothing , \varepsilon, c \: (\text{for any } c \in \Sigma)$ are **RE**s
	- For all REs $R, S$, 
		- $(R+S), (RS), R^*$ are **RE**s.
 - Each **RE** $R$ defines
	 - Language $\mathcal{L}(R)=\{\text{strings matching R}\}$
### Formal Definition of Language
Language $\mathcal{L} \subseteq \Sigma^{*}$ is "regular" 
- **iff** $L=\mathcal{L}(A)$  for some **DFA**  $A$
- **iff** $L=\mathcal{L}(A)$ for some **NFA**  $A$
- **iff** $L=\mathcal{L}(R)$ for some **RE** $R$
---
## Non-regularity
>Ex: $L_{1}=\{a^{n}b^{n}:n\in \mathbb{N}\}$
- string **"exponent"**:
	- $\displaystyle a^{n}=\underbrace{aa\cdots a}_{n\text{ copies}}$ 
	- **NOT** a regular expression!
- $L_{1}=\{\varepsilon, ab, aabb, aaabbb, \cdots \}$
	- $\neq \mathcal{L}(a^{*}b^{*}) \because abb \notin L_{1},\: abb \in \mathcal{L}(a^{*}b^{*})$ 
	- even though $L_{1} \subseteq \mathcal{L}(a^{*}b^{*})$.
> How do we prove that DFA/NFA for $L_{1}$ does not exist?

To show that $L_{1}$ is **not** regular, find a set of **pairwise distinguishable strings** w.r.t. $L$ s.t.
- The set is *infinite*. 
- (Pairwise distinguishable string = each string in set is distinguishable from **all** other strings)
$$\begin{align}
\text{Set }\mathcal{D}&=\{\varepsilon, a, aa, aaa, \dots \}  \\[3pt]
&= \{a^{n}: n \in \mathbb{N}\}  \\[3pt]
&= \mathcal{L}(a^{*})
\end{align}$$
Let $a^{n} \in \mathcal{D}, a^{m} \in \mathcal{D}$ with $m\neq n$.
- $a^{n}b^{n} \in L_{1}$
- $a^{m}b^{n} \not\in L_{1} \because m\neq n$
- Where $b^n$ is a **suffix**
- So **suffix** $b^n$ distinguishes $a^{n}$ from $a^m$.
- $\therefore \mathcal{D}$ is **pairwise distinguishable**.
**Conclusion**: by *Myhill-Nerode Theorem*, **each** DFA for $L_{1}$ has at least $|\mathcal{D}|$ many states.
- But $|\mathcal{D}|=\infty$
- $\therefore L_{1}$ has **no** DFA.
### Example
> $L_{2}=\{s \in\{a, b\}^{*}: |s|\text{ is a power of 2}\}$

$$\begin{align}
\text{Set }\mathcal{D} &=\{a, aa, aaaa, \dots \}\\[3pt]
&= \{a^{2^{n}}: n \in \mathbb{N}\}  
\end{align}$$
Let $\displaystyle a^{2^{m}}, a^{2^{n}}$ with $m\neq n$.
- $\displaystyle a^{2^{n}}a^{2^{n}}=a^{(2^{n} +2^{n)}}=a^{2^{n+1}} \in L_{2}$
-  $\displaystyle a^{2^{m}}a^{2^{n}}=a^{(2^{m} +2^{n)}}=a^{2^{n+1}} \not\in L_{2}$
	- $\because 2^{m}+ 2^{n}$ is **not** a power of 2 when $n\neq m$.

## Other Properties of DFA/NFA/RE
$$\begin{align}
L_{a} &= \{s \in \{a, b\}^{*}: s \text{ ends with an }'a'\} \\[3pt]
L_{e} &= \{s \in \{a, b\}^{*}: s \text{ has an even \# of b's}\} 
\end{align}$$
- $L_{a}$ is **regular**.
	- $\displaystyle\because L_{a}=\mathcal{L}\big((a+b)^{*}a\big)$
	- ![[DFA 6|300]]
	- $\overline{L_{a}} = \{a,b\}^{*}-L_{a}$
### Complement
>Is there a **RE** for $\overline{L_{a}}$?
- **Claim**: $\overline{L_{a}}$ is also **regular**.
	![[DFA 7|250]]
- This generalizes that $\overline{L_{a}}$ always have the corresponding **DFA** .
### Union
> If $L_{1}$ and $L_{2}$ are **regular**, is $L_{1} \cup L_{2}$ **regular**?
- $L_{1}=\mathcal{L}(R_{1})$, $L_{2}=\mathcal{L}(R_{2})$
- $L_{1} \cup L_{2}=\mathcal{L}(R_{1}+R_{2})$
- Therefore, $L_{1} \cup L_{2}$ is **regular**.
### Intersection
> If $L_{1}$ and $L_{2}$ are **regular**, is $L_{1} \cap L_{2}$ **regular**?

Example : **DFA**  for $L_{a} \cap L_{e}$, take **DFA** s $A_{a}, A_{e}$.
Remind: $$\begin{align}
L_{a} &= \{s \in \{a, b\}^{*}: s \text{ ends with an }'a'\} \\[3pt]
L_{e} &= \{s \in \{a, b\}^{*}: s \text{ has an even \# of b's}\} 
\end{align}$$
![[DFA 8]]
#### Product Construction $A_{a} \times A_{e}$
![[DFA 9]]
Also, note that $L_{1} \cap L_{2} = \overline{L_{1}} \cup \overline{L_{2}}$.
### NFA to DFA
![[DFA 10]]
- Create a DFA with **one state for each set** of states of the NFA.
	- $q_{0}:\{r_{0}\}$
	- $q_{1}:\{r_{0}, r_{1}\}$
	- $q_{2}: \{r_{0}, r_{2}\}$
	- $q_{3}: \{r_{0}, r_{1}, r_{2}\}$
![[DFA 11|500]]
- This is called **Subset Construction**
	- It demonstrates that every **NFA**  can be converted into **DFA** .
### RE to NFA
There are three basic expressions: 
![[NFA 1]]
- $\varnothing$ : No matter what string is being read, it is **no state** at all. 
	- (which does not contain accepting state)
- $\varepsilon$ : Starts in one accepting state, if there's any character then it will not accept.
---
#### Union
> Let $R_{1}$ has NFA $A_{1}$, $R_{2}$ has NFA $A_{2}$.

Then $R_{1} + R_{2}$ is  NFA $A_{1}A_{2}$.
Visually, 
![[NFA 2]]
#### Concatenation
> $R_{1}R_{2}$
- Initial states: those of $A_{1}$
- Accepting states: those of $A_{2}$
- Each transition into an old accepting state of $A_{1}$ is duplicated into each old start states of $A_{2}$
Example: $a(a+b)$
![[NFA 3|500]]
#### Kleene Star (\*)
> $R_{1}^*$

![[NFA 4]]
