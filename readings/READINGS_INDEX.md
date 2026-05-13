# READINGS_INDEX.md — Papers and Readings by Module

Each entry lists: filename, citation, module, and the key concepts it covers for slide generation.

---

## Module 10: Causal inference meets machine learning

### jesson2020_uncertainty_aware_cate.pdf
**Citation:** Jesson, Mindermann, Shalit, Gal. "Identifying Causal-Effect Inference Failure with Uncertainty-Aware Models." NeurIPS 2020.

**Key concepts:**
- CATE estimation with neural networks (TARNet, CFRNet/CFR-MMD, Dragonnet, CEVAE)
- Epistemic vs. aleatoric uncertainty in CATE
- MC Dropout as approximate Bayesian inference for causal models
- Non-overlap reframed as covariate shift: when `p(t=1|x) ≈ 0`, estimating `μ₁(x)` is OoD
- Negative sampling for non-overlap in CEVAE
- Rejection policies: epistemic uncertainty vs. propensity score trimming
- Benchmarks: IHDP, ACIC 2016, CEMNIST (new, high-dimensional)
- Main result: uncertainty-based rejection outperforms propensity trimming, especially in high dimensions

**Slide angle for this course:**
Use to motivate why positivity/overlap is not just a theoretical assumption but a practical ML failure mode, and how uncertainty quantification bridges causal inference and modern deep learning.
