# Strict Local Efficiency Analyzer for Multiobjective Optimization

This repository provides an interactive Python implementation of the mathematical framework proposed in the research paper: **"Characterizing strict efficiency for convex multiobjective programming problems"** by Anjana Gupta, Aparna Mehra, and Davinder Bhatia.

Navigating the theory of higher-order Strict Local Efficient Solutions (s.l.e.s.) can be mathematically heavy. This project bridges that gap by providing a dynamic, computational tool that analyzes Multiobjective Programming Problems (MOPs), evaluates localized distance penalties, and automatically partitions objective functions to construct Reduced Multiobjective Programming Problems (RMOPs).

---

## 🚀 Features

* **Interactive Mathematical Parsing:** Define custom objective functions and inequality constraints directly via the console using standard algebraic text.
* **Automated Objective Partitioning:** Automatically categorizes objective sets into essential ($P^<$) and non-essential ($P^=$) indices.
* **Monte Carlo Neighborhood Sampling:** Explores the feasible space $B(x^*, \delta)$ dynamically to bypass the limitations of complex analytical boundary checking.
* **Constraint Validation:** Built-in feasibility checking to strictly enforce $g_j(x) \le 0$ across all randomly sampled points.

---

## 🌐 Interactive Google Colab Notebook

Want to see the model in action without installing anything locally? You can run the entire SLES analysis tool directly in your browser using Google Colab. This environment is pre-configured with all necessary dependencies, allowing you to instantly experiment with the Monte Carlo sampling and objective partitioning.

[![Open In Colab]([https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/akshat-tyagi-2006/internship-project/blob/main/project.ipynb](https://colab.research.google.com/drive/1hlf8XS6TXh7R7QNJCJv84bvxcGukTDIc?usp=sharing))

## ⚙️ How the Code Works

This script numerically tests whether a specific candidate point ($\bar{x}$) is a Strict Local Efficient Solution (SLES). Instead of using complex analytical calculus, it uses randomized sampling to verify the mathematical conditions.

1. **Penalty Calculation & Sampling:** 
   The script defines a penalty function for each objective: 
   $$pen_i(x) = f_i(x) - \alpha_i \|x - \bar{x}\|^m$$
   It generates random points inside a defined radius ($\delta$) around a test point ($x'$). It filters these to keep only "feasible" points (where $g_j(x) \le 0$). Then, it isolates a subset of these points ($S^*$) where the penalty values are equal to or better than the penalty at $x'$.
2. **Partitioning the Objectives:** 
   It analyzes how the objectives behave on the $S^*$ set and splits them into two index sets:
   * **$P_<$**: Objectives that strictly decrease.
   * **$P_=$**: Objectives that remain constant.
3. **Reduced Problem Formulation (RMOP):** 
   The script outputs a simplified "Reduced Problem". Objectives in the $P_=$ set are dropped from the objective list and converted into standard constraints.
4. **Theorem 2.2 Verification:** 
   It performs a numerical check on a specific mathematical margin to see if Theorem 2.2 holds.
5. **Stress-Test:** 
   The script runs a second, independent Monte Carlo simulation directly around the candidate point ($\bar{x}$). It aggressively searches for any point that violates the core SLES inequality condition. If no point is found after thousands of samples, it concludes there is strong "numerical evidence" that $\bar{x}$ is a SLES.

> **Limitations:** This is a numerical exploration tool, not an analytical proof generator. Finding no violations provides strong statistical confidence, but cannot guarantee absolute mathematical certainty.

---

## 🛠️ Prerequisites & Installation

This project is built using Python 3 and relies on two core libraries for matrix operations and algebraic parsing.

Ensure you have Python 3.7+ installed, then run the following command to install the required dependencies:

```bash
pip install numpy sympy
