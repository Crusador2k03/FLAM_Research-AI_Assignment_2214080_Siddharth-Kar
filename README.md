This repository contains a lightweight Python script to fit a parametric 2-D curve to a cloud of (x,y) points by projecting each point onto a moving coordinate t (along a line defined by angle θ and offset X) and modelling the perpendicular coordinate s with a damped sinusoid:

s(t) = exp(M * t) * sin(0.3 t)

The script finds the best line orientation θ and offset X (outer optimization) while fitting the single amplitude/decay parameter M (inner optimization). It supports both SciPy-based optimization (fast, continuous) and a fallback grid-search when SciPy is not available.

Key features

Projects observed (x,y) into along-track t and cross-track s.

Fits s(t) to exp(M t) * sin(0.3 t) (optimizes M) for a given (θ, X).

Outer optimization over θ and X using scipy.optimize.minimize (L-BFGS-B) or a robust grid search fallback.

PRODUCES:

fitted parameters (theta in radians & degrees, X, M),

final perpendicular MSE for the s model,

mean L1 and L2 errors between observed and predicted (x,y),

LaTeX expressions for the fitted parametric curve,

fit_summary.csv with the summary of fitted values,

a diagnostic plot (if matplotlib is available).

Usage

Put your data as two columns x,y (the script reads the data_str variable by default).

Run the script:

python fit_parametric_curve.py


Output:

Console summary of fitted parameters and error metrics.

fit_summary.csv saved in the working directory.

A scatter + fitted-curve plot (if matplotlib available).

Main algorithm (brief)

Compute PCA-based initial guess for θ and estimate X so that the mean projected t is near a target.

For candidate (θ,X):

Project each (x,y) to t (along-track) and s (perp).

If all t lie in the allowed interval (6..60), fit M by minimizing MSE between s and s_model(t).

Outer optimizer picks (θ,X) minimizing the inner MSE.

Construct predicted (x,y) from fitted (θ,X,M) and compute error metrics & plots.

Dependencies

Required: numpy, pandas

Optional but recommended: scipy (for efficient optimization), matplotlib (for plotting)

Suggested install

pip install numpy pandas
