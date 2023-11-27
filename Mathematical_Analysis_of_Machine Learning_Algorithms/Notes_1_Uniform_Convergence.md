### The Union Bound
![image.png](https://raw.githubusercontent.com/chxliou/chenxi-notes/main/utils/202311271218599.png)
This question is designed to show one property of **Union Bound**: the union bound is relatively tight when events are independent, and the probability is small.

**Proving Union Bound** To make an additive decomposition, we need to separate $E_1 \cup \cdots \cup E_m$ into disjoint parts. Let $B_i:= \cap_{j<i} E_j^c$ be the event that none of the first $i-1$ events occur. 
Therefore
$$
\begin{aligned}
& \Pr(E_1 \cup \cdots \cup E_m) \\
= & \Pr(E_1 \cup B_1E_2 \cup \cdots \cup B_mE_m) \\ 
= & \Pr(E_1) + \sum_{i=2}^m\Pr(B_iE_i) \\
= & \Pr(E_1) + \sum_{i=2}^m(\Pr(E_i) - \Pr(B_i^cE_i)) \\
= & \sum_{i=1}^m\Pr(E_i) - \sum_{i=2}^m \Pr(B_i^cE_i)
\end{aligned}
$$
Therefore, we have $\Pr(E_1 \cup \cdots \cup E_m) \leq \sum_{i=1}^m\Pr(E_i)$.

**Proving the tightness of Union Bound** Observing $B_i^cE_i = E_i(\cup_{j<i}E_j)=\cup_{j<i}E_iE_j$ , the union bond tells us that $\Pr(B_i^cE_i) = \Pr(\cup_{j<i}E_iE_j)\le \sum_{j<i}\Pr(E_iE_j).$  Therefore, 
$$
\begin{aligned}
\Pr(E_1 \cup \cdots \cup E_m) & \ge \sum_{i=1}^m\Pr(E_i) - \sum_{i=2}^m \sum_{j<i}\Pr(E_iE_j) \\
& = \sum_{i=1}^m\Pr(E_i) - \sum_{i=2}^m \sum_{j<i}\Pr(E_i)\Pr(E_j)\\
& = \sum_{i=1}^m\Pr(E_i) - 0.5 (\sum_{i=2}^m \sum_{j<i}2\Pr(E_i)\Pr(E_j))\\
& = \sum_{i=1}^m\Pr(E_i) - 0.5 (\sum_{i=1}^m \Pr(E_i))^2 +0.5\sum_{i=1}^m \Pr(E_i)^2 \\
& \ge \sum_{i=1}^m\Pr(E_i) - 0.5 (\sum_{i=1}^m \Pr(E_i))^2
\end{aligned}
$$


### PAC Learnability
![image.png](https://raw.githubusercontent.com/chxliou/chenxi-notes/main/utils/202311271218601.png)
**I.I.D. Assumption.** Assume we call an oracle$\mathcal{O}$to return$n$i.i.d. samples from an unknown distribution$\mathcal{D}.$

- True function to learn $f _ { * } ( x )$
- Feature $X \sim \mathcal{D},$  label $Y=f_*(X),$training data $S _ { n } = \{ ( X _ { i } , Y _ { i } ) \} _ { i = 1 , \cdots , n } \sim \mathcal{D} ^ { n }$
- Generalization error $\text { err } _ { D } ( f ) = \mathbb{E} _ { X \sim D } \mathbb{1} ( f ( x ) \neq f _ { * } ( x ) )$
- Training error $\widehat{\text { err } }_ { S_n } ( f ) = \frac { 1 } { n } \sum _ { i = 1 } ^ { n } 1 ( f ( X _ { i } ) \neq Y _ { i } )$
This assumption is necessary to apply the Chernoff bound.

**The Realizability Assumption** There exists $f \in \mathcal{C}$ s.t.  $\text { err } _ { D } ( f ) =0.$ 
Otherwise, no learner can produce a valid function (if $\mathcal{C}$ is a finite set).
![image.png](https://raw.githubusercontent.com/chxliou/chenxi-notes/main/utils/202311271218602.png)
**Learning Decision List** Define a map: $g: A \mapsto \{ (j,a,b):\forall k \in A, (X_{kj}=a)\implies (Y_k=b)\}.$ We initiate $A_1:=[n]$ and randomly pick one element in $g(A_1)$ as $(i_1, a_1, b_1).$ We update $A_2:=A_1\setminus \{k: X_{ki_1}=a_1\},$ then randomly pick one element in $g(A_2)$ as $(i_2, a_2, b_2)$ with the constraint that $i_2$ is not occupied before. After $d$ iterations, the left examples have only one choice for their values; therefore, they share the same label value. Take that value as $b_{d+1}.$ As a result, the training error can always be reduced to 0 with this algorithm. In addition, since the total number of candidate functions is finite, the decision list is PAC learnable because we can apply the uniform convergence result to this setting.
