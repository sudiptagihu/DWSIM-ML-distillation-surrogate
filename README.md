<<<<<<< HEAD
# Binary Benzene-Toluene Distillation Column Surrogate Modeling

A comprehensive machine learning surrogate modeling framework for a continuous binary distillation column (`DCOL-1`) modeled in **DWSIM** using the Peng-Robinson equation of state.

---

## 📋 Project Overview
Rigorous thermodynamic simulations like DWSIM are computationally intensive, making them challenging for real-time optimization, digital twins, and Model Predictive Control (MPC). This project addresses this by generating a high-fidelity dataset from DWSIM sensitivity analysis and benchmarking multiple machine learning surrogate architectures to emulate the column's steady-state behavior with millisecond-level inference times.

---

## ⚙️ DWSIM Simulation Parameters
* **Feed Mixture:** Equimolar binary solution ($0.5$ Benzene, $0.5$ Toluene molar ratio)
* **Feed Conditions:** $T = 298.15\text{ K}$ ($25^\circ\text{C}$), $P = 101,325\text{ Pa}$ ($1.01325\text{ bar}$)
* **Column Setup (`DCOL-1`):** $20$ equilibrium stages, feed introduced at stage $10$
* **Thermodynamic Package:** Peng-Robinson (PR) Equation of State

---

## 📊 Dataset Summary (`Dataset.csv`)
Generated via full-factorial sensitivity analysis across $N = 120$ converged steady-state instances:
* **Inputs / Independent Variables:**
  * Condenser Specification Value ($S_{cond}$ / Reflux Ratio): Uniformly discretized from $1.20$ to $5.00$ ($24$ steps)
  * Reboiler Specification Value ($S_{reb}$): Sampled at $5$ discrete levels ($1.00, 1.50, 2.00, 2.50, 3.00$)
* **Outputs / Target Variables:**
  * Distillate Benzene Purity ($x_D$)
  * Bottoms Toluene Purity ($x_B$)
  * Condenser Thermal Duty ($Q_C$)
  * Reboiler Thermal Duty ($Q_R$)

---

## 🤖 Machine Learning Surrogate Models Benchmarked
Models were evaluated using an 80:20 train-test split ($N_{train} = 96$, $N_{test} = 24$) with Z-score standardization:

1. **Polynomial Regression (Degree 2):** Best overall performance. Captures physical quadratic response surfaces of vapor-liquid equilibrium and energy balances exceptionally well ($R^2 \approx 1.0000$ for duties).
2. **Random Forest ($N=100$):** Non-parametric ensemble approach capturing general trends with strong reliability.
3. **Artificial Neural Network (ANN):** Deep architecture optimized for nonlinear multi-input multi-output mapping.

### Summary Performance Table
| Architecture | Target Variable | MAE | RMSE | $R^2$ Score |
| :--- | :--- | :--- | :--- | :--- |
| **Polynomial Reg (Deg 2)** | Distillate Benzene ($x_D$) <br> Bottoms Purity ($x_B$) <br> Condenser Duty ($Q_C$) <br> Reboiler Duty ($Q_R$) | $0.000125$ <br> $0.000016$ <br> $0.05016\text{ kW}$ <br> $0.04988\text{ kW}$ | $0.000138$ <br> $0.000032$ <br> $0.06622\text{ kW}$ <br> $0.06532\text{ kW}$ | $0.999992$ <br> $0.915369$ <br> $1.000000$ <br> $1.000000$ |

---

## 🚀 Getting Started
1. Ensure Python dependencies are installed (`numpy`, `pandas`, `scikit-learn`, `matplotlib`).
2. Place your `Dataset.csv` file in the root workspace directory.
3. Run the surrogate training script to reproduce parity plots and polynomial coefficients.
=======
# DWSIM-ML-distillation-surrogate
A comprehensive machine learning surrogate modeling pipeline for a binary distillation column using DWSIM simulation data, comparing multiple regression models (Polynomial Regression, Random Forest, ANN) for real-time performance and energy prediction. This project is open-source and available under the MIT License.
>>>>>>> d586e3fbc4f2e7f11418270235d7f7511e42075b
