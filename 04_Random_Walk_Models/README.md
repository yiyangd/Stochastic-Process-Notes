## Stochastic Process 04 - Random Walk Model, Gambler's Ruin Problem and Drug Testing



### 1. Random Walk Model



#### 1.1. Definition and Interpretation


A **Markov Chain** whose state space is given by the integers $i = 0, ±1, ±2, . . .$ is said to be a **Random Walk** if, for some number $0 < p < 1$,
$$
\begin{aligned}
P_{i,i+1} &= p \\
P_{i,i−1} &= 1-p = q
\end{aligned}
$$

- think of it as being a model for an individual walking on a straight line who **at each point of time** either 
  - takes **one step to the right (+1)** with probability $p$ or 
  - **one step to the left (-1)** with probability $q = 1 − p$
  
![](https://files.mdnice.com/user/1474/e9773a3f-af94-4c9e-a05d-94fe8c0b179f.png)

- it could represent **the wanderings of a drunken man** as he *walks along a straight line*. 
- or **the winnings of a gambler** who on each play of the game *either wins or loses one dollar*.

#### Example
> Find the **probability** that *starting at 0*, the chain will be *in state i* after *5 steps* if *p=0.6*

**Solution:**
- The **Possible States** that Random Walk may **Stop** after 5 steps are

$$\{-5, -3, -1, \ 1, \ 3,  \ 5\}$$ 

- The transition matrix is:

![The First Row, First Column is $P_{-5,-5} = 1$](https://files.mdnice.com/user/1474/1f1bde1d-8bd8-488d-bd25-2b74289a8022.png)

- Use Online Matrix Calculator


![](https://files.mdnice.com/user/1474/d8f312bd-1f03-4229-8123-9e7bc8815bd5.png)

- We get $\textbf{P}^5$


![](https://files.mdnice.com/user/1474/7ed1b3b8-d100-4a69-9001-e3a83a896b54.png)

- As a Check

$$
\begin{aligned}
(\textbf{P}^5)_{0,-5} &= \binom{5}{5}(0.4)^5 (0.6)^0 = 0.01024 \\
(\textbf{P}^5)_{0,-3} &=  \binom{5}{4}(0.4)^4 (0.6)^1 = 0.0768\\
(\textbf{P}^5)_{0,-1} &=  \binom{5}{3}(0.4)^3 (0.6)^2  = 0.2304\\
(\textbf{P}^5)_{0,1} &=  \binom{5}{2}(0.4)^2 (0.6)^3  = 0.3456\\
(\textbf{P}^5)_{0,3} &=  \binom{5}{1}(0.4)^1 (0.6)^4  = 0.2592\\
(\textbf{P}^5)_{0,5} &=  \binom{5}{0}(0.4)^0 (0.6)^5  = 0.07776\\
\end{aligned}
$$

#### 1.2. Classification of States


Since $ 0<p<1 $,  **ALL States clearly communicate**, 


- the Chain has *ONE Communicating Class*
- By **Class Property** from 2.4, they are either *ALL Transient* or *ALL Recurrent*
  - so let us consider **State 0** and determine if $$\sum_{n=1}^{\infty}P^n_{00}$$ is *Finite* or *Infinite*
  
  

- Since it is **IMPOSSIBLE TO BE EVEN** (using the gambling model interpretation) after an *ODD NUMBER of Plays*, we must have that



$$P_{00}^{2n-1}=0, \ \ n = 1,2,...$$

- On the other hand, we would be **EVEN after $2n$ Trails** if and only if we *won $n$ of these* and *lost $n$ of these*
  - because each play of the game results in a *win with probability $p$* and a *loss with probability $1 − p$*, 
  - the desired probability is thus the **binomial probability**


$$
\begin{aligned}
P_{00}^{2n} &= P(X_{2n}=0|X_0=0) \\
&=\binom{2n}{n} p^n (1-p)^n \\
&= \frac{(2n)!}{n!n!}(p(1-p))^n
\end{aligned}
$$
$$n = 1,2,3,...$$

For **$p=\frac{1}{2}$**, the preceding process is called a *Symmetric Random Walk*



$$
\begin{aligned}
P_{00}^{2n}  &= \color{red}\frac{(2n)!}{n!n!}\color{black}\left(\frac{1}{4}\right)^{n} \\
& \color{blue}\text{(By Stirling's approximation)} \\
P(X_{2n}=0)& \approx \color{red}\frac{4^n}{\sqrt{\pi n}}\color{black}\frac{1}{4^n} \approx \frac{1}{\sqrt{\pi n}} \approx P(-\frac{1}{2} < X_{2n} < \frac{1}{2})
\end{aligned}
$$ 
  - which shows that $$\sum_{n=1}^{\infty}P_{00}^{2n}=\infty,$$ and thus **ALL States are Recurrent**










#### Example


> Find the **probability** that *the chain will return to state 0*. 

**Solution:**
- Let 
$$\beta = P(\text{chain eventally returns to 0})$$
- To determine $\beta$, start by **conditioning on the initial transition** to obtain

$$
\begin{aligned}
\beta = &P(\text{returns to 0} | X_1=1) \ p \\
        &+P(\text{returns to 0} | X_1=-1)(1-p)
\end{aligned}
$$

- Let 

$$\alpha = P(\text{chain returns to  } 0 \ | \ \text{currently in state } 1 )$$

- Because the Markov chain will always *increase by 1* with *probability p* or *decrease by 1* with *probability 1 − p* no matter what its current state, note that

$$\alpha = P(\text{chain enters } i-1 \ | \  \text{currently in state } i \ )$$
$$\text{for any } \ i$$

- To obtain an equation for $\alpha$, **condition on the next transition** to obtain
  $$
  \begin{aligned}

  \alpha 
  = \ &P(\text{returns to 0} \ | \ X_1=1, X_2=0)(1-p)\\
    & +P(\text{returns to 0} \ | \ X_1=1, X_2=2) \ p \\
  = \ &1 - p +\color{blue}P(\text{returns to 0} \ | \ X_1=1, X_2=2) \color{black} \ p \\
  = \ & 1 -p + p \ \color{blue}\alpha^2

  \end{aligned}
  $$
  where the final equation follows by noting that in order **for the chain to ever go from state 2 to state 0**, it *must first go to state 1* with *probability $\alpha$*, 
  - and then it *must still go to state 0*, with *conditional probability $\alpha$*, so **$\alpha^2$**

  - The two roots of this equation are
$$\alpha = 1, \text{ and } \alpha = \frac{1-p}{p}$$

- In the case of the **Symmetric Random Walk** where **p = 1/2**, we can conclude that  $$\alpha = \frac{1-p}{p} = 1 $$
  By *Symmetry*, 
  $$P(\text{returns to 0} | X_1=1) = P(\text{returns to 0} | X_1=-1)$$
  $$=f_0=\beta=\alpha=1$$ 
  proving that **ALL States of a Symmetric Random Walk** are *Recurrent*

- In the case of the **NonSymmetric Random Walk** where **p > 1/2**, 
  $$P(\text{returns to } 0 \ | \ X_1 = −1) = 1$$
  and since *the random walk is transient* in state 0, then 
  $$\beta = \alpha p + 1 - p < 0$$
  Using $\alpha = \frac{1-p}{p}$, we get
  $$\beta=2(1-p), \ p > 1/2$$

- In the case of the **NonSymmetric Random Walk** where **p <  1/2**, 
  $$P(\text{returns to } 0 \ | \ X_1 = 1) = 1$$
  and we need $P(\text{returns to } 0 \ | \ X_1 = −1)$, let 
  $$
  \begin{aligned}
  \alpha^{*}  
  = \ &P(\text{returns to 0} \ | \ X_1=-1, X_2=0) \ p\\
  & +P(\text{returns to 0} \ | \ X_1=-1, X_2=-2) \ (1-p) \\
  = \ &p +\color{blue}P(\text{returns to 0} \ | \ X_1=-1, X_2=-2) \color{black} \ (1-p) \\
  = \ & 1 -p + p \ \color{blue}(\alpha^*)^2
  \end{aligned}
  $$
  when $X_2 = -2$, the chain must return to -1 with **probability $\alpha^*$** and then to 0 with **probability $\alpha^*$**
  
  - The two roots of this equation are
  $$\alpha^* = 1, \text{ and } \alpha^* = \frac{p}{1-p}$$
  - and since *the random walk is transient* in state 0, then $$\beta = \alpha^* p + (1 - p) < 1$$
  Using $\alpha = \frac{p}{1-p}$, we get
  $$\beta=2p, \ p < 1/2$$

- Finally, the **probability** that *the chain will return to state 0* is

$$P(\text{returns to 0}) = 2 \min (p, 1 − p)$$


















### 2. Gambler's Ruin Problem


#### 2.1. Definition
Consider a **Gambler** who, at each play of the game, either 
- **wins 1 dollar** with **probability $p$** or 
- **loses 1 dollar** with **probability $1 − p$**.   

If we suppose that the Gambler **quits playing** either when 
- he *goes broke* or 
- he *attains a fortune of N dollars*   

If we let **$X_n$** denote the **player’s fortune at time n**, then **the process $\{X_n, n = 0,1,2,...\}$** is a **Markov Chain** with transition probabilities 


$$
\begin{aligned}
P_{i,i+1} &= p \\
P_{i,i−1} &= 1-p = q
\end{aligned}
$$ 


for $i = 1,2,...,N-1$ and $$P_{00} = P_{NN} = 1$$

We can visualize this game as a *finite state random walk* on the integers between 0 and N
- the **game ends** when *the random walk reaches 0 or N*

![](https://files.mdnice.com/user/1474/7bd757a3-f419-41f1-9dc9-f20d64271ba4.png)


  - **States 0 and N** are called **Absorbing States** since *once entered they are never left*.
    - Therefore, This Markov chain has **three classes**, namely, {0}, {1, 2, ... , N − 1}, and {N}, 
    - *States 0 and N* are *Recurrent*, and *ALL other states* are *Transient*


![](https://files.mdnice.com/user/1474/f7407197-be4e-4bee-9fd4-506bda3d6075.png)



- The chain is **reducible** because *from state 0* it is *only possible to go to state 0*, and *from state N*  it is *only possible to go to state N*

- Since each **transient state $\{1,2, ..., N-1\}$** is visited only *finitely often*, it follows that, after some *finite amount of time*, the gambler will **either attain his goal of N or go broke**.


#### Example
> *Starting with 5 dollars* and *p=0.45*, and the Gambler's will *stop* if the fortune *attain 10 or 0 dollars*, 
>  - Find the **probability** that, the game will last **less than 20 rounds**?

**Solution:**
- The Transition Matrix for the gambler's fortune is 

![](https://files.mdnice.com/user/1474/61506d23-d1af-41ac-a383-f7b4571c438d.png)

- Then Use Online Matrix Calculator

![https://matrix.reshish.com/power.php](https://files.mdnice.com/user/1474/0bdbcc17-9b85-46a2-8f19-c41e567bad6f.png)

- We get $\textbf{P}^{20}$


![](https://files.mdnice.com/user/1474/556ba50f-3430-42bf-a020-c3a6b8d94930.png)

- So, the **probability** that, the game will last **less than 20 rounds** is:

$$(\textbf{P}^{20})_{5,0}+(\textbf{P}^{20})_{5,10} = 0.41+0.15 = 0.56$$ 

#### 2.2. Probability to Win
> What is the **probability** that, *starting with $i$ dollars*, the Gambler's  fortune will **attain $N$ before reaching 0**?

**Solution:**
- Let **$P_i, i = 0, 1, ..., N$**, denote the probability that, *starting with $i$ dollars*, the **gambler's fortune will eventually reach N**
- This Game has a **Recursive Structure:**
  - after the *first step*, it's exactly the *same game*, except that the Gambler's fortune is now either $i+1$ (win) and $i-1$ (lose)
- By *Law of Total Probability (LOTP)*, conditioning on the outcome of the initial play of the game, we have $
  \begin{aligned}
  P_i = &P(\text{reaches N} | \text{starts at i, wins}) \cdot p \\
  &+ P(\text{reaches N} | \text{starts at i, loses}) \cdot q\\
  = &P(\text{reaches N} | \text{starts at i+1}) \cdot p \\
  &+ P(\text{reaches N} | \text{starts at i - 1}) \cdot q\\
  = &P_{i+1} \cdot p + P_{i-1} \cdot q,  \ \ (i = 1,2,...,N-1)
  \end{aligned}
  $

- Since $p + q = 1$,

$$
\begin{aligned}
P_i 
= P_i \cdot 1 = &P_i \cdot (p+q)\\
= &P_{i} \cdot p + P_{i} \cdot q \\

\end{aligned}
$$ 
- Hence,

$$
\begin{aligned}
P_{i} \cdot p + P_{i} \cdot q &= P_{i+1} \cdot p + P_{i-1} \cdot q \\
P_{i+1} - P_{i} &=\frac{q}{p}(P_i - P_{i-1}) \\
i = 1, 2, &..., N-1
\end{aligned}
$$
- Since $P_0 = 0$, we have

$
\begin{aligned}
P_{2} - P_{1} =\frac{q}{p}(&P_1 - P_{0})=\frac{q}{p}P_1 \\
P_{3} - P_{2} =\frac{q}{p}(&P_2 - P_1)=(\frac{q}{p})^2P_1 \\
&\vdots\\
P_{i} - P_{i-1} =\frac{q}{p}(&P_{i-1} - P_{i-2})=(\frac{q}{p})^{i-1}P_1 \\
&\vdots\\
P_{N} - P_{N-1} =\frac{q}{p}(&P_{N-1} - P_{N-2})=(\frac{q}{p})^{N-1}P_1 \\
\end{aligned}
$
- Adding the first $i-1$ of these equations yields 

$
\begin{aligned}
P_i-&P_1 = \left[(\frac{q}{p})+(\frac{q}{p})^2+\cdots+(\frac{q}{p})^{i-1}\right] P_1 \\
P_i&= \left[(\frac{q}{p})+(\frac{q}{p})^2+\cdots+(\frac{q}{p})^{i-1}\right] P_1 +P_1\\
&= \left[1+(\frac{q}{p})^1+(\frac{q}{p})^2+\cdots+(\frac{q}{p})^{i-1}\right] P_1\\
&(\text{by formula of sum for geometric seq})\\
&= \begin{cases}\left[1 \cdot \frac{1-(q/p)^{i}}{1-(q/p)}  \right] P_1, &\text{if} \ \frac{q}{p}\neq 1, q\neq p \neq \frac{1}{2} \\
iP_1, &\text{if} \ \frac{q}{p}= 1,q= p = \frac{1}{2}
\end{cases}
\end{aligned}
$
- Using the fact that $P_N = 1$, we obtain

$$
\begin{aligned}
P_N =1= \begin{cases}\left[ \frac{1-(q/p)^{N}}{1-(q/p)}  \right] P_1, &\text{if} \ p \neq \frac{1}{2} \\
NP_1, &\text{if} \ p = \frac{1}{2}
\end{cases}
\end{aligned}
$$
- Then,

$$
\begin{aligned}
P_1 = \begin{cases}\left[ \frac{1-(q/p)}{1-(q/p)^N}  \right] , &\text{if} \ p \neq \frac{1}{2} \\
\frac{1}{N}, &\text{if} \ p = \frac{1}{2}
\end{cases}
\end{aligned}
$$

- Hence,

$$
\begin{aligned}
P_i = \begin{cases}\left[ \frac{1-(q/p)^i}{1-(q/p)^N}  \right] , &\text{if} \ p \neq \frac{1}{2} \\
\frac{i}{N}, &\text{if} \ p = \frac{1}{2}
\end{cases}
\end{aligned}
$$

- As $N \rightarrow \infty$, 

$$
\begin{aligned}
(\frac{q}{p})^N &\rightarrow 
\begin{cases} 0 , &\text{if} \ p > q \ (p > \frac{1}{2}) \\
\infty, &\text{if} \ p  < q \ (p < \frac{1}{2})
\end{cases}\\


P_i &\rightarrow
\begin{cases} 1-(\frac{q}{p})^i , &\text{if} \ p > \frac{1}{2} \\
0, &\text{if} \ p \leq \frac{1}{2}

\end{cases}
\end{aligned}
$$
- Thus, if $p>\frac{1}{2}$, there is a **positive probability** that *the gambler’s fortune will reach N*;
  - while $p \leq \frac{1}{2}$, the gambler will, with **0 probability, reach N before going broke**.


#### Example

> What is the probability that, *starting with $5$ dollars* and *p=0.45*, the Gambler's  fortune will **attain $10$ dollars before reaching 0**?

**Solution:**
- Let $i = 5, N = 10$ and $p = 0.45$, since

$$
\begin{aligned}
P_i = \begin{cases} \frac{1-(q/p)^i}{1-(q/p)^N}  , &\text{if} \ p \neq \frac{1}{2} \\
\frac{i}{N}, &\text{if} \ p = \frac{1}{2}
\end{cases}
\end{aligned}
$$

- Then, the probability that, starting with 5 dollars, the gambler's fortune will reaching 10 before reaching 0 is:


$$
\begin{aligned}
P_5 &= \frac{1-(0.55/0.45)^5}{1-(0.55/0.45)^{10}} \\
&= 0.2683
\end{aligned}
$$


#### Experiment in R
```R
# The Gambler will stop if he attains N or 0
N <- 10
# The probability of 1 dollar win at each round
p <- 0.45
# The number of rounds of the game
nround <- 80
# Vector x stores the values of the Markov Chain
x <- rep(0,nround)
# The Gambler starts with $5
x[1] <- 5

# Each pass through the loop represents 
# one step of the Markov chain.
for (i in 2:nround){
    # First check to see whether the chain is already 
    # at one of the endpoints, 0 or N
    if (x[i-1]==0 || x[i-1]==N){
        # set its new value equal to its previous value
        # since the chain is not allowed to escape 0 or N
        x[i] <- x[i-1]
    }
    else{
        # Use the sample command to move 
        # to the right 1 unit or to the left 1 unit,
        # with probabilities p and 1-p, respectively.
        x[i] <- x[i-1] + sample(c(1,-1), 1, prob=c(p,1-p))
    }
}
# The path taken by the Markov chain during simulation
plot(x,type='l',ylim=c(0,N))
```

![A path that starts at $5 and bounces up and down before being absorbed into state 0 or state N.](https://files.mdnice.com/user/1474/665e954b-41d7-4367-8275-55441ec72308.png)

### 3. Application: Drug Testing

#### 3.1. Intro to Problem
One **application of the gambler’s ruin problem** is **Drug Testing**, 
- suppose that **two new drugs** have been developed for treating a certain disease
- Drug $i$ has a *cure rate* $$P_i, i = 1, 2$$ in the sense that *each patient treated with drug $i$ will be cured with probability $P_i$* .
- These *cure rates*, however, are *NOT known*, and suppose we are interested in a method for *deciding whether*
$$P_1 > P_2 \ \text{ or } \ P_2 > P_1$$
#### 3.2. Steps of Testing
To decide upon one of these alternatives, consider the following test:
- **Pairs of patients are treated sequentially**
  - with one member of the pair receiving drug 1 and the other drug 2
- The *results for each pair are determined*, and the *testing stops* when 
  - the cumulative number of cures using one of the drugs **exceeds** the cumulative number of cures when using the other
    - *by some fixed predetermined number*.
- More formally, let

$
X_j = 
\begin{cases}
1, \text{if the patient in the pair j using drug 1 is cured}\\
0, \text{otherwise}
\end{cases}
$

$
Y_j = 
\begin{cases}
1, \text{if the patient in the pair j using drug 2 is cured}\\
0, \text{otherwise}
\end{cases}
$

- for a **predetermined positive integer M** the test *stops after pair N* where *N is the first value of n* such that either
  $$ (X_1 + \cdots + X_n) - (Y_1 + \cdots + Y_n) = M$$
  or
  $$(X_1 + \cdots + X_n) - (Y_1 + \cdots + Y_n) = -M$$
- In the **former case** we then assert that $P_1 > P_2$ , 
  - and in the **latter** that $P_2 > P_1$

#### 3.3. Probability of Incorrect Decision
In order to help ascertain **whether the preceding is a GOOD Test**, 
- one thing we would like to know is **the probability** of it leading to an *incorrect decision*.
- That is, for given $P_1$ and $P_2$ where $$\color{blue}P_1 > P_2,$$ what is the **probability** that the *test will Incorrectly assert that $P_2 > P_1$*?

To determine this probability, note that *after each pair is checked* the **cumulative difference of cures** using *drug 1 versus drug 2* will either 
- *go up by 1* with probability $$P_1(1-P_2)$$ since this is the probability that *drug 1 leads to a cure* and *drug 2 does not*, or
- *go down by 1* with probability $$(1 − P_1 )P_2$$
- or **remain the same** with probability $$P_1P_2+(1-P_1)(1-P_2)$$ since this is the probability that *both drugs lead to a cure* or *both drugs do not*

Hence, if we ONLY consider *those pairs in which the Cumulative Difference changes*, 
- then **the difference will go up 1** with probability
  $$
  \begin{aligned}
  p &= P(\text{ up 1 }| \text{ up 1 or down 1}) \\
    &= \frac{P_1(1-P_2)}{P_1(1-P_2)+(1-P_1)P_2}
  \end{aligned}
  $$ 
  and **down 1** with probability
  $$
  \begin{aligned}
  q &= 1-p \\
    &= \frac{P_2(1-P_1)}{P_1(1-P_2)+(1-P_1)P_2}
  \end{aligned}
  $$ 
- The **probability** that *the test will assert that $P_2 > P_1$* is
  - **equal to the probability** that 
    - *a Gambler who wins each (one unit) bet* with **probability p will go down M before going up M**.
    $$
    \begin{aligned}
    P_i = \begin{cases}\left[ \frac{1-(q/p)^i}{1-(q/p)^N}  \right] , &\text{if} \ p \neq \frac{1}{2} \\
    \frac{i}{N}, &\text{if} \ p = \frac{1}{2}
    \end{cases}
    \end{aligned}
    $$
      with $i=M, N = 2M$
- So

$
\begin{aligned}
P(\text{test asserts that } P_2 > P_1) &= 1 - \frac{1-(q/p)^M}{1-(q/p)^{2M}} \\
&= \frac{1}{1+(p/q)^M}
\end{aligned}
$

- Thus, for instance, if $P_1 = 0.6$ and $P_2 = 0.4$, then the **probability of an incorrect decision** is *0.017 when M = 5* and *reduces to 0.0003 when M = 10*.

#### Resources:
[1] Sheldon M. Ross, Introduction to Probability Models, Academic Press; 12th edition (2019)

[2] Joseph K. Blitzstein, Jessica Hwang, Introduction to Probability, Chapman and Hall/CRC, 2nd Edition (2019)
