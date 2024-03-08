## Stochastic Process 02 - Markov Chains

### 0. Intro to Markov Chain
Markov Chains were first introduced in 1906 by Andrey Markov (of Markov’s in-
equality), with the goal of showing that the law of large numbers can apply to
random variables that are NOT independent.
- for modeling real-world phenomena, **independence** can be an *excessively restrictive assumption*:
  - it means that the $X_n$ provide **absolutely NO information** about each other.
  - At the other extreme, allowing arbitrary interactions between the $X_n$ makes it very difficult to compute even basic things.
- A Markov chain is a sequence of r.v.s that exhibits **one-step dependence**, in a precise sense that we shall soon
define. 
  - Thus Markov chains are a *happy medium* between **complete independence**
and **complete dependence**.
### 1. One-Step Transition Probability

$$

$$

Let $\{X_n , n = 0, 1, 2, . . .\}$ be a **stochastic process** that takes on a *finite or countable* number of possible values in the **State Space $S = \{0, ... , h\}$**.
- If $X_n = i$, then **the process** is said to be **in state $i$ at time $n$**.

- suppose that **whenever the process is in state $i$**, there is a (fixed) **Transition Probability $P_{ij}$** that it **will next be in state $j$**, that is 
  $$P_{i,j} = P \{X_{n+1} = j \ | \ X_n = i\}, \ \ i,j \in S$$


### 2. Markov Property
The *key assumption underlying Markov Chains* is that the **transition probabilities $P_{ij}$** apply whenever **state i is visited**, 
- **NO matter what** happened in the past, and **NO matter how** state i was reached.
- Mathematically, we assume the **Markov property** , which requires that   for *all (earlier) states* $i_0 , i_1 , \cdots , i_{n−1}$, *ALL states* $\ i, \ j$ and ALL times $n\geq0$

$
  \begin{aligned}
  &P \{X_{n+1} = j \ | \ X_n = i, X_{n-1}=i_{n-1}\cdots,  X_0 = i_0 \} \\
  = &P \{X_{n+1} = j \ | \ X_n = i\} = P_{i,j}
  \end{aligned}
$ 


- Such a **stochastic process** is known as a **Markov chain**.

**Interpretation**: 
- for a Markov chain, the **conditional distribution** of any *future state $X_{n+1}$* , **given** the *past states $X_0 , X_1 , . . . , X_{n−1}$* and the *present state $X_n$* , is 
  - **independent of the past states** and 
  - **depends only on the present state**.


### 3. Transition Probability Matrix

All of the elements of a Markov chain model can be encoded in a $(h+1) \times (h+1)$ **transition probability matrix**,
  
$$
P = 
\begin{pmatrix}
P_{0,0} & P_{0,1} & \cdots & P_{0,h} \\
P_{1,0} & P_{1,1} & \cdots & P_{1,h} \\
\vdots & \vdots & \vdots & \vdots \\
P_{h,0} & P_{h,1} & \cdots & P_{h,h} 
\end{pmatrix}
$$

- the transition probabilit $P_{ij}$ is **nonnegative**, and *each row in matrix sums to 1*:
  $$\sum_{j=0}^{h} P_{i,j} = 1, \ \ \ \text{for ALL} \ \ i$$
- because the *process must make a transition into some state*, ALL states are disjoint and their union has probability 1



### 4. N-Step Transition Probability

$$

$$

Many Markov chain problems require the **calculation of the probability of
the state at some future time**, *conditioned on the current state*. 
- this probability is captured by the **n-step transition probabilities $P_{ij}^n$**, defined by 

$$
P_{ij}^n = P\{X_{k+n} = j \ | X_k = i\},
k, n \geq 0
$$

-  In words, this is the **probability** that *a process in state i will be in state j*  after *n additional transitions* (time periods)
- It can be calculated using the following **basic recursion**, known as the **Chapman-Kolmogorov equation**.

### 5. Chapman-Kolmogorov Equations

$$

$$

$
\begin{aligned}
& P_{ij}^{n+m} = P(X_{n+m}=j | X_0 = i)\\
&=  \sum_{k=0}^\infty P(X_{n+m}=j, X_n = k | X_0 = i) \\
&=  \sum_{k=0}^\infty P(X_{n+m}=j |X_n = k, X_0 = i) P(X_n = k | X_0 = i)\\
  & \  \ \ \ \color{blue} \text{(By Markov Property)} \\
&=  \sum_{k=0}^\infty P(X_{n+m}=j |X_n = k) P(X_n = k | X_0 = i) \\
&= \sum_{k=0}^\infty P_{kj}^m P_{ik}^n \\
&= \sum_{k=0}^\infty P_{ik}^n P_{kj}^m \ \ \ \ \text{for ALL} \ \ i,j, n, m \geq 0
\end{aligned}
$

- $P_{ik}^n P_{kj}^m$ represents the probability that **starting in i** the process will **go to state j** in **n + m transitions** through a path which **takes it into state k** at the **$n^{th}$ transition**.
  - **summing over ALL intermediate states k** yields the *probability that the process will be in state j after $n + m$ transitions*.

- If we let $P^{(n)}$ denote the **matrix of n-step transition probabilities** $P_{ij}^n$ , then

$$
P^{(n+m)} = P^{(n)}  P^{(m)}
$$

