# Bayesian Multi-method Occupancy Model for Oriental Pied Hornbill (OPHB)

This repository contains R and JAGS code for fitting a **Bayesian multi-method occupancy model** to estimate species occupancy, availability, and detection probabilities. The example use case focuses on the **Oriental Pied Hornbill (Anthracoceros albirostris), integrating multiple survey methods such as passive acoustic monitoring (PAM), human observations, and BirdNET.

---

##Overview

This model separates the detection process into three stages:

- **Occupancy (ψ)**: The probability that a site is occupied by the species.
- **Availability (θ)**: The probability that the species is available (e.g., vocalizing) during a survey visit, conditional on occupancy.
- **Detection (p)**: Method-specific detection probabilities, given that the species is available.

The model is implemented in [JAGS](http://mcmc-jags.sourceforge.net/) and run through R using the `jagsUI` package.

---

##Repository Contents

| File | Description |
|------|-------------|
| `multi_method_model.R` | Main R script to prepare data and run the JAGS model |
| `model.txt` | JAGS model specification (automatically written from R) |
| `example_data.csv` | Example detection history dataset (user-provided) |
| `README.md` | Project documentation |

---

##Model Structure

```text
z[s] ~ dbern(psi)                    # True occupancy state
w[s, j] ~ dbern(theta * z[s])       # Availability during visit j
DH[s, m, j] ~ dbern(p[m] * w[s, j]) # Observed detection by method m
