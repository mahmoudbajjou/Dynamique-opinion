# Opinion Dynamics: Modeling, Control, and Real-World Applications

This repository explores the mathematical modeling and simulation of opinion evolution within interconnected social networks. It combines classical theoretical models with modern optimization techniques—such as **Optimal Transport** and **Optimal Control**—to understand how consensus, polarization, and radicalization emerge and can be influenced.

---

##  Overview
The project is divided into three main pillars:
1.  **Theoretical Modeling**: Implementation of linear (DeGroot) and non-linear (Bounded Confidence) models.
2.  **Influence & Control**: Simulating the impact of "radical" leaders and developing "counter-radical" strategies using differential evolution.
3.  **Real-world Application**: Applying these dynamics to longitudinal data from the **World Values Survey (WVS)**.

---

##  Features

### 1. Dynamics Models
* **DeGroot Model**: A linear model where agents adjust their opinions based on a weighted average of their neighbors. Convergence to a consensus is a key property of this model.
* **Bounded Confidence (Hegselmann-Krause)**: A non-linear model where agents only interact with those whose opinions are within a specific threshold $\epsilon$.
* **Radical Influence**: Introduction of fixed-opinion agents (leaders) that can pull the collective distribution toward extremes.

### 2. Optimization & Control
* **Optimal Transport**: Uses the **POT (Python Optimal Transport)** library to find the most economical way to transform one opinion distribution into another.
* **Optimal Control**: Employs **Differential Evolution** to determine the best temporal sequence of radical opinions to achieve a target social state (e.g., maximizing the mean opinion).
* **Counter-Strategies**: Real-time optimization to neutralize radical influence and maintain social stability.

### 3. Data Analysis
* **WVS Data Processing**: Extraction and cleaning of longitudinal survey data (1981–2020) regarding perceived "freedom of choice".
* **Empirical Distributions**: Normalization and sampling of survey responses to create comparable opinion distributions across different "waves".

---

## 📁 Project Structure
The repository contains the following core components:
* `de_groot.py`: Implementation of the linear DeGroot model.
* `bounded_confidence.py`: Simulations of the Bounded Confidence model.
* `transport_optimal.py`: Optimal transport strategies using the POT library.
* `radicals.py`: Modeling of radical agents and their influence.
* `optimiseur_basinhopping.py` / `optimiseur_brute.py`: Global optimization tools for control strategies.
* `Rapport.pdf`: Comprehensive project report detailing all mathematical formulations and results.

---

##  Key Results
* **Polarization**: Low confidence thresholds ($\epsilon$) lead to fragmented "echo chambers," while higher values promote consensus.
* **Strategic Radicalization**: Volatile, extreme shifts in leader opinions ("rupture" strategies) are often more effective at destabilizing a group than constant moderate pressure.
* **Effective Defense**: Optimized counter-influence can successfully preserve a central consensus even under aggressive radical attacks.

---

##  Requirements
To run these simulations, you will need:
* Python 3.x
* `numpy`
* `matplotlib`
* `scipy`
* `POT` (Python Optimal Transport)

---
*This project was developed to model and analyze the complex dynamics of social influence.*
