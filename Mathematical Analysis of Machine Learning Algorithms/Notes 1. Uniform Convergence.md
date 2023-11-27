### The Union Bound
![image.png](https://cdn.nlark.com/yuque/0/2023/png/1044864/1700885739277-8e603e01-cfb8-4e72-b105-1cb42f5f22f1.png#averageHue=%23fbfaf9&clientId=u015fcbda-a463-4&from=paste&height=189&id=u885c9e48&originHeight=189&originWidth=932&originalType=binary&ratio=1&rotation=0&showTitle=false&size=49615&status=done&style=none&taskId=u1b07cf33-c91d-468c-bb41-062c4bd224d&title=&width=932)
This question is designed to show one property of **Union Bound**: the union bound is relatively tight when events are independent, and the probability is small.

**Proving Union Bound** To make an additive decomposition, we need to separate $E_1 \cup \cdots \cup E_m$into disjoint parts. Let $B_i:= \cap_{j<i}E_j^c$ be the event that none of the first $i-1$events occur. 
Therefore$$\begin{aligned}
& \Pr(E_1 \cup \cdots \cup E_m) \\
= & \Pr(E_1 \cup B_1E_2 \cup \cdots \cup B_mE_m) \\ 
= & \Pr(E_1) + \sum_{i=2}^m\Pr(B_iE_i) \\
= & \Pr(E_1) + \sum_{i=2}^m(\Pr(E_i) - \Pr(B_i^cE_i)) \\
= & \sum_{i=1}^m\Pr(E_i) - \sum_{i=2}^m \Pr(B_i^cE_i)
\end{aligned}$$
Therefore, we have $\Pr(E_1 \cup \cdots \cup E_m) \leq \sum_{i=1}^m\Pr(E_i)$.
**Proving the tightness of Union Bound** Observing $B_i^cE_i = E_i(\cup_{j<i}E_j)=\cup_{j<i}E_iE_j$, the union bond tells us that $\Pr(B_i^cE_i) = \Pr(\cup_{j<i}E_iE_j)\le \sum_{j<i}\Pr(E_iE_j).$  Therefore, $$\begin{aligned}
\Pr(E_1 \cup \cdots \cup E_m) & \ge \sum_{i=1}^m\Pr(E_i) - \sum_{i=2}^m \sum_{j<i}\Pr(E_iE_j) \\
& = \sum_{i=1}^m\Pr(E_i) - \sum_{i=2}^m \sum_{j<i}\Pr(E_i)\Pr(E_j)\\
& = \sum_{i=1}^m\Pr(E_i) - 0.5 (\sum_{i=2}^m \sum_{j<i}2\Pr(E_i)\Pr(E_j))\\
& = \sum_{i=1}^m\Pr(E_i) - 0.5 (\sum_{i=1}^m \Pr(E_i))^2 +0.5\sum_{i=1}^m \Pr(E_i)^2 \\
& \ge \sum_{i=1}^m\Pr(E_i) - 0.5 (\sum_{i=1}^m \Pr(E_i))^2
\end{aligned}$$

### PAC Learnability
![image.png](https://cdn.nlark.com/yuque/0/2023/png/1044864/1700988238868-35597bb4-ca0f-45d1-8174-e9ab94ceba5f.png#averageHue=%23f9f7f5&clientId=uac4fe65e-c54b-4&from=paste&height=214&id=ud5b4d439&originHeight=214&originWidth=737&originalType=binary&ratio=1&rotation=0&showTitle=false&size=98855&status=done&style=none&taskId=u16a3e4e5-24e8-43d4-8d43-fa13a18e01e&title=&width=737)
**I.I.D. Assumption.** Assume we call an oracle$\mathcal{O}$to return$n$i.i.d. samples from an unknown distribution$\mathcal{D}.$

- True function to learn $f _ { * } ( x )$
- Feature $X \sim \mathcal{D},$  label $Y=f_*(X),$training data $S _ { n } = \{ ( X _ { i } , Y _ { i } ) \} _ { i = 1 , \cdots , n } \sim \mathcal{D} ^ { n }$
- Generalization error$\operatorname { err } _ { D } ( f ) = \mathbb{E} _ { X \sim D } \mathbb{1} ( f ( x ) \neq f _ { * } ( x ) )$
- Training error $\widehat{\operatorname { err } }_ { S_n } ( f ) = \frac { 1 } { n } \sum _ { i = 1 } ^ { n } 1 ( f ( X _ { i } ) \neq Y _ { i } )$

This assumption is necessary to apply the Chernoff bound.
**The Realizability Assumption** There exists$f \in \mathcal{C}$s.t. $\operatorname { err } _ { D } ( f ) =0.$
Otherwise, no learner can produce a valid function (if$\mathcal{C}$is a finite set).
![image.png](https://cdn.nlark.com/yuque/0/2023/png/1044864/1700990552215-09349473-b31e-462f-9825-5ae84720c19a.png#averageHue=%23b7b9d7&clientId=uac4fe65e-c54b-4&from=paste&height=181&id=u3b390aae&originHeight=181&originWidth=701&originalType=binary&ratio=1&rotation=0&showTitle=false&size=29946&status=done&style=none&taskId=ufd453b2c-2419-4e8e-8465-f4454bfb612&title=&width=701)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/1044864/1700982127639-6566f49f-0d79-4d17-8ab5-2e2c73cf1059.png#averageHue=%23f8f6f5&clientId=uac4fe65e-c54b-4&from=paste&height=166&id=u5f8ee5f4&originHeight=166&originWidth=890&originalType=binary&ratio=1&rotation=0&showTitle=false&size=89161&status=done&style=none&taskId=u1709574f-f6ec-40e6-a49e-76babc364c4&title=&width=890)
**Learning Decision List **Define a map:$g: A \mapsto \{ (j,a,b):\forall k \in A, (X_{kj}=a)\implies (Y_k=b)\}.$We initiate$A_1:=[n]$and randomly pick one element in $g(A_1)$as $(i_1, a_1, b_1).$We update $A_2:=A_1\setminus \{k: X_{ki_1}=a_1\},$then randomly pick one element in $g(A_2)$as $(i_2, a_2, b_2)$with the constraint that $i_2$is not occupied before. After$d$iterations, the left examples have only one choice for their values; therefore, they share the same label value. Take that value as $b_{d+1}.$As a result, the training error can always be reduced to 0 with this algorithm. In addition, since the total number of candidate functions is finite, the decision list is PAC learnable because we can apply the uniform convergence result to this setting.