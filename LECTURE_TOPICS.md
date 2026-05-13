# LECTURE_TOPICS.md — Suggested Lecture Modules

## Module 1: Potential outcomes and randomized experiments
Main concepts:

- potential outcomes,
- observed outcome formula,
- SUTVA,
- ATE/ATT,
- randomization.

Key misconception:

- “We can observe both outcomes for a person.”

## Module 2: Observational studies and adjustment
Main concepts:

- confounding,
- unconfoundedness,
- positivity,
- regression adjustment,
- adjustment formula.

Key misconception:

- “Regression automatically makes estimates causal.”

## Module 3: Propensity scores
Main concepts:

- propensity score definition,
- balancing score intuition,
- matching,
- stratification,
- IPTW.

Key misconception:

- “The propensity score predicts the outcome.”

## Module 4: Sensitivity analysis
Main concepts:

- hidden confounding,
- random common cause refuter,
- data subset refuter,
- unobserved confounder strength,
- Rosenbaum-style sensitivity.

Key misconception:

- “Passing a refuter proves there is no hidden confounding.”

## Module 5: Instrumental variables
Main concepts:

- instrument,
- relevance,
- independence,
- exclusion,
- monotonicity,
- Wald estimator,
- LATE/compliers.

Key misconception:

- “IV always gives ATE.”

## Module 6: Pearl DAGs and backdoor criterion
Main concepts:

- DAGs,
- SCMs,
- do-operator,
- d-separation,
- confounders,
- colliders,
- mediators,
- backdoor adjustment.

Key misconception:

- “Condition on every variable.”

## Module 7: Causal graph discovery
Main concepts:

- path analysis vs graph discovery,
- Markov condition,
- faithfulness,
- skeleton and v-structures,
- PC algorithm,
- FCI (latent variables), GES (score-based),
- Markov equivalence classes and CPDAGs,
- LiNGAM (linear non-Gaussian models),
- ANM (additive noise models, non-linear).

Key misconception:

- “The algorithm discovers the true graph from observational data alone.”

## Module 8: Difference-in-differences
Main concepts:

- treatment/control group,
- before/after,
- ATT target,
- missing counterfactual trend,
- parallel trends.

Key misconception:

- “Before-after difference is the treatment effect.”

## Module 9: Regression discontinuity
Main concepts:

- running variable,
- cutoff,
- sharp RD: deterministic assignment at cutoff,
- fuzzy RD: jump in probability at cutoff (IV analog),
- positivity violation in sharp RD,
- continuity assumption,
- local effect at cutoff,
- bandwidth selection and local polynomial regression.

Key misconceptions:

- “RD estimates a global ATE.”
- “Fuzzy RD is just sharp RD with noise — they target the same estimand.”

## Module 10: Causal inference meets machine learning
Main concepts:

- heterogeneous treatment effects (CATE) and when they matter,
- neural CATE estimators: T-Learner, TARNet, CFRNet/CFR-MMD, Dragonnet, CEVAE,
- double ML / debiased ML: Neyman orthogonality and cross-fitting,
- causal forests and honest estimation,
- ML-based propensity score and outcome models,
- epistemic vs. aleatoric uncertainty in CATE,
- non-overlap as a covariate shift problem: when p(t=1|x)≈0 means μ₁(x) is OoD,
- MC Dropout as approximate Bayesian inference for causal models,
- rejection policies: uncertainty-based vs. propensity score trimming,
- targeted learning (TMLE) at a conceptual level,
- causal representation learning: when does a latent model support do-calculus?

Key readings:

- Jesson et al., NeurIPS 2020 — `readings/jesson2020_uncertainty_aware_cate.pdf`

Key misconceptions:

- “A better ML model means a better causal estimate.”
- “Causal forests give ATE, not LATE or local effects.”
- “Propensity score trimming is always a safe way to handle non-overlap.”

## Module 11: Putting it together
Main concepts:

- choose estimand (ATE, ATT, LATE, CATE, local RD effect, DiD ATT),
- choose identification strategy (randomization, unconfoundedness, IV, parallel trends, continuity),
- check assumptions (overlap, exclusion, parallel trends, continuity),
- choose estimator (regression, matching, IPTW, Wald, DiD regression, local polynomial),
- report limitations and sensitivity.

Key misconception:

- “A causal method is a black box.”
