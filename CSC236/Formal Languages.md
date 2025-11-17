\[= Sets of `string`s\]
## Example 1: L-R Game

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
### Deterministic Finite Automata (DFA)
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
## Example 2
$$\{s\in\{a,b\}^{*}: |s|\geq 2\text{ and 2nd-last char of }s \text{ is an }a\}: $$