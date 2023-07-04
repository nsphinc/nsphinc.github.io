---
layout: page
title: B8-3
---

**Lectures** [1](#lecture-1-option-pricing-binomial-model) | [2](#lecture-2-itos-lemma-and-applications) | [3]() | [4]() | [5]() | [6]() | [7]() | [8]() | [9]() | [10]() | [11]() | [12]() | [13]() | [14]() | [15]() | [16]()  

# *Lecture 1,* Option pricing: binomial model

* Arbitrage pricing
* Binomial trees
* Risk-neutral valuation

## Options

* European call/put option
    * Right to purchase/sell the underlying at pre-specified time at expiration date for strike price
* American call/put option
    * Right to purchase/sell the underlying at any time up until expiration date for strike price
* Terminology
    * Underlying (stock, say) price S
    * Expiration date T
    * Strike price K
    * Risk-free rate r
        * Gross risk free rate $R = 1+r$
* Look for *replicating payoff*, say, of $A_3$ using $A_1$ and $A_2$

## Binomial model
* Two possible states, say the up and down states

* Pricing a call in a binomial model
    * $C_u^E=\max{(uS-K,0)}$ payoff in up state (probability p, S worth uS)
    * $C_d^E=\max{(dS-K,0)}$ payoff in down state (probabilty $q=1-p$, S worth dS)

* Set up portfolio with B cash in bond and $\Delta$ amount of stock to replicate payoff
     * $\Pi(0)=B+\Delta S$
     * Choose $\Delta$ such that
        * $\Delta uS+ RB=C_u^E$
        * $\Delta dS+ RB=C_d^E$
    * **Therefore solve for $\Delta$ and B in matrix form**

* **Given** solution, this (replicating) portfolio, by **no arbitrage**, is the same value as that of the call $C^E(S,t=0;K,1)$ (European option so superscript E)
    * **No arbitrage**: the price of the derivative is set at the same level as the value of the replicating portfolio, so that no trader can make a risk-free profit by buying one and selling the other
    * Value of the call (price of the call as an expectation) can thus be seen as the *discounted (/R) weighted average of the **portfolio** payoff at expiry*
    * In other words, $C^E(S,t=0;K,1)=\frac{1}{R}[p^*C_u^E+q^*C_d^E]$
        * Basically $C^E$ is the *price you set*

* $C^E(S,t=0;K,1)$ can be also thought of as the *intrinsic value* of the call, which would be the value, or benefit, obtained by the holder by exercising the option *immediately*
    * Total value = intrinsic value + time premium (https://www.scranton.edu/faculty/hussain/teaching/fin471_/DSEC03.pdf) 
    * Therefore, with zero strike price, it can be seen that:

* Note $C^E(S,t=0;K=0,1)=S=\frac{1}{R}[p^*C_u^E+q^*C_d^E]=\frac{1}{R}[p^*uS+(1-p^*)dS]=\frac{1}{R}\mathbb{E}^*[S_1]$
    * So, under no arbitrage, $RS=\mathbb{E}^*[S_1]$

* **Proposition:** American call written on S (underlying that pays no dividends) is never exercised early 
    * $C^A(S,t;K,T)\geq S-Ke^{-r(T-t)}$    
    * Think NPV lost on *not* delaying K consumption
        * https://www.math.ucla.edu/~caflisch/181.1.07w/Lect18.pdf

* **Proposition:** Put-call-parity for European options
    * $C^E(S,t;K,T)-P^E(S,t;K,T)=S-Ke^{-r(T-t)}$

# *Lecture 2,* Ito's Lemma and applications

* Brownian Motion, Wiener Process
* Stochastic Integrals
* Itô's Lemma
* Modelling returns

## Brownian Motion, Wiener Process

* **Definition:** stochastic process W is a Wiener process (or Brownian motion) iff
    1\. $W_0$=0
    2\. W has independent increments (where $r<s\leq t<u$, then $W_u-W_t$ and $W_s-W_r$ are independent stochastic variables)
    3\. For $s<t$ the distribution of the stochastic variable $W_t-W_s$ is $N(0,t-s)$
    4\. W has *continuous trajectories*
    * We work with these now.

* Some properties of the Wiener process
    * $\mathbb{E}[\Delta W]=0$
    * $\mathbb{E}[(\Delta W)^2]=\Delta t$
    * $Var[\Delta W]= \Delta t$
    * $Var[(\Delta W)^2]=2(\Delta t)^2$

* Random walk $$X_{t+\Delta t}-X_t=\mu (t,X)\Delta t+\sigma (t,X)\Delta W_t$$ where $\Delta W_t=W_{t+\Delta t}-W_t$
    * Taking $\Delta t$ to the limit, $dX_t=\mu (t,X)dt+\sigma (t,X)dW_t$
    * And with initial condition $X(0)=a$, $$X_t=a+\int^t_0{\mu (s,X)ds}+\int^t_0{\sigma (s,X)dW_s}$$

## Stochastic Integrals

* To guarantee existence of stochastic integral $\int^t_0{g(s)dW_s}$, impose integrability conditions on g $\rightarrow$ and the class of $\mathcal{L}^2$ turns out to be natural
    * g belongs to class $\mathcal{L}^2[0,t]$  for all $t>0$

## *Itô's Isometry*

$$\mathbb{E}[\int^b_a{g(s)dW_s}]=0$$ and $$\mathbb{E}[(\int^b_a{g(s)dW_s})^2]=\int^b_a{\mathbb{E}[g^2(s)]ds}$$ such that one can say that as $\Delta t \rightarrow 0$ we must have $$(dW_t)^2=dt$$

* Work some mathematical magic
* Where process S satisfies the stochastic DE: $$dS_t=\mu (S,t)dt+\sigma (S,t)dW_t$$  
    * Where $\mu (S,t),\sigma (S,t)$ are adapted processes, and let $f$ be a *twice continuous differentiable function*, then: $$df(S,t)=(\frac{\partial f}{\partial t}+\mu(S,t)\frac{\partial f}{\partial S}+\frac12\sigma^2(S,t)\frac{\partial^2f}{\partial^2t})dt+\sigma(S,t)\frac{\partial f}{\partial S}dW_t$$
* Model returns using stochastic DE $$\frac{dS_t}{S_t}=\mu (S,t)dt+\sigma (S,t)dW_t$$
    * Using Itô's lemma tells us that $S_t=S_0e^{(\mu-\frac12\sigma^2)t+\sigma W_t}$, assuming $\mu(S,t)=\mu S$ and $\sigma(S,t)=\sigma S$

$$???$$

## Black-Scholes PDE

* Problem: 
    * Assume $\frac{dS_t}{S_t}=\mu (S,t)dt+\sigma (S,t)dW_t$
    * Price a European-style option, $V(S,t;K,T)$ written on S with payoff $V(S,T;K,T)=V(S,T)$
* Approach:
    * Form a hedge portfolio long a call and 'delta' amount of the underlying
    * See what is the change in the value of the portoflio over a small time step
    * Try to choose the amount of the underlying in the portfolio so that risk or randomness is reduced

* The hedge portfolio $$\Pi(S,t)=V(S,t;K,T)-\Delta S_t$$ where $\Delta$ is the *number of shares we choose to hold* in the portfolio 
    * Change in value of portfolio $d\Pi=dV-\Delta dS$
    * Using Itô's lemma, $$d\Pi=(\frac{\partial V}{\partial t}+\mu S\frac{\partial V}{\partial S}+\frac12\sigma^2S^2\frac{\partial^2V}{\partial S^2}-\Delta \mu S)dt+(\frac{\partial V}{\partial S}-\Delta)S\sigma dW_t$$
    * Choose at every instant in time, the following amount of stock $\Delta = \frac{\partial V}{\partial S}$ so the change in portfolio is deterministic
    * Therefore obtain $$d\Pi=(\frac{\partial V}{\partial t}+\frac12\sigma^2S_t^2\frac{\partial^2V}{\partial S^2})dt$$
    * Separately note that portfolio grows like a risk-free bond, $d\Pi=r\Pi dt$
* Therefore, $$rV=\frac{\partial V}{\partial t}+rS\frac{\partial V}{\partial S}+\frac12\sigma^2S^2\frac{\partial^2V}{\partial S^2}$$ and this is the Black-Scholes PDE (will need BCs to solve for a particular European-style option)

# Heat Equation

