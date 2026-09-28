# LMCE2026 Immune-State Modeling

## Overview

This repository contains the computational workflow for a mathematical state-space analysis of whole-blood transcriptomics in bacterial, viral, and noninfectious febrile illness.

The study integrates transcriptomic immune-program characterization with an interpretable linear Ordinary Differential Equations (ODE) state-space framework to estimate relationships among latent immune states and evaluate the stability of the estimated system.

This project was prepared for LMCE 2026.

## Dataset

The analysis uses the publicly available whole-blood RNA-sequencing dataset **GSE211567** from the NCBI Gene Expression Omnibus (GEO).

The final analytical cohort includes **290 clinically annotated samples**:

- Bacterial: 101
- Viral: 123
- Noninfectious: 66

Raw sequencing data are not redistributed in this repository. The original data can be obtained from GEO using accession **GSE211567**.

## Immune-State Representation

Gene-expression profiles were summarized into four biologically informed immune programs:

- Interferon-antiviral
- Neutrophil-antibacterial
- Myeloid-inflammatory
- Regulatory-resolution

These programs were used to construct a low-dimensional representation of host immune states.

## Mathematical Framework

A linear Ordinary Differential Equations (ODE) state-space model was used to estimate relationships among four biologically informed transcriptomic immune programs: **Interferon–Antiviral (I)**, **Neutrophil–Antibacterial (N)**, **Myeloid–Inflammatory (M)**, and **Regulatory–Resolution (R)**.

Rather than modeling thousands of genes individually, these four programs were represented as a low-dimensional immune-state vector:

\[
X(t)=
\begin{bmatrix}
I(t)\\
N(t)\\
M(t)\\
R(t)
\end{bmatrix}
\]

The model can be represented as:

\[
\frac{dX}{dt}=AX
\]

where **X** represents the four-dimensional immune-state vector and **A** represents the estimated interaction matrix. Interaction coefficients were estimated using ridge-regularized regression.

The estimated interaction matrix was:

\[
A=
\begin{bmatrix}
-1.026 & -0.128 & -0.294 & +0.141\\
-0.013 & -0.835 & +0.143 & -0.090\\
-0.064 & +0.034 & -1.052 & +0.010\\
+0.002 & -0.094 & -0.163 & -0.766
\end{bmatrix}
\]

Rows correspond to the modeled change in each immune program, while columns represent the estimated contribution of each immune program to that change. The diagonal elements describe estimated **self-regulation**, whereas the off-diagonal elements describe estimated **cross-program coupling**.

For example, the first row of the matrix gives the interferon-state equation:

\[
\frac{dI}{dt}
=
-1.026I
-0.128N
-0.294M
+0.141R
\]

Within the fitted model, the negative diagonal coefficient for interferon (**−1.026**) represents estimated negative self-regulation. The myeloid-to-interferon coefficient (**−0.294**) represents negative cross-program coupling, whereas the regulatory-to-interferon coefficient (**+0.141**) represents positive coupling. These coefficients describe relationships within the fitted transcriptomic state-space model and should not be interpreted as experimentally established causal molecular interactions.

The linear formulation is intended as an interpretable approximation of local immune-state relationships and does not assume that the underlying biological immune system is globally linear.

### Stability of the Estimated System

System stability was evaluated from the eigenvalue spectrum of the estimated interaction matrix **A**. The four estimated eigenvalues were approximately:

\[
\lambda =
\{-1.16,\,-0.97,\,-0.89,\,-0.67\}
\]

All eigenvalues had negative real parts:

\[
\operatorname{Re}(\lambda_i)<0
\]

which indicates **asymptotic stability of the estimated continuous linear ODE system**. In mathematical terms, perturbations within the fitted linear system tend to decay rather than increase indefinitely.

This stability result refers specifically to the mathematical behavior of the estimated ODE system and should not be interpreted as direct evidence that an individual patient's biological immune response is clinically stable.

### How to Interpret the Model

The framework can be understood conceptually as:

**Whole-blood transcriptomics**

→ **Gene-expression profiles**

→ **Four immune programs (I, N, M, R)**

→ **Four-dimensional immune-state vector X**

→ **Estimated interaction matrix A**

→ **Linear ODE system dX/dt = AX**

→ **Interaction structure and eigenvalue-based stability analysis**

Because GSE211567 contains cross-sectional transcriptomic measurements rather than serial longitudinal measurements from the same individuals, the ODE represents an **inferred transcriptomic state-space model**. Accordingly, \(dX/dt\) is a model-derived state-space quantity rather than a directly measured patient-level change over chronological time.

The model therefore provides an interpretable mathematical representation of **immune-state structure, self-regulation, cross-program coupling, and system stability**, rather than a direct reconstruction of longitudinal immune kinetics.

## Analysis Workflow

The computational workflow includes:

1. Transcriptomic data processing and gene annotation
2. Clinical metadata harmonization
3. Construction of biologically informed immune programs
4. Low-dimensional immune-state representation
5. Linear ODE state-space modeling
6. Ridge-regularized estimation of immune interactions
7. Eigenvalue-based stability analysis
8. Immune-program correlation analysis
9. Immune fingerprint characterization
10. Model-derived immune-state analyses and visualization

## Interpretation and Limitations

GSE211567 provides cross-sectional transcriptomic measurements rather than longitudinal measurements of individual patients.

Therefore, the ODE framework should be interpreted as an **inferred transcriptomic state-space model**. Model-derived transition tendencies and interaction coefficients do not represent directly observed longitudinal immune kinetics.

The framework is intended for computational characterization and hypothesis generation and requires independent validation before clinical application.

## Software

Analyses were performed using **Python** and **Jupyter Notebook**.

The principal computational notebook and software dependencies are provided in this repository to support reproducibility.

## Repository Structure

```text
LMCE2026-Immune-State-Modeling/
├── README.md
├── .gitignore
├── requirements.txt
└── notebooks/
    └── LMCE2026_Immune_State_ODE_Modeling.ipynb
