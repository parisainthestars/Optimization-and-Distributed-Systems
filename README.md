# Optimization and Distributed Systems (DOL) - Homework 1

This repository contains the report and Python implementations for the first homework of the **Optimization and Distributed Systems** course.

## 📚 Assignment Overview

### Part 1: Theoretical Foundations (Q1–Q6)
Mathematical derivations and proofs covering:
* **Curvature Analysis:** Determining convexity/concavity of various functions.
* **Duality Theory:** Deriving the dual problem for $l_1$-norm projection and analyzing Slater's condition.
* **KKT Conditions:** Solving for global minima in non-convex quadratic problems using KKT stationarity and feasibility.
* **Line Search:** Analytical derivation of exact step sizes for descent directions.

### Part 2: Simulations & Algorithms (Q7–Q8)
Python implementations comparing optimization algorithms:

* **Projected Subgradient Method:**
    * Minimized a piece-wise linear function.
    * Analyzed convergence behavior under four different step-size rules (Constant vs. Diminishing).

* **Newton's Method vs. Steepest Descent:**
    * Implemented **Steepest Descent**, **Newton's Method**, and a **Combined Method** with backtracking line search.
    * Tested on three distinct functions (Strongly Convex, Non-Convex/Unstable, and Rosenbrock) to demonstrate convergence rates and stability.

---

### 🛠 Tools
* **Language:** Python
* **Libraries:** `cvxpy` (for ground truth verification), `numpy`, `matplotlib`.
