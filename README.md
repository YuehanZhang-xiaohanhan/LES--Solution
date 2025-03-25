# LES--Solution
#  Yuehan Zhang - ISE Coursework: Performance Tuning Classification Model

## Project Overview

This is the Lab 3 coursework project by Yuehan Zhang for the ISE course, focusing on **Performance Tuning and Optimization Algorithms**.

I designed and implemented **6 tuning strategies** to explore their adaptability and optimization effects across real system configuration spaces. The tested algorithms include:

- BestConfig (dimension-wise perturbation)
- Decision Tree Regressor
- Flash (CART-based model)
- Bayesian Optimization
- Genetic Algorithm (GA)
- Bayesian + Genetic Algorithm (hybrid)

These were applied to **8 representative systems**:  
`7z`, `Apache`, `brotli`, `LLVM`, `PostgreSQL`, `spear`, `storm`, and `x264`.  
Each data point represents a full configuration trial with associated performance metrics (e.g., runtime, throughput, compression ratio).

---

## Project Structure

```
lab3/
│
├──  datasets/                                  # Dataset files
│
├──  doc/                                       # Documentation
│   ├──  Yuehan Zhang ISE lab3.pdf              # Lab report
│   ├──  replicationpdf.pdf                     # Replication instructions
│
├──  results/                                   # Output performance data
│   └──  *_search_results.csv
│
├──  results_img/                               # Visualized performance graphs
│   └──  Search_Results_Visualization_for_*.png
│
├──  main.py                                    # Main entry point
├──  README.md                                  # Project README
├──  requirements.txt                           # Python dependencies
└──  visualization.ipynb                        # Notebook for visualizing results
```

---

## Environment Setup

- Windows 10/11 or macOS  
- Python 3.10+  
- Recommended IDE: VSCode  

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Run Tuning Experiment

To run the tuning workflow (excluding Bayesian + GA hybrid by default):

```bash
python main.py
```

To replicate a specific algorithm or dataset, modify the search method and dataset path in `main.py`.

---

## Optimization Algorithms

| Algorithm        | Description |
|------------------|-------------|
| **BestConfig**   | Coordinate-wise search, fast but easily trapped in local optima. |
| **Decision Tree**| Uses regression trees to model config-performance relations. |
| **Flash**        | Based on CART trees; robust for high-dim tasks with steep performance cliffs. |
| **Bayesian**     | Uses Gaussian processes via `skopt.gp_minimize`; good for expensive evals. |
| **GA**           | Simulates evolutionary process via DEAP; good for large discrete spaces. |
| **Bayesian + GA**| Hybrid that combines global exploration and convergence speed. |

---

## Sample Results

| System      | BestConfig | Decision Tree | Flash | Bayesian | GA   | Bayes + GA |
|-------------|------------|----------------|--------|-----------|------|-------------|
| 7z          | 4353.8     | 4196.4         | 4196.4 | 849149.2  | 4327.4 | 4361.8     |
| Apache      | 31.03      | 30.74          | 30.74  | 162.9     | 32.55  | 30.59      |
| brotli      | 1.46       | 1.46           | 1.46   | 1.574     | 1.46   | 1.46       |
| LLVM        | 59297.6    | 52285.4        | 52285.4| 207383.6  | 55001.2| 55200.1    |
| PostgreSQL  | 45922.8    | 45922.8        | 45922.8| 287886.4  | 46054.6| 46099.7    |
| spear       | 0.0        | 0.0            | 0.0    | ~0        | ~0     | ~0         |
| storm       | ~0         | 0.0            | 0.0    | 0.0148    | ~0.00004 | ~0.00003 |
| x264        | 22.14      | 21.56          | 21.58  | 21.67     | 21.71  | 21.73      |

> Performance values are minimized. Lower is better.

---

## Visualizing Performance

To see the convergence trend of each optimization method per system:

1. Open `visualization.ipynb` in Jupyter or VSCode.
2. Run all cells.
3. Visual performance plots will be saved to `results_img/`.

Each graph shows:
- **Blue line**: performance over iterations
- **Red star**: best config found so far

---

## Key Takeaways

- **Bayesian Optimization** works best in low-dimensional or smooth spaces.
- **Decision Tree / Flash** models are more robust across systems.
- **Genetic Algorithm** offers good diversity but may require careful tuning.
- **Bayesian + GA** is a strong hybrid, balancing exploration and convergence.

---

## Troubleshooting

- If `skopt` is missing, install with:
```bash
pip install scikit-optimize
```
- Define custom parameter bounds per system before search.
- Some methods (e.g., Flash) may take several minutes per dataset.
- Bayesian Optimization may underperform if the objective function is too flat.

---

## Citation & Reference

If referencing this project, please cite:

> Zhang, Y. (2025). *Performance tuning classification model: Exploratory evaluation based on optimization algorithms*. University of Birmingham, ISE Lab 3.

Related works:
1. Hutter et al. (2011). SMBO for Algorithm Configuration.
2. Bergstra et al. (2013). Hyperparameter Optimization in Vision Models.
3. Feurer et al. (2015). Efficient AutoML with SMAC.

---

## GitHub Repository

Full source code, dataset, and replication instructions:  
🔗 https://github.com/YuehanZhang-xiaohanhan/LES--Solution
