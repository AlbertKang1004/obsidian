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
 
 