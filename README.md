# Bayesian Hierarchical Modelling of Fish Weights

A Quarto report implementing a Bayesian hierarchical Normal model on the 
[Fish Market dataset](https://www.kaggle.com/datasets/vipullrathod/fish-market) 
(Kaggle). The project was originally developed as a coursework implementation of 
a Bayesian hierarchical model and is included here as a portfolio piece 
demonstrating applied Bayesian inference in a multi-group setting.


## Live report

The interactive HTML report is available here:  
👉 https://risam0arek.github.io/fish-bayesian-hierarchical-model/

## What the project covers

- Exploratory data analysis across 7 fish species with unequal sample sizes
- Log-transformation and normality assessment (Shapiro–Wilk)
- Hierarchical model specification with semi-conjugate priors
- Half-Cauchy hyperprior on the between-group scale parameter, following [Gelman (2006)](https://sites.stat.columbia.edu/gelman/research/published/taumain.pdf)
- MCMC simulation via JAGS (3 chains, 5,000 samples each after burn-in)
- Back-transformation of lognormal parameters to the original gram scale
- Posterior analysis: group means, precisions, joint contour plots, shrinkage visualisation
- Prior and hyperparameter sensitivity checks

## Why this is relevant to catastrophe modelling and (re)insurance

Hierarchical Bayesian models are a workhorse in actuarial science and nat-cat modelling. The key mechanism — **partial pooling** across groups — is directly analogous to pooling loss data across:

- geographic zones or regions with different exposure sizes
- peril types (wind, flood, earthquake) within a single model
- lines of business with unequal claims history

Groups with sparse data borrow strength from the global distribution; data-rich groups are primarily driven by their own observations. This adaptive shrinkage is especially valuable when group sample sizes are highly unequal, which is the typical situation in practice.

## Repository structure

```
.
├── fish_bayes_hierarchical.qmd   # Main Quarto report
├── fish_bayes_hierarchical.html  # Rendered HTML report
├── Fish.csv                      # Dataset (download from Kaggle link above)
└── README.md
```

## Requirements

- R ≥ 4.2
- JAGS ≥ 4.3 (install separately: https://mcmc-jags.sourceforge.io/)
- R packages: `tidyverse`, `runjags`, `rjags`, `ggplot2`, `HDInterval`, `bayestestR`, `invgamma`, `DT`, `knitr`, `kableExtra`, `scales`, `viridis`

Install all R packages with:

```r
install.packages(c(
  "tidyverse", "runjags", "rjags", "ggplot2",
  "HDInterval", "bayestestR", "invgamma",
  "DT", "knitr", "kableExtra", "scales", "viridis"
))
```

## Rendering

Place `Fish.csv` in the same directory as the `.qmd` file, then run:

```r
quarto::quarto_render("fish_bayes_hierarchical.qmd")
```

Or from the terminal:

```bash
quarto render fish_bayes_hierarchical.qmd
```
