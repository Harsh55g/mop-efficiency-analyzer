# Strict Local Efficiency Analyzer for Multiobjective Optimization

This repository provides an interactive Python implementation of the mathematical framework proposed in the 2007 research paper: **"Characterizing strict efficiency for convex multiobjective programming problems"** by Anjana Gupta, Aparna Mehra, and Davinder Bhatia.

Navigating the theory of higher-order Strict Local Efficient Solutions (s.l.e.s.) can be mathematically heavy. This project bridges that gap by providing a dynamic, computational tool that analyzes Multiobjective Programming Problems (MOPs), evaluates localized distance penalties, and automatically partitions objective functions to construct Reduced Multiobjective Programming Problems (RMOPs).

---

## 🚀 Features

* **Interactive Mathematical Parsing:** Define custom objective functions and inequality constraints directly via the console using standard algebraic text.
* **Automated Objective Partitioning:** Automatically categorizes objective sets into essential ($P^<$) and non-essential ($P^=$) indices.
* **Monte Carlo Neighborhood Sampling:** Explores the feasible space $B(x^*, \delta)$ dynamically to bypass the limitations of complex analytical boundary checking.
* **Constraint Validation:** Built-in feasibility checking to strictly enforce $g_j(x) \le 0$ across all randomly sampled points.

---

## 🛠️ Prerequisites & Installation

This project is built using Python 3 and relies on two core libraries for matrix operations and algebraic parsing.

Ensure you have Python 3.7+ installed, then run the following command to install the required dependencies:

```bash
pip install numpy sympy

```

---

## 💻 Usage

To launch the interactive framework, simply run the main script from your terminal:

```bash
python strict_efficiency_model.py

```

### Input Walkthrough

The console will prompt you to build your multiobjective problem step by step:

1. **Variables:** Enter the number of decision variables ($n$). The model assumes the format `x1`, `x2`, etc.
2. **Objectives ($p$):** Enter each function you want to minimize using standard Python math syntax (e.g., `x12 + sp.sqrt(x2)`).
3. **Constraints ($q$):** Enter the inequality rules in the format $g(x) \le 0$ (e.g., `x1 + x2 - 1`).
4. **Parameters:**
* `x_bar`: The target solution point being evaluated.
* `alpha`: The penalty scaling vector.
* `delta`: The radius of the local neighborhood to sample.
* `m`: The strictness order coefficient ($m \ge 1$).
* `x_star`: The neighborhood test point.



### Example Execution

If you want to replicate **Example 2.1** from the research paper, use the following inputs when prompted:

* Variables: `2`
* Objective 1: `-x1 + x2`
* Objective 2: `sp.sqrt(x12 + x22)` *(Note: This is a simplified boundary for the example)*
* Constraint 1: `x1 - x2 + 0.5*x1*x2 - 1`
* Constraint 2: `x12 + x22 - 2`
* Parameters: `x_bar` = `0 0`, `alpha` = `1 0.5`, `delta` = `0.5`, `m` = `1`, `x_star` = `1 0`

---

## 🧠 Mathematical Background

This framework determines if a point is a Strict Local Efficient Solution by penalizing objectives based on their distance from a target solution $\overline{x}$.

The core evaluation relies on the penalized objective formula:

$$f_i(x) - \alpha_i \|x - \overline{x}\|^m$$

By evaluating thousands of feasible points in a localized neighborhood, the engine splits the objectives into two sets:

* **$P^=$ (Equal Set):** The non-essential objectives where the penalized score remains completely static across the local neighborhood.
* **$P^<$ (Strictly Less Set):** The essential objectives driving the optimization, where the penalized score strictly decreases for at least one feasible point in the neighborhood.

---

## 📖 Citation & References

If you use this code in an academic or research context, please refer back to the original mathematical theory:

> Gupta, A., Mehra, A., & Bhatia, D. (2007). Characterizing strict efficiency for convex multiobjective programming problems. *Journal of Global Optimization*, 49(2), 265-280. DOI: 10.1007/s10898-010-9543-7

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! If you want to enhance the boundary-detection algorithms, improve the Monte Carlo sampling efficiency, or extend the tool for saddle-point criteria mapping (Section 4 of the paper), feel free to open a pull request.
