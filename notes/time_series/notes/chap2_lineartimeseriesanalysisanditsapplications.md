# Chapter 2 : Linear Time Series and its Applications

# Key Formulas

Variance
Var(aX + )

Covariance

### AR(p) Process

#### Solving for AR(p)
1. Analytical Solution
   1. AR(1) process
      - Let $X_t = \phi X_{t-1} + \varepsilon_t$, where $|\phi| < 1$ for stationarity.
      - The ACF for AR(1) is:
         $$\rho_k = \phi^k, \quad \text{for } k \geq 0$$
         - Where $\rho_k$ is the autocorrelation at lag $k$.

   2. AR(2) process
      - Let $X_t = \phi_1 X_{t-1} + \phi_2 X_{t-2} + \varepsilon_t$
      - The ACF for AR(2) is:
         $$\rho_1 = \frac{\phi_1}{1 - \phi_2}$$
         $$\rho_2 = \phi_1\rho_1 + \phi_2$$
      - For $k > 2$:
         $$\rho_k = \phi_1\rho_{k-1} + \phi_2\rho_{k-2}$$
   3. Higher-order AR(p) process
      - For $X_t = \phi_1 X_{t-1} + \phi_2 X_{t-2} + \cdots + \phi_p X_{t-p} + \varepsilon_t$
      - The ACF is given by the Yule-Walker equations:
            $$\rho_k = \phi_1\rho_{k-1} + \phi_2\rho_{k-2} + \cdots + \phi_p\rho_{k-p}, \quad \text{for } k > 0$$
      - With initial conditions:
         $$\rho_0 = 1$$
         $$\rho_{-k} = \rho_k \quad \text{(due to symmetry)}$$

      - For $k \leq p$, we have $p$ equations with $p$ unknowns, which can be solved to get the first $p$ autocorrelations. For $k > p$, we can use the general equation recursively.

      To solve these equations analytically:
        1. For AR(1), it's straightforward.
        2. For AR(2), you can solve the system of equations for $\rho_1$ and $\rho_2$, then use recursion.
        3. For higher orders, you typically need to:
            1.  Set up the system of Yule-Walker equations
            2.  Solve them using matrix algebra
            3.  Use the results to generate the rest of the ACF recursively

# Proofs

