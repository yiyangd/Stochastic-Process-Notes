## Stochastic Process 03 - Classification of Markov Chain States


### 1. Relations Between States

#### 1.1. Accessible
State $j$ is said to be **accessible** from state $i$ if 
$$P_{ij}^n>0 \  \text{ for some } \  n \geq 0$$
- this implies that state $j$ is **accessible** from state $i$ if and only if, *starting in i*, it is possible that *the process will ever enter state j* .

$$i \rightarrow j$$

#### 1.2. Communication
Two states $i$ and $j$ that are **accessible to each other** are said to **communicate**, and we write

$$ i \leftrightarrow j$$

- The **relation of communication** satisfies the following *three properties*:
- (i. Reflexive) **Any state $i \geq 0$ communicates with itself** $$i\leftrightarrow i$$
  since, by definition, 
  $$P_{ii}^0 = P \{X_0 = i|X_0 = i\} = 1$$
- (ii. Symmetric) If state $i$ communicates with state $j$ , then state $j$ communicates with state $i$. $$\text{if } \ i\leftrightarrow j, \ \text{ then } j\leftrightarrow i$$
- (iii. Transitive) If state i communicates with state j , and state j communicates with state k, then state i communicates with state k. $$\text{if } \ i\leftrightarrow j \ \text{ and } \  j \leftrightarrow k, \ \text{ then } i\leftrightarrow k$$ **Proof:** Since there exist integers n and m such that $$P_{ij}^n > 0, P_{jk}^m > 0$$ Now by the *Chapman-Kolmogorov Equations*, we have $$P_{ik}^{n+m} = \sum_{r=0}^\infty P_{ir}^n P_{rk}^m \geq P_{ij}^n P_{jk}^m > 0$$ Hence, state $k$ is accessible from state $i$. Similarly, we can show that state $i$ is accessible from state $k$. Hence $$i\leftrightarrow k$$

#### 1.3. Classes of States
**Two States that communicate** are said to be in the **same class**.
- It is an easy consequence of (i), (ii), and (iii) that **any two classes of states** are either *identical* or *disjoint*.
- In other words, the concept of communication **divides the state space up into a number** of *Separate Communicating Classes*

#### 1.4. Irreducible and Reducible Chain

The Markov chain is said to be **Irreducible** if there is **ONLY ONE class**, 
- that is, if **ALL States communicate with each other** in a *finite number of steps* (with *positive probability*).
  - for any States $i,j$ there is some positive integer $n$ such that $P^n_{ij} > 0$
- A Markov chain that is not irreducible is called reducible.
### 2. Classification of States by Number of Visits

#### 2.1. Introduction
**The states of a Markov chain** can be **classified** as *recurrent* or *transient*, 
- depending on whether they are *visited over and over again in the long run* or are *eventually abandoned*.


