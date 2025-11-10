# 📈 Parametric Curve Fitting

This repository contains a Python implementation for fitting a **damped sinusoidal parametric curve** to a set of 2-D data points `(x, y)`.  
It estimates the optimal orientation `θ`, horizontal offset `X`, and exponential coefficient `M` by minimizing the perpendicular mean-squared error between model predictions and observed data.

---

## ⚙️ Model Overview

The fitted curve is expressed as:

\[
(x, y) =
\left(
X + t\cos(\theta) - e^{M|t|}\sin(0.3t)\sin(\theta),\;
42 + t\sin(\theta) + e^{M|t|}\sin(0.3t)\cos(\theta)
\right)
\]

where:

- `θ` → orientation angle (radians or degrees)  
- `X` → x-axis offset (translation)  
- `M` → exponential growth/decay coefficient  

---

## 🧮 Fitted Equation (Radians)

<p align="center">
  <img src="Screenshot_2025-11-10_221323.png" alt="Equation in radians" width="750">
</p>

---

## 📊 Model Fitting Results

<p align="center">
  <img src="Screenshot_2025-11-10_221647.png" alt="Model fitting results table" width="750">
</p>

---

## 📈 Mean Euclidean Error

<p align="center">
  <img src="Screenshot_2025-11-10_221742.png" alt="Mean Euclidean distance result" width="600">
</p>

---

## 🧾 Fitted Equation (Degrees)

<p align="center">
  <img src="Screenshot_2025-11-10_221341.png" alt="Equation in degrees" width="750">
</p>

---

## 🧠 Method Summary

1. **Data projection**:  
   Observed `(x, y)` points are projected to local coordinates `(t, s)` defined by an axis with angle `θ` and offset `X`.

2. **Inner fit (M)**:  
   For each `(θ, X)`, the exponential coefficient `M` is optimized by minimizing mean squared error between observed and modeled `s(t)`.

3. **Outer optimization**:  
   Global minimization of `(θ, X)` using `scipy.optimize.minimize` (`L-BFGS-B`) or fallback grid search.

4. **Result evaluation**:  
   - `mean_L1` and `mean_L2` errors computed  
   - LaTeX curve expression printed  
   - Fitted curve visualized using `matplotlib`

---

## 📦 Dependencies

```bash
pip install numpy pandas
# optional (recommended)
pip install scipy matplotlib