1. Proving -1 <= $\rho(k)$ <= 1 is the autocorrelation of a weakly stationary process. Let $X(t)$ be a weakly stationary process.
   1.  <b>Proof 1: Using Properties of Variance</b>
          1. Define autocorrelation:
             $\rho(\tau) = \text{Corr}(X(t), X(t+\tau)) = \frac{\text{Cov}(X(t), X(t+\tau))}{\sqrt{\text{Var}(X(t)) \cdot \text{Var}(X(t+\tau))}}$

          2. For a weakly stationary process:
             - $E[X(t)] = \mu$ for all $t$
             - $\text{Var}(X(t)) = \sigma^2$ for all $t$
             - $\text{Cov}(X(t), X(t+\tau)) = \gamma(\tau)$

          3. Rewrite autocorrelation:
             $\rho(\tau) = \frac{\gamma(\tau)}{\sigma^2}$

          4. Consider $\text{Var}(X(t) - X(t+\tau))$:
             $\text{Var}(X(t) - X(t+\tau)) = E[(X(t) - X(t+\tau))^2] - (E[X(t) - X(t+\tau)])^2$

          5. Expand:
             ${Var}(X(t) - X(t+\tau)) = E[X(t)^2] + E[X(t+\tau)^2] - 2E[X(t)X(t+\tau)] - (\mu - \mu)^2 \\
                                           = \sigma^2 + \sigma^2 - 2\gamma(\tau) - 0 \\
                                           = 2\sigma^2 - 2\gamma(\tau)$

          6. Since variance is non-negative:
             $2\sigma^2 - 2\gamma(\tau) \geq 0$

          7. Rearrange:
             $\gamma(\tau) \leq \sigma^2$

          8.  Similarly, consider $\text{Var}(X(t) + X(t+\tau))$:
             ${Var}(X(t) + X(t+\tau)) = E[(X(t) + X(t+\tau))^2] - (E[X(t) + X(t+\tau)])^2 \\
                                           = \sigma^2 + \sigma^2 + 2\gamma(\tau) - (2\mu)^2 \\
                                           = 2\sigma^2 + 2\gamma(\tau)$
          9.  Again, since variance is non-negative:
             $2\sigma^2 + 2\gamma(\tau) \geq 0$

          10. Rearrange:
              $\gamma(\tau) \geq -\sigma^2$

          11. Combine inequalities:
              $-\sigma^2 \leq \gamma(\tau) \leq \sigma^2$

          12. Divide by $\sigma^2$ (positive as it's a variance):
              $-1 \leq \frac{\gamma(\tau)}{\sigma^2} \leq 1$

          13. Recall $\rho(\tau) = \frac{\gamma(\tau)}{\sigma^2}$, therefore:
              $-1 \leq \rho(\tau) \leq 1$

   2. <b>Proof 2: Using Cauchy-Schwarz Inequality</b>

      1. The Cauchy-Schwarz inequality states that for any two random variables $X$ and $Y$:
         $|E[XY]|^2 \leq E[X^2] \cdot E[Y^2]$

      2. Let $X = X(t) - E[X(t)]$ and $Y = X(t+\tau) - E[X(t+\tau)]$

      3. Apply Cauchy-Schwarz:
         $|\text{Cov}(X(t), X(t+\tau))|^2 \leq \text{Var}(X(t)) \cdot \text{Var}(X(t+\tau))$

      4. For a weakly stationary process, this becomes:
         $|\gamma(\tau)|^2 \leq \sigma^4$

      5. Dividing both sides by $\sigma^4$:
         $\left|\frac{\gamma(\tau)}{\sigma^2}\right|^2 \leq 1$

      6. Recall $\rho(\tau) = \frac{\gamma(\tau)}{\sigma^2}$, so:
         $|\rho(\tau)|^2 \leq 1$

      7. Taking the square root:
         $-1 \leq \rho(\tau) \leq 1$

      Both proofs demonstrate that $-1 \leq \rho(\tau) \leq 1$ for a weakly stationary process.

   3. <b>Proof 3: Proof of Autocorrelation Bounds Using $V[aX_t + bX_{t+\tau}]$</b>
      1. Consider the variance of a linear combination: $V[aX_t + bX_{t+\tau}]$

      2. By the properties of variance and covariance:
         $V[aX_t + bX_{t+\tau}] = a^2V[X_t] + b^2V[X_{t+\tau}] + 2abCov(X_t, X_{t+\tau})$

      3. For a weakly stationary process:
         - $V[X_t] = V[X_{t+\tau}] = \sigma^2$
         - $Cov(X_t, X_{t+\tau}) = \gamma(\tau)$

      4. Substituting these in:
         $V[aX_t + bX_{t+\tau}] = a^2\sigma^2 + b^2\sigma^2 + 2ab\gamma(\tau)$

      5. Since variance is always non-negative:
         $a^2\sigma^2 + b^2\sigma^2 + 2ab\gamma(\tau) \geq 0$ for all $a$ and $b$

      6. Divide by $\sigma^2$ (which is positive as it's a variance):
         $a^2 + b^2 + 2ab(\gamma(\tau)/\sigma^2) \geq 0$

      7.  Recall that $\rho(\tau) = \gamma(\tau)/\sigma^2$, so:
         $a^2 + b^2 + 2ab\rho(\tau) \geq 0$

      8.  This inequality must hold for all values of $a$ and $b$. Let's choose $a = 1$ and $b = -1$:
         $1^2 + (-1)^2 + 2(1)(-1)\rho(\tau) \geq 0$
         $2 - 2\rho(\tau) \geq 0$
         $-\rho(\tau) \geq -1$
         $\rho(\tau) \leq 1$

      9.  Now, let's choose $a = 1$ and $b = 1$:
         $1^2 + 1^2 + 2(1)(1)\rho(\tau) \geq 0$
         $2 + 2\rho(\tau) \geq 0$
         $\rho(\tau) \geq -1$

      10. Combining the results from steps 8 and 9:
         $-1 \leq \rho(\tau) \leq 1$

      Thus, we have proven that the autocorrelation of a weakly stationary process is bounded between -1 and 1.

2. <b>Independent Random Variables are Uncorrelated</b>
   Let $X$ and $Y$ be two random variables that are independent.

   1. Definition of uncorrelated random variables:
      Two random variables $X$ and $Y$ are uncorrelated if their covariance is zero:
      $Cov(X,Y) = 0$

   2. Recall the definition of covariance:
      $Cov(X,Y) = E[(X - E[X])(Y - E[Y])]$

   3. Expand this expression:
      $Cov(X,Y) = E[XY - XE[Y] - YE[X] + E[X]E[Y]]$

   4. Using the linearity of expectation:
      $Cov(X,Y) = E[XY] - E[X]E[Y] - E[Y]E[X] + E[X]E[Y]$

   5. Simplify:
      $Cov(X,Y) = E[XY] - E[X]E[Y]$

   6. Now, we use the key property of independent random variables:
      If $X$ and $Y$ are independent, then for any functions $f$ and $g$:
      $E[f(X)g(Y)] = E[f(X)]E[g(Y)]$

   7. In our case, let $f(X) = X$ and $g(Y) = Y$. Then:
      $E[XY] = E[X]E[Y]$

   8. Substituting this into our covariance expression:
      $Cov(X,Y) = E[XY] - E[X]E[Y] = E[X]E[Y] - E[X]E[Y] = 0$

   9. Therefore:
      $Cov(X,Y) = 0$

   Thus, we have proven that if $X$ and $Y$ are independent random variables, then $Cov(X,Y) = 0$, which means they are uncorrelated.