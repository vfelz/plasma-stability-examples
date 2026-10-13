# Plasma Stability Examples

This repository contains three compact examples developed from numerical
and analytical tools used during my PhD research on thermal instability,
coronal condensations, and normal-mode analysis (NMA) in astrophysical
plasmas.

The examples illustrate different aspects of linear plasma stability,
including numerical eigenvalue analysis, the effects of thermal conduction
and radiative losses, and the mathematical structure of the thermal-mode
dispersion relation.

The repository is intentionally small and focuses on reproducible,
educational examples rather than the full research framework.

## Repository structure

```text
.
├── README.md
├── homogeneous_periodic.ipynb
├── NMA_toy_model.ipynb
├── nma_example_background.h5
└── Cusp_catastrophe_clean.ipynb
```

## 1. Homogeneous periodic normal modes

`homogeneous_periodic.ipynb` solves a one-dimensional normal-mode
problem for a **static, homogeneous, adiabatic plasma with periodic
boundary conditions**.

Assuming perturbations proportional to $e^{nt}$, the linearised equations are

$$
n\rho_1 = -\rho_0\frac{\partial v_1}{\partial s},
$$

$$
nv_1 = -\frac{1}{\rho_0}
\left[
\frac{p_0}{\rho_0}\frac{\partial \rho_1}{\partial s}
+
\frac{p_0}{T_0}\frac{\partial T_1}{\partial s}
\right],
$$

$$
nT_1 = -(\gamma-1)T_0\frac{\partial v_1}{\partial s}.
$$

The notebook uses a staggered finite-difference discretisation and
solves the resulting sparse eigenvalue problem with SciPy.

For a periodic domain of length $L$, the acoustic modes satisfy

$$
\omega_m = k_m c_s,
\qquad
k_m = \frac{2\pi m}{L},
\qquad
c_s = \sqrt{\frac{\gamma p_0}{\rho_0}}.
$$

The numerical acoustic frequencies are compared with this analytical
result.

In the adiabatic problem, the $n=0$ branch corresponds to a stationary
entropy perturbation rather than the absence of a mode.

## 2. Normal-mode analysis with thermal conduction and radiative losses

`NMA_toy_model.ipynb` provides a more general example of normal-mode
analysis in a one-dimensional hydrodynamic plasma.

The notebook is based on a simplified version of the numerical framework
developed for studying thermal instability in coronal loops.

It considers a static background and solves the linearised continuity,
momentum, and energy equations, including the effects of radiative
cooling and thermal conduction.

The perturbations are assumed to evolve as

$$
f_1(s,t)=\hat{f}_1(s)e^{nt},
$$

where the complex eigenvalue $n$ determines the growth rate and
oscillation frequency.

The linearised equations are discretised using a staggered
finite-difference grid, leading to the matrix eigenvalue problem

$$
\mathbf{A}\mathbf{x}=n\mathbf{x},
$$

where

$$
\mathbf{x}=
\begin{pmatrix}
\boldsymbol{\rho}_1\\
\mathbf{v}_1\\
\mathbf{T}_1
\end{pmatrix}.
$$

The resulting dense eigenvalue problem is solved using `scipy.linalg.eig`.

### Features

- Background density and temperature profiles loaded from an external
  HDF5 file.
- Independent control of the numerical grid resolution, with interpolation
  of the input background.
- Staggered finite-difference discretisation.
- Two boundary-condition options:
  - **Reflecting:** $v_1=0$, $\partial_s\rho_1=0$, and $\partial_sT_1=0$.
  - **Line-tied:** $v_1=0$ and $T_1=0$.
- Optional thermal conduction and radiative cooling.
- Identification of growing, damped, and oscillatory eigenmodes.
- Visualisation of eigenvalue spectra and eigenfunctions.
- Comparison of adiabatic acoustic frequencies with analytical results.
- Residual diagnostics for the linearised equations.

The example uses a homogeneous equilibrium, although the input background
is read from an external file. Extending the analysis to nonuniform
equilibria requires additional terms and appropriate equilibrium constraints.

### Boundary conditions and validation

In the homogeneous adiabatic limit, reflecting boundaries reproduce the
expected standing acoustic waves,

$$
\omega_m=\frac{m\pi c_s}{L}.
$$

The corresponding velocity eigenfunctions have a sine dependence, while
the density and temperature perturbations follow cosine profiles.

For line-tied boundaries, imposing both $v_1=0$ and $T_1=0$ is incompatible
with the usual nontrivial standing acoustic solutions in the strictly
adiabatic homogeneous problem.

The inclusion of thermal conduction allows temperature boundary layers
to develop and permits the use of Dirichlet temperature conditions in
the nonadiabatic problem.

The notebook includes a discussion of this distinction and residual
diagnostics to assess the numerical solutions.

**Note:** This notebook is intended as a pedagogical example. The
adiabatic acoustic modes have been checked against analytical solutions,
but the full nonadiabatic formulation should not be considered a
comprehensively validated research solver.

## 3. Cubic root structure and cusp discriminant

`Cusp_catastrophe_clean.ipynb` explores the cubic thermal-mode
dispersion relation through its depressed-cubic form

$$
x^3+ax+b=0.
$$

The notebook examines the discriminant

$$
\Delta=-4a^3-27b^2,
$$

the associated root degeneracies, critical wavenumbers, and the path
traced by the physical system through the $(a,b)$ control plane as the
wavenumber varies.

The curve

$$
4a^3+27b^2=0
$$

is the bifurcation set of the canonical cusp catastrophe.

The notebook uses this geometry to visualise changes in the algebraic
root structure while keeping the distinction between a **cubic root
degeneracy** and a stronger dynamical catastrophe interpretation explicit.

The analysis also transforms the depressed-cubic roots back to the
original eigenvalue variable before examining the physical root
branches.

## Requirements

The notebooks use standard Python scientific-computing packages.

```bash
pip install numpy scipy matplotlib sympy h5py
```

The optional interactive three-dimensional cusp visualisation
additionally uses Plotly:

```bash
pip install plotly
```

## Getting started

Clone the repository:

```bash
git clone https://github.com/vfelz/Plasma-Stability-Examples.git
```

Navigate to the repository and launch Jupyter:

```bash
cd Plasma-Stability-Examples
jupyter notebook
```

Each notebook can be run independently.

For `NMA_toy_model.ipynb`, ensure that the example HDF5 background file
is available in the working directory.

## Research context

These notebooks are simplified examples extracted from a larger
normal-mode-analysis framework developed during my PhD research at the
Universitat de les Illes Balears (UIB).

The full research framework treats thermal instability in spatially
structured and dynamically evolving coronal-loop backgrounds and
includes additional physical effects, such as gravity, background
flows, and variations in loop cross-sectional area.

Those components are intentionally not included in this public
repository.

## Author

**Varsha Felsy**  
PhD Candidate in Physics  
Universitat de les Illes Balears (UIB)

GitHub: [vfelz](https://github.com/vfelz)
