## Dirichlet Process

* Distribution over distributions
* Parameterized by: $\alpha,\ G$
* **Concentration parameter** $\alpha$ shows how the $G^{\prime}$ is similar to the **base distribution** $G$. The larger the $\alpha$ is, more similar it will be.
* Can then draw observations from $x\sim DP(\alpha,\ G)$ or $x\sim\ G^\prime.$



## Defining a DP

* like breaking off sticks
  $$
  V_1,V_2,...\sim_{iid}\ Beta(1,\alpha)\\
  and\ C_k :=V_k\prod_{j=1}^{k-1}(1-V_j)
  $$
  Varibles $V_i$ are [0, 1]

  Stick breaking weights $C_k$ 

* Draw atoms
  $$
  \Phi_1,\Phi_2,...\sim_{iid} G
  $$

* Merge into complete distribution
  $$
  \Theta=\sum_{k\in N}C_k\delta_{\Phi_k}
  $$
  

## Properties of a DPMM

* Expected value is the same as base distribution
  $$
  E_{DP(\alpha,\ G)}[x]=E_{G}[x]
  $$

* As $\alpha\rightarrow \infty$, $DP(\alpha, G)=G$.

* Number of components unbounded

* Impossible to represent fully on computer (truncation)

* You can nest DPs
  $$
  H\sim DP(\alpha,\ G)\\
  J\sim DP(\alpha,\ H)
  $$
  

