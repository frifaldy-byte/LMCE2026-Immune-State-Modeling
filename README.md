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

A linear ODE state-space model was used to estimate relationships among the four immune programs.

The model can be represented as:

**dX/dt = AX**

where **X** represents the immune-state vector and **A** represents the estimated interaction matrix.

Interaction coefficients were estimated using ridge-regularized regression. System stability was subsequently evaluated from the eigenvalue spectrum of the estimated interaction matrix.

The linear formulation is intended as an interpretable approximation of local immune-state relationships and does not assume that the underlying biological immune system is globally linear.

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
