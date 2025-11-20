# Optimization and Distributed Systems (DOL) - Homework 1


This repository contains the detailed report, mathematical derivations, and Python implementations for the first homework assignment of the **Optimization and Distributed Systems** course. The assignment covers fundamental concepts of convex analysis, duality theory, KKT conditions, and the implementation of various optimization algorithms.

## 📚 Assignment Overview

The homework is divided into **Theoretical Problems** (Q1–Q6) and **Simulation/Coding Tasks** (Q7–Q8).

### 🧠 Part 1: Theoretical Foundations

#### Q1: Curvature Analysis
Analyzed the curvature (convex, concave, affine, or none) of various mathematical functions, determining their Hessian properties and domains [cite: 567-607].
* **Key Functions Analyzed:**
    * $f(x) = \min\{2, x, \sqrt{x}\}$ (Concave)
    * $f(x_1, x_2) = x_1/x_2$ (Indefinite Hessian)
    * Geometric mean compositions and Cobb-Douglas-like functions ($x_1^\alpha x_2^{1-\alpha}$).

#### Q2: Projection onto the $l_1$-Norm Unit Ball
Derived the **Dual Problem** for projecting a point $a \in \mathbb{R}^n$ onto the unit ball $||x||_1 \leq 1$.
* **Method:** Derived the Lagrangian and Dual Function $g(\lambda)$.
* **Dual Solution:** The optimal primal variable $x^*$ is related to the dual variable via the **Soft-Thresholding Operator**: $S_\lambda(a_i) = \text{sign}(a_i)\max(0, |a_i| - \lambda)$.
* **Algorithm:** Proposed an efficient **Bisection Search** to find the root of the monotonic dual gradient function to solve for $\lambda^*$.

#### Q3: Duality Gap & Slater's Condition
Investigated a specific convex problem where **Strong Duality fails**.
* **Problem:** Minimize $e^{-x}$ subject to $x^2/y \leq 0$ on domain $y>0$.
* **Findings:**
    * Primal Optimal ($p^*$): 1
    * Dual Optimal ($d^*$): 0
    * **Duality Gap:** 1 (Non-zero).
    * **Reason:** Slater's condition does not hold because the strictly feasible set is empty.

#### Q4: Convex Optimization Properties
Evaluated statements regarding KKT conditions, uniqueness of solutions, and boundedness in convex problems satisfying Slater's constraint qualification [cite: 723-754].

#### Q5: Nonconvex Quadratic Optimization
Analyzed a nonconvex problem with a quadratic objective and quadratic equality constraint.
* **Task:** Derived KKT conditions and found all solution pairs $(x, \nu)$.
* **Global Minimum:** Identified the specific Lagrange multiplier range ($\nu > 3$) that satisfies the second-order sufficient condition for optimality.

#### Q6: Exact Line Search
Performed an analytical line search for the function $f(x) = (x_1 + x_2^2)^2$.
* Verified descent direction conditions.
* Solved the 1D minimization problem $\min_{\alpha > 0} f(x + \alpha p)$ analytically to find the exact step size $\alpha = 0.5$.

---

### 💻 Part 2: Simulations & Algorithms

This section involves the Python implementation of optimization algorithms to solve specific problems.

#### Q7: Projected Subgradient Method
**Objective:** Minimize a piece-wise linear function $f(x) = \max_i (a_i^T x + b_i)$ subject to linear constraints. The ground truth optimal value $f^*$ was calculated using `cvxpy`.

**Experiments:**
Run the projected subgradient method for 50,000 iterations using four different step-size rules:
1.  **Constant Step-Size**
2.  **Constant Step-Length**
3.  **Non-Summable Diminishing:** $\alpha_k = 0.1/\sqrt{k}$
4.  **Square Summable:** $\alpha_k = 1/k$

**Results & Convergence:**
* Constant step rules failed to converge to $f^*$, oscillating with a large optimality gap (~0.16).
* Diminishing step rules (Square Summable and Non-Summable) successfully converged towards the optimum with significantly smaller gaps (~0.06) [cite: 913-915].
* **Conclusion:** The subgradient method is robust but has a slow convergence rate of $O(1/\sqrt{k})$.

#### Q8: Gradient Descent vs. Newton's Method
**Objective:** Minimize three distinct functions using **Steepest Descent**, **Newton's Method**, and a **Combined Method** (with backtracking line search).

**Test Functions:**
1.  **$f_1$ (Strongly Convex):** $e^{x-3} - \frac{\pi}{2}x - 2$
    * *Result:* Newton's method achieved quadratic convergence (vertical drop in error) in 5-6 iterations. Steepest descent showed linear (slow) convergence [cite: 948-951].
2.  **$f_2$ (Non-Convex/Unstable):** $-(1 + 2^{-x})\cos(x)\sin(x)$
    * *Result:* Algorithms diverged or failed due to the highly non-convex nature ("wavy" landscape) and numerical instability caused by the $2^{-x}$ term [cite: 955-962].
3.  **$f_3$ (Rosenbrock/Valley):** $100(x_2 - x_1^2)^2 + (1-x_1)^2$
    * *Result:* Steepest descent got stuck zig-zagging on the valley walls (slow convergence). Newton's method utilized curvature information to jump directly to the minimum in ~15 iterations [cite: 966-970].

---

### 🛠 Tools & Technologies
* **Language:** Python
* **Optimization Solver:** CVXPY (for ground truth calculation in Q7)
* **Libraries:** NumPy (linear algebra), Matplotlib (visualization)
