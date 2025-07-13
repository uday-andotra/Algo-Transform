# 3SAT-to-ExperimentalCuisine-Reduction

## Overview

This repository implements a polynomial-time reduction from the 3SAT problem to a custom NP-complete problem called "Experimental Cuisine." The algorithm takes a 3SAT formula with \( m \) clauses and \( n \) variables as input and produces a graph \( G_F = (V, E) \) with \( |V| = 3m \) vertices and \( |E| = 3m + k \) edges (\( k = O(m^2) \)), encoding the formula. If the 3SAT instance is satisfiable, the graph contains an independent set of size \( m \); otherwise, it does not.

The project was developed for CS 512 (Algorithms) under Prof. Abello by Nicholas Gutierrez, Udayveer Singh Andotra, and Ridwanur Sarder.

Key components:
- **Input**: 3SAT clauses from CSV files.
- **Transformation**: Generates "ingredients" (true configurations per clause) and a discord matrix for incompatibilities.
- **Output**: Verifies satisfiability via brute-force search and optional PySAT solver.
- **Complexity**: Time and space dominated by discord matrix: \( O((7m)^2) \).

The repository includes a Jupyter notebook for the implementation, sample 3SAT instances (satisfiable and unsatisfiable), and a project report PDF.

## Table of Contents

- [Overview](#overview)
- [Files](#files)
- [Requirements](#requirements)
- [Installation and Setup](#installation-and-setup)
- [Usage](#usage)
- [Methods](#methods)
- [Results](#results)
- [References](#references)

## Files

- **`Algo_transformation_Project_Group_5.ipynb`**: Jupyter Notebook implementing the 3SAT to Experimental Cuisine transformation, brute-force solution search, verification, and optional PySAT validation.
- **`3sat_clauses_1.csv`**, **`3sat_clauses_2.csv`**, **`3sat_clauses_3.csv`**, **`3sat_clauses_unsatisfiable.csv`**: Sample 3SAT clause inputs in CSV format (satisfiable and unsatisfiable instances).
- **`DS and Alg Project Report Group 5.pdf`**: Project report detailing the problem, algorithm, complexity analysis, and results.

## Requirements

### Python Dependencies
- itertools
- copy
- numpy
- pysat (for optional SAT solver verification)

## Installation and Setup

1. Clone the repository:
   ```
   git clone https://github.com/uday-andotra/3SAT-to-ExperimentalCuisine-Reduction.git
   cd 3SAT-to-ExperimentalCuisine-Reduction
   ```

2. Install dependencies via pip:
   ```
   pip install numpy pysat
   ```

## Usage

### Running the Jupyter Notebook
- Open `Algo_transformation_Project_Group_5.ipynb` in Jupyter Notebook or Google Colab.
- Update the CSV file path in the "Reading Input" section to one of the provided CSVs (e.g., `3sat_clauses_2.csv` for a satisfiable instance).
- Run all cells sequentially.
- Key outputs: 
  - List of ingredients and discord matrix.
  - Satisfiability check with variable assignments (if satisfiable).
  - Verification for both 3SAT and Experimental Cuisine.
  - Optional: All satisfying assignments via PySAT.

For unsatisfiable inputs (e.g., `3sat_clauses_unsatisfiable.csv`), the brute-force search will report no solution.

## Methods

### Transformation Algorithm
1. **Read 3SAT Input**: Parse clauses from CSV, identify unique variables.
2. **Generate Ingredients**: For each clause, enumerate 7 true configurations (all but the all-false case).
3. **Discord Matrix**: \( O((7m)^2) \) matrix where entries indicate incompatibilities (same-clause opposites or cross-clause negations).
4. **Brute-Force Search**: Iterate over combinations of ingredients (one per clause) to find a discord-free selection (independent set of size \( m \)).
5. **Verification**: Map selection back to variable assignments and validate against original 3SAT.

If no such selection exists, the 3SAT is unsatisfiable.

For mathematical details and proofs, refer to the PDF report.

## Results

- **Time/Space Complexity**: \( O((7m)^2) \) due to discord matrix construction.
- **Sample Outputs**:
  - Satisfiable instances: Outputs variable assignments (e.g., x1=True, x2=True, x3=True) and confirms zero discord.
  - Unsatisfiable: Reports no solution.
- **Extra Validation**: PySAT enumerates all satisfying assignments for comparison.

The transformation preserves satisfiability, as shown in the report.

## References

- Garey and Johnson, "Computers and Intractability: A Guide to the Theory of NP-Completeness" (1979).
- PySAT library for SAT solving.