![Left: 4-state Markov chain with ALL states recurrent. Right: 6-state Markov chain with states 1, 2, and 3 transient.](https://files.mdnice.com/user/1474/249859b9-1c11-482b-996b-3fa7cdc5a76a.png)

- In the Markov chain shown on the left, a particle moving around between states will *continue to spend time in ALL 4 states in the long run*, 
  - since **it is possible** to *get from any state to any other state*.
- In contrast, consider the chain on the right, and let the particle start at state 1. 
  - For a while, the chain may linger in the triangle formed by states 1, 2, and 3, but *eventually it will reach state 4*, and from there it can **never return to states 1, 2, or 3**. 
    - States 1, 2, and 3 are *Transient*
  - It will then **wander around between states 4, 5, and 6 forever**. 
    - States 4, 5, and 6 are *Recurrent*.

#### 2.2. Definition of Recurrent and Transient States
For any state $i$ we **let $f_i$ denote the probability** that, *starting in state $i$*, the *process will ever reenter state $i$*.
- **State $i$** of a Markov chain is *Recurrent* 
  - if *starting from $i$*, the *probability is 1* that *the chain will eventually return to $i$*.  $$f_i=1$$
  - it follows that the process will *reenter state $i$ infinitely many times* (assuming the process ever get to $i$)
  - so the **Expected Number of Visits that the process is in state $i$ is Infinite** if *starting in $i$*

- Otherwise, the **State $i$** is *Transient*, which means that 
  - if *the chain starts from $i$*, there is *a positive probability* of *ever returning to $i$*. $$f_i < 1$$
  - it follows that the process will *never return to $i$* with probability $$1-f_i$$  So, **N, the Number of Visits to $i$** (including visit at time 0) has a **Geometric Distribution** $$P(N=n|X_0=i)=f_i^{n-1}(1-f_i)$$ 
    $$n=1,2,...$$ 
    with *Finite Mean* $$E(N|X_0=i)=\frac{1}{1-f_i}$$

#### 2.3. Proposition
**State $i \ $**  is  

$$\text{Recurrent iff} \ \sum^{\infty}_{n=1}P^n_{ii}=\infty$$
$$\text{Transient iff} \ \sum^{\infty}_{n=1}P^n_{ii}<\infty$$

**Proof:**
- Let 
$$I_n = \cases{
1, \text{if } \ X_n = i  \\
0, \text{if } \ X_n \neq i
}$$
- We have the number of visits that the process is in state $i$
$$ N = \sum^{\infty}_{n=0}I_n$$
- Then,
$$ 
\begin{aligned}
E(N | X_0=i) &= E(\sum_{n=0}^{\infty}I_n | X_0 = i) \\
             &= \sum_{n=0}^{\infty} E(I_n | X_0=i) \\
             &= \sum_{n=0}^{\infty} P(X_n=i | X_0 = i) \\
             &= \sum_{n=0}^{\infty} P_{ii}^n
\end{aligned}
$$
- if **State $i$ is Recurrent**, the *expected value is Infinite* 
- if **State $i$ is Transient**, it will *ONLY be visited a Finite number of times*
  - this implies that for a *Finite-State Markov Chain*, **NOT ALL States can be Transient**
    - if ALL States are Transient, after a Finite Time, *NO States will be Visited*, which is a Contradiction to the *process must be in some state*
    - so, **At Least ONE of the States MUST be Recurrent**.
- this proposition can be used to show that **Recurrence is a Class Property**
#### 2.4. Class Property
If ONE state in a **Communicating Class** is *Recurrent*, then *ALL States in its Class are Recurrent*
- If state $i$ is recurrent, and  , then state $j$ is recurrent

**Proof:**
- Let **State $i$ be a Recurrent State**, so
$$\sum_{n=1}^{\infty} P_{ii}^n=\infty$$
- Assume state $i$ and $j$ **communicate**, then there exist integers $k$ and $m$ such that
$$P^k_{ij} > 0, \ P^m_{ji} > 0$$
- Now, for any integer $n$, 

$$P_{jj}^{m+n+k} \geq P_{ji}^{m} P_{ii}^{n} P_{ij}^{k}$$

- This follows the probability of going from $j$ to $j$ in $m + n + k$ steps via a path that goes from $j$ to $i$ in $m$ steps, then from $i$ to $i$ in an additional $n$ steps, then from $i$ to $j$ in an additional $k$ steps.
- Summing Over $n$,
$$\sum^{\color{red}\infty}_{\color{red}{n=1}}P_{jj}^{m+n+k} \geq \underbrace{\sum^{\color{red}\infty}_{\color{red}n=1}P_{ji}^{m} P_{ii}^{\color{red}n} P_{ij}^{k}}_{=\underbrace{P_{ji}^{m}}_{>0} \underbrace{P_{ij}^{k}}_{>0} \underbrace{\sum^{\color{red}\infty}_{\color{red}n=1}P_{ii}^{\color{red}n}}_{=\infty} \ = \ \infty}  $$
- by Proposition from 2.3, state $j$ is also **Recurrent**
- this also means that *Transience* is a *Class Property*: 
  - if a state in a **Communicating Class** is *Transient*, then its class is *Transient*

  
  
### 3. Classification of States by Period

Another way to **classify states** is *according to their periods*. 
- The *period of a state* summarizes *how much time can elapse between successive visits to the state*.

#### 3.1. Definition 

The **Period $d$ of a State $i$** in a Markov Chain is *the Greatest Common Divisor (gcd)* of **the possible numbers of steps** it can take *to return to $i$ when starting at $i$*


$$d = \gcd  \{n: P_{ii}^n > 0\}$$
- The **period of $i$ is $d=\infty$** if it’s *impossible ever to return to $i$ after starting at $i$*.

- A State is called **Periodic** if its *period $d > 1$*

- A State is called **Aperiodic** if its *period $d = 1$*
  - the Chain is called **Aperiodic** if *ALL its states are aperiodic*, and periodic otherwise.
- **Periodicity** is a *Class Property*, 
  - if $i \leftrightarrow j$ and $i$ is periodic, then $j$ is periodic
#### 3.2. Example 
![Left: an Aperiodic Markov chain (ALL d = 1). Right: a Periodic Markov chain in which states 1,
2, and 3 have period d = 3.](https://files.mdnice.com/user/1474/249859b9-1c11-482b-996b-3fa7cdc5a76a.png)

- Consider the 6-state chain on the right. **Starting from state 1**, it is **possible** to be **back at state 1** after *3 steps, 6 steps, 9 steps, etc*., 
  - but it is not possible to be back at state 1 after any number of steps that is not a multiple of 3.
  - Therefore, **state 1 has period $d = 3$**. 
  - Similarly, **states 2 and 3 also have period $d=3$**.
- On the other hand, **states 4, 5, and 6 have period $d=1$**, but the chain is **periodic** since *at least one state does NOT have period 1*.
- By contrast, in the chain on the left **ALL States are Aperiodic**, so that **chain is Aperiodic**.

#### Resources:
[1] Sheldon M. Ross, Introduction to Probability Models, Academic Press; 12th edition (2019)

[2] Joseph K. Blitzstein, Jessica Hwang, Introduction to Probability, Chapman and Hall/CRC, 2nd Edition (2019)

[3] Dimitri P. Bertsekas , John N. Tsitsiklis, Introduction to Probability, Athena Scientific; 2nd edition (2008)
