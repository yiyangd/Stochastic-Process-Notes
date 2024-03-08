## Stochastic Process 05. Long-Run Proportions and Mean Time in Transient States

### 1. Long-Run Proportions
The concepts of **recurrence and transience** are important for understanding the **long-run behavior of a Markov chain**.
- At first, the chain may *spend time* in *transient states*. 
- Eventually though, the chain will *spend ALL its time* in *recurrent states*. 
- But what *fraction of the time will it spend* in each of the recurrent states?
  - This question is answered by the **stationary distribution** of the chain, 
    - also known as the **steady-state distribution**.
- The **stationary distribution** describes the **long-run behavior** of the chain, *regardless of its initial conditions*
  - It will tell us both the **long-run probability** of being in any particular state, 
  - and the **long-run proportion of time** that the chain spends in that state.
  
#### Definition of Positive Recurrent and Null Recurrent

### 2. Initial and Stationary Distribution
#### 2.1.Definition 
A **row probability vector $\vec{\alpha}$** such that *$\alpha_i \geq 0$ for ALL $i$* and *$\sum_{i=0}^\infty\alpha_i = 1$* is called an **Initial Distribution** if
$$P(X_0=i)=\alpha_i$$


An **Initial Distribution** is called **Stationary Distribution** if the Markov Chain with *Transition Matrix $P$* such that
$$\vec{\alpha} P = \vec{\alpha}$$
$$P(X_1=1)=P(X_0=i)=\alpha_i \ \text{for all i}$$

- if **$\vec{\alpha}$** is **the distribution of $X_0$** , then **$\vec{\alpha}P$** is the **marginal distribution of $X_1$** . 
- Thus the equation $\vec{\alpha} P = \vec{\alpha}$ means that if $X_0$ has distribution $\vec{\alpha}$, then $X_1$ also has distribution $\vec{\alpha}$. 
  - But then $X_2$ also has distribution $\vec{\alpha}$, as does $X_3$ , etc. 
- That is, a Markov chain whose **initial distribution is the stationary distribution $\vec{\alpha}$**  will *stay in the stationary distribution forever*.


#### Example: A Communications System
Consider a communications system that **transmits the digits 0 and 1**.
- Each digit transmitted must pass through several stages,
  - at each of which there is a **probability p** that the **digit entered will be unchanged when it leaves**.
> a) Find a **stationary initial distribution**.

**Solution:**
- Letting $X_n$ denote the digit entering the $n^{th}$ stage, then $\{X_n , n = 0, 1, . . .\}$ is a two-state Markov chain having a transition probability matrix
$$ P = 
\begin{pmatrix}
p & 1-p  \\
1-p & p 
\end{pmatrix}
$$

- The Stationary Distribution is of the form $$\vec{\alpha} = (\alpha, 1-\alpha)$$  and we need solve for $\alpha$ in $$\vec{\alpha}P = \vec{\alpha}$$  $(\alpha, 1-\alpha) \begin{pmatrix} p & 1-p  \\ 1-p & p  \end{pmatrix} = (\alpha, 1-\alpha)$  $$$$ which is equivalent to

$$
\begin{aligned}
\alpha p + (1-\alpha)(1-p) &= \alpha \\
\alpha(1-p) + (1-\alpha)p &= 1-\alpha
\end{aligned}
$$
- The ONLY Solution to these equations is $$\alpha = \frac{1}{2}$$ so the **Unique Statinary Initial Distribution** of this Markov Chain is
$$\vec{\alpha} = (\frac{1}{2}, \frac{1}{2})$$
- which are **long-run proportions of digit 0 and digit 1**


#### Example: Weather depending on last 2 days

#### 2.2. Hitting TImes


#### 2.3. Infinite State Spaces



### 3. Mean Time Spent in Transient States

#### 3.1. Definition of Transition Matrix for Transient States

Consider a Finite State Markov Chain with **Transition Probabilities $\textbf{P}_\textbf{T}$** between its *$t$ Transient States*, let 

$$ 
\textbf{P}_\textbf{T} =
\begin{pmatrix}
P_{11} & P_{12} & \cdots & P_{1t}\\
\vdots & \vdots & \vdots & \vdots\\
P_{t1} & P_{t2} & \cdots & P_{tt}
\end{pmatrix}
$$

- Note that **$\textbf{P}_\textbf{T}$ is NOT a Stochastic Matrix** since the *recurrent states are removed*
  - **$\textbf{P}_\textbf{T}$ specifies ONLY the transition probabilities from transient states into transient states**, some of its row sums are less than 1
  
#### Example