- Since

$$
 P^{(2)} = P^{(1+1)} = P^{(1)}  P^{(1)} = P  P = P^2
$$

- By Induction

$$
 P^{(n)} = P^{(n-1+1)} = P^{(n-1)} P^{(1)} = P^n
$$

- That is, the **n-step transition matrix** may be obtained by **multiplying the matrix $P$ by itself $n$ times**.



#### Example: Weather Prediction
> Suppose that on any given day, the weather can either be rainy (R) or sunny (S). Assume that tomorrow’s weather **depends on ONLY today’s weather** but *NOT on past days*.
> - If today is rainy, then tomorrow will be rainy with probability 0.7 and sunny with probability 0.3.
> - If today is sunny, then tomorrow will be rainy with probability 0.4 and sunny with probability 0.6.
> - **Calculate the probability** that *it will rain four days from today* given that *it is raining today*.
>  

**Solution:**
- Letting $X_n$ be the weather on day n, $X_0 , X_1 , X_2 , . . .$ is a **Markov Chain** on the **state space** {R, S}

- The one-step transition probability matrix is given by:

$$
P = 
\begin{pmatrix}
0.7 & 0.3  \\
0.4 & 0.6 
\end{pmatrix}
$$
- Hence
$
\begin{aligned}
\\
&P(X_2 =R|X_0=R)
= P(X_{1+1} =R|X_0=R)\\
\\
&=P^{(1+1)} = P^{(1)}P^{(1)} = \begin{pmatrix}
0.7 & 0.3  \\
0.4 & 0.6 
\end{pmatrix}
\begin{pmatrix}
0.7 & 0.3  \\
0.4 & 0.6 
\end{pmatrix}\\
&=
\begin{pmatrix}
0.61 & 0.39  \\
0.52 & 0.48 
\end{pmatrix} = P^{(2)}
\end{aligned}
$
$
\begin{aligned}
\\
&P(X_4 =R|X_0=R)
= P(X_{2+2} =R|X_0=R)\\
\\
&=P^{(2+2)} = P^{(2)}P^{(2)} = \begin{pmatrix}
0.61 & 0.39  \\
0.52 & 0.48 
\end{pmatrix}
\begin{pmatrix}
0.61 & 0.39  \\
0.52 & 0.48 
\end{pmatrix}\\
&=
\begin{pmatrix}
0.575 & 0.425  \\
0.567 & 0.433 
\end{pmatrix}
\end{aligned}
$
- the desired probability that *it will rain four days from today* given that *it is raining today* is

$$P_{00}^4 = 0.575$$
#### Example: Number of Flips until HHH occurs
> In a sequence of independent flips of a fair coin, let $N$ denote **the number of flips until there is a run of three consecutive heads (HHH)**. 
> - Find $$P(N \leq 8) \ \text{and} \  P(N = 8)  $$

**Solution:**  
- To determine $P (N ≤ 8)$, define a *Markov Chain* with states 0, 1, 2, 3 where 
  - for $i < 3$, *state i* means that we currently are on *a run of i consecutive heads*,
and where
  - *state 3* means that *a run of three consecutive heads has already occurred*.
- Thus, the **Transition Probability Matrix** is

$$
P = 
\begin{pmatrix}
1/2 & 1/2 & 0 & 0 \\
\color{blue} 1/2 & 0 & \color{blue}1/2 & 0 \\
1/2 & 0 & 0 & 1/2 \\
0 & 0 & 0 & 1 
\end{pmatrix}
$$

- where, for instance, **the values for row 2** are obtained by noting that if we currently are *on a run of size 1 then the next state will be 0* if the next flip is a tail, or 2 if it is a head.

$$
P_{1,0} = P_{1,2} = 1/2
$$
- Because there would be **a run of three consecutive heads within the first 8 flips** if and only if $X_8 = 3$, the disired probability is $P_{0,3}^8$.
- Squaring $P$ to obtain $P^2$ , then squaring the result to obtain $P^4$, and then squaring that matrix gives the result
$$
P^8 = \begin{pmatrix}
\frac{81}{256} & \frac{44}{256} & \frac{24}{256} & \color{red}\frac{107}{256} \\
\frac{68}{256} & \frac{37}{256} & \frac{20}{256} & \frac{131}{256} \\
\frac{44}{256} & \frac{24}{256} & \frac{13}{256} & \frac{175}{256} \\
0 & 0 & 0 & 1 \\
\end{pmatrix}
$$

- Hence, the ***probability that there will be a run of three consecutive heads within the first eight flips*** is 107/256 ≈ .4180.

- To determine $P (N = 8)$, noting that $N = 8$ if the pattern hasn’t yet occurred in the first 7 transitions, the state after 7 transitions is 2, and the next flip lands heads, shows that

$$P(N=8) = \frac{1}{2}P_{0,2}^7$$


#### Resources:
[1] Sheldon M. Ross, Introduction to Probability Models, Academic Press; 12th edition (2019)

[2] Dimitri P. Bertsekas , John N. Tsitsiklis, Introduction to Probability, Athena Scientific; 2nd edition (2008)

[3] Joseph K. Blitzstein, Jessica Hwang, Introduction to Probability, Chapman and Hall/CRC, 2nd Edition (2019)
