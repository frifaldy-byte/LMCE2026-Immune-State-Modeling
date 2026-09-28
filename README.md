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

## Mathematical Framework

A linear Ordinary Differential Equations (ODE) state-space model was used to estimate relationships among four biologically informed transcriptomic immune programs: **Interferon–Antiviral (I)**, **Neutrophil–Antibacterial (N)**, **Myeloid–Inflammatory (M)**, and **Regulatory–Resolution (R)**.

Rather than modeling thousands of individual genes separately, the transcriptomic information was summarized into a low-dimensional immune-state representation. The four immune programs form the state vector:

$$
X(t)=
\begin{bmatrix}
I(t) \\
N(t) \\
M(t) \\
R(t)
\end{bmatrix}
$$

where each component represents the activity of one transcriptomic immune program within the reduced immune-state space.

### Linear ODE State-Space Model

The immune-state system was represented as:

$$
\frac{dX}{dt}=AX
$$

where **X** is the four-dimensional immune-state vector and **A** is the estimated interaction matrix. Interaction coefficients in **A** were estimated using ridge-regularized regression.

The estimated interaction matrix was:

$$
A=
\begin{bmatrix}
-1.026 & -0.128 & -0.294 & +0.141 \\
-0.013 & -0.835 & +0.143 & -0.090 \\
-0.064 & +0.034 & -1.052 & +0.010 \\
+0.002 & -0.094 & -0.163 & -0.766
\end{bmatrix}
$$

The rows and columns follow the same order:

**Interferon–Antiviral (I), Neutrophil–Antibacterial (N), Myeloid–Inflammatory (M), Regulatory–Resolution (R).**

Each **row** describes the modeled change in one immune program, whereas each **column** represents the estimated contribution of an immune program to that change.

- **Diagonal coefficients** represent estimated self-regulation of each immune program.
- **Off-diagonal coefficients** represent estimated cross-program coupling.
- **Positive coefficients** indicate positive coupling within the fitted model.
- **Negative coefficients** indicate negative coupling within the fitted model.
- The absolute magnitude of a coefficient reflects the strength of the corresponding relationship within this fitted linear representation.

For example, the first row describes the modeled interferon state:

$$
\frac{dI}{dt}
=
-1.026I
-0.128N
-0.294M
+0.141R
$$

Within the fitted model, the interferon diagonal coefficient (**−1.026**) represents estimated negative self-regulation. The myeloid-to-interferon coefficient (**−0.294**) represents negative cross-program coupling, whereas the regulatory-to-interferon coefficient (**+0.141**) represents positive cross-program coupling.

These coefficients describe **model-derived relationships among transcriptomic immune states**. They should not be interpreted as experimentally established molecular signaling pathways or causal biological interactions.

### Why Use a Linear Model?

The underlying biological immune system is substantially more complex and may contain nonlinear, time-dependent, and context-specific interactions. The linear formulation therefore does **not** assume that human immune biology is globally linear.

Instead, the model provides an interpretable low-dimensional approximation of local relationships among the inferred transcriptomic immune states. This representation allows self-regulation, cross-program coupling, and mathematical stability to be examined within a common state-space framework.

### Stability Analysis

System stability was evaluated from the eigenvalue spectrum of the estimated interaction matrix **A**.

The estimated eigenvalues were approximately:

$$
\lambda =
\{-1.16,\,-0.97,\,-0.89,\,-0.67\}
$$

All four eigenvalues had negative real parts:

$$
\operatorname{Re}(\lambda_i)<0
\quad \text{for all } i
$$

For the estimated continuous linear ODE system, this condition indicates **asymptotic stability**. In mathematical terms, perturbations within the fitted linear system tend to decay rather than grow indefinitely.

This result refers specifically to the **mathematical stability of the estimated linear ODE system**. It should not be interpreted as evidence that the biological immune response of an individual patient is necessarily clinically stable.

### Conceptual Interpretation

The mathematical workflow can be summarized as:

**Whole-blood RNA sequencing**

↓

**Gene-level expression profiles**

↓

**Four biologically informed immune programs**

↓

**Low-dimensional immune-state vector**

$$
X=(I,N,M,R)^T
$$

↓

**Estimated interaction matrix A**

↓

**Linear ODE state-space model**

$$
\frac{dX}{dt}=AX
$$

↓

**Self-regulation + cross-program coupling + eigenvalue-based stability analysis**

This framework therefore converts high-dimensional transcriptomic information into a smaller mathematical representation that can be interpreted in terms of relationships among major immune programs.

### Important Interpretation of Time and Dynamics

GSE211567 provides **cross-sectional transcriptomic measurements**, rather than serial longitudinal measurements of the same individuals across continuous time. Consequently, the derivative \(dX/dt\) should be interpreted as a **model-derived state-space quantity**, not as a directly measured temporal change in an individual patient's immune state.

Accordingly, terms such as **interaction**, **coupling**, **dynamics**, and **stability** in this repository refer to properties inferred within the fitted mathematical state-space framework. The model is intended to characterize transcriptomic immune-state structure and its mathematical relationships rather than to reconstruct directly observed longitudinal patient-level immune kinetics.

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