Let **$s_{ij}$ be the expected number of visits** to *state $j$* given the chain *starts in state $i$*, where $i$ and $j$ are *transient states*.
- Conditioning on the first transition:
  $$s_{ij} = 1(\text{if } i=j, 0 \ \text{ otherwise}) + \sum^t_{k=1} P_{ik}s_{kj}$$
  Only need to consider *$k$ is transient*
  - since it is impossible to go from a recurrent to a transient state, implying that **$s_{kj} = 0$ when k is a recurrent state**.

Let $\textbf{S}$ be the matrix of values *$\textbf{s}_\textbf{ij} \, \ i, j = 1, 2 ..., t$*, then the equation above can be written in matrix form

$$ 
\begin{aligned}
\textbf{S} &=
\begin{pmatrix}
s_{11} & s_{12} & \cdots & s_{1t}\\
\vdots & \vdots & \vdots & \vdots\\
s_{t1} & s_{t2} & \cdots & s_{tt}
\end{pmatrix}\\
\\
&=\textbf{I} + \textbf{P}_\textbf{T} \textbf{S}
\end{aligned}
$$
- where $\textbf{I}$ is **the identity matrix of size t**, then

$$ 
\begin{aligned}
\text{I} \ &\textbf{S} 
=\textbf{I} + \textbf{P}_\textbf{T} \textbf{S}\\

(\text{I} - \textbf{P}_\textbf{T}) &\textbf{S} = \text{I} \\
(\text{Multiply } & \text{ Both Sides by }  \ (\text{I} - \textbf{P}_\textbf{T})^{-1})\\
&\textbf{S} = (\text{I} - \textbf{P}_\textbf{T})^{-1}
\end{aligned}
$$
- That is, the quantities $s_{ij} , i ∈ T , j ∈ T$ , can be obtained by **inverting the identity matrix $\textbf{I}$ minus $\textbf{P}_\textbf{T}$**
#### Example
> Consider the gambler’s ruin problem with *p = 0.4 and N = 7*. Starting with *3 dollars*, determine
> - the **expected amount of time** the gambler has *2 dollars*,
> - the **expected amount of time** the gambler has *5 dollars*.

**Solution:**
- The matrix $\textbf{P}_\textbf{T}$ , which specifies $P_{ij}$ , $i, j \in \{1, 2, 3, 4, 5, 6\}$, is as follows:
$$
\textbf{P}_\textbf{T}=
\begin{pmatrix}
0 & 0.4 & 0 & 0 & 0 & 0 \\
0.6 & 0 & 0.4 & 0 & 0 & 0 \\
0 & 0.6 & 0 & 0.4 & 0 & 0 \\
0 & 0 & 0.6 & 0 & 0.4 & 0 \\
0 & 0 & 0 & 0.6 & 0 & 0.4 \\
0 & 0 & 0 & 0 & 0.6 & 0
\end{pmatrix}
$$

- Inverting $\textbf{I}-\textbf{P}_\textbf{T}$ gives

$$
\begin{aligned}
\textbf{S} &= (\textbf{I}-\textbf{P}_\textbf{T})^{-1}\\
&=
\begin{pmatrix}
1.61 & 1.02 & 0.63 & 0.37 & 0.19 & 0.08 \\
1.54 & 2.56 & 1.58 & 0.92 & 0.49 & 0.19 \\
1.42 & \color{red}2.37 & 3.00 & 1.75 & \color{red}0.92 & 0.37 \\
1.25 & 2.08 & 2.63 & 3.00 & 1.58 & 0.63 \\
0.98 & 1.64 & 2.08 & 2.37 & 2.56 & 1.02 \\
0.59 & 0.98 & 1.25 & 1.42 & 1.54 & 1.61
\end{pmatrix}
\end{aligned}
$$

- Hence, the **expected amount of time** the gambler has *2 dollars* and *5 dollars* are
$$\color{red}s_{32} = 2.37, s_{35}=0.92$$


#### 2.4. Probability between two states



#### Example
> Consider the gambler’s ruin problem with *p = 0.4 and N = 7*. Starting with *3 dollars*, determine
> - the **probability** that the gambler ever *has  1 dollar*.

**Solution:**
- Since 
$$
\textbf{S}
=
\begin{pmatrix}
\color{red}1.61 & 1.02 & 0.63 & 0.37 & 0.19 & 0.08 \\
1.54 & 2.56 & 1.58 & 0.92 & 0.49 & 0.19 \\
\color{red}1.42 & 2.37 & 3.00 & 1.75 & 0.92 & 0.37 \\
1.25 & 2.08 & 2.63 & 3.00 & 1.58 & 0.63 \\
0.98 & 1.64 & 2.08 & 2.37 & 2.56 & 1.02 \\
0.59 & 0.98 & 1.25 & 1.42 & 1.54 & 1.61
\end{pmatrix}
$$
- Then

$$f_{31}=\frac{s_{31}}{s_{11}}=\frac{\color{red}1.42}{\color{red}1.61} \approx 0.88$$

- As a check, note that $f_{31}$ is just 
