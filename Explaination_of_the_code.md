# SLES Characterization Tool - Code Explanation

## 1. Core Purpose
This script numerically tests whether a specific candidate point ($\bar{x}$) is a **Strict Local Efficient Solution (SLES)** for a Multiobjective Programming Problem (MOP). Instead of using complex analytical calculus, it uses Monte Carlo (randomized) sampling to verify the mathematical conditions outlined by Gupta, Mehra & Bhatia (2011).

---

## 2. Workflow & Execution Steps

### Step 0: Input Parsing & Setup
*   The script uses the `sympy` library to parse user-defined mathematical functions (objectives $f_i$ and constraints $g_j$) from string inputs.
*   It converts these into fast, executable `numpy` functions.

### Step 1: Penalty Calculation & Sampling
*   It defines a penalty function: 
    $$pen_i(x) = f_i(x) - \alpha_i \|x - \bar{x}\|^m$$
*   It generates $N$ random points inside a defined radius ($\delta$) around a test point ($x'$). 
*   It filters these points to keep only the "feasible" ones (those that satisfy all $g_j(x) \leq 0$ constraints).
*   It isolates a subset of these points ($S^*$) where the penalty values are equal to or better than the penalty at $x'$.

### Step 2: Partitioning the Objectives
It analyzes how the objectives behave on the $S^*$ set and splits them into two index sets:
*   **$P_<$**: Objectives that strictly decrease.
*   **$P_=$**: Objectives that remain constant.

### Step 3: Reduced Problem Formulation (RMOP)
The script outputs a simplified "Reduced Problem". Objectives in the $P_=$ set are dropped from the objective list and converted into standard constraints.

### Step 4: Theorem 2.2 Verification
The code performs a numerical check on a specific mathematical margin to see if Theorem 2.2 holds. If the condition passes, and the RMOP is locally efficient, $\bar{x}$ is mathematically certified as a SLES.

### Step 5: Proposition 1.1 Stress-Test
*   The script runs a second, independent Monte Carlo simulation directly around the candidate point ($\bar{x}$).
*   It aggressively searches for any point that violates the core SLES inequality condition.
*   If a violating point is found, $\bar{x}$ is conclusively **NOT** a SLES. If no point is found after thousands of samples, the script concludes there is strong "numerical evidence" that $\bar{x}$ is a SLES.

---

## 3. Limitations
> **Note:** This is a numerical exploration tool, not an analytical proof generator. Finding no violations provides strong statistical confidence, but cannot guarantee absolute mathematical certainty.
