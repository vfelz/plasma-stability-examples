# Plasma Stability Examples

This repository contains two compact examples developed from numerical
and analytical tools used during my PhD research on thermal instability,
coronal condensations, and normal-mode analysis in astrophysical
plasmas.

The repository is intentionally small. It contains one numerical
validation problem and one analytical exploration of the cubic
thermal-mode dispersion relation.

## Repository structure

``` text
.
├── README.md
├── homogeneous_periodic.ipynb
└── Cusp_catastrophe_clean.ipynb
```

## 1. Homogeneous periodic normal modes

`homogeneous_periodic.ipynb` solves a one-dimensional normal-mode
problem for a **static, homogeneous, adiabatic plasma with periodic
boundary conditions**.

For perturbations proportional to (e\^{nt}), the linearised equations
are

\[ n`\rho`{=tex}\_1 = -`\rho`{=tex}\_0
`\frac{\partial v_1}{\partial s}`{=tex}, \]

\[ nv_1 = -`\frac{1}{\rho_0}`{=tex} `\left[
\frac{p_0}{\rho_0}\frac{\partial \rho_1}{\partial s}
+
\frac{p_0}{T_0}\frac{\partial T_1}{\partial s}
\right]`{=tex}, \]

\[ nT_1 = -(`\gamma-1`{=tex})T_0`\frac{\partial v_1}{\partial s}`{=tex}.
\]

The notebook uses a staggered finite-difference discretisation and
solves the resulting sparse eigenvalue problem with SciPy.

For a periodic domain of length (L), the acoustic modes satisfy

\[ `\omega`{=tex}\_m = k_m c_s, `\qquad`{=tex} k_m =
`\frac{2\pi m}{L}`{=tex}, `\qquad`{=tex} c_s =
`\sqrt{\frac{\gamma p_0}{\rho_0}}`{=tex}. \]

The numerical acoustic frequencies are compared with this analytical
result. In the adiabatic problem, the (n=0) branch corresponds to a
stationary entropy perturbation rather than the absence of a mode.

## 2. Cubic root structure and cusp discriminant

`Cusp_catastrophe_clean.ipynb` explores the cubic thermal-mode
dispersion relation through its depressed-cubic form

\[ x\^3 + ax + b = 0. \]

The notebook examines the discriminant

\[ `\Delta `{=tex}= -4a\^3 - 27b\^2, \]

the associated root degeneracies, critical wavenumbers, and the path
traced by the physical system through the ((a,b)) control plane as the
wavenumber varies.

The curve

\[ 4a\^3 + 27b\^2 = 0 \]

is the bifurcation set of the canonical cusp catastrophe. The notebook
uses this geometry to visualise changes in the algebraic root structure
while keeping the distinction between a **cubic root degeneracy** and a
stronger dynamical catastrophe interpretation explicit.

The analysis also transforms the depressed-cubic roots back to the
original eigenvalue variable before examining the physical root
branches.

## Requirements

The notebooks use standard Python scientific-computing packages.

``` bash
pip install numpy scipy matplotlib sympy
```

The optional interactive three-dimensional cusp visualization
additionally uses Plotly:

``` bash
pip install plotly
```

## Research context

These notebooks are simplified examples extracted from a larger
normal-mode-analysis framework developed during my PhD research at the
Universitat de les Illes Balears (UIB).

The full research framework treats thermal instability in spatially
structured and dynamically evolving coronal-loop backgrounds and
includes additional physical effects. Those components are intentionally
not included in this public repository.

## Author

**Varsha Felsy**\
PhD Candidate in Physics\
Universitat de les Illes Balears (UIB)

GitHub: `vfelz`
