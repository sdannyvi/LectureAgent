# COURSE_NOTATION.md — Causal Inference Notation

## Core variables

| Concept | Default notation | Alternatives |
|---|---|---|
| Treatment | `T` | `W` in homework / some slides |
| Outcome | `Y` | — |
| Covariates/confounders | `X` | `Z` only when not used as instrument |
| Instrument | `Z` | — |
| Time | `s_0,s_1` or `t=0,t=1` | choose one per lecture |
| Group | `G` | `Group \in \{T,C\}` for DiD |
| Running variable | `W` | for RD |
| Cutoff | `c` | — |

## Potential outcomes

Binary treatment:

```latex
Y(1),\quad Y(0)
```

Observed outcome:

```latex
Y^{obs}=T Y(1)+(1-T)Y(0)
```

Individual treatment effect:

```latex
Y_i(1)-Y_i(0)
```

ATE:

```latex
ATE=E[Y(1)-Y(0)]
```

ATT:

```latex
ATT=E[Y(1)-Y(0)\mid T=1]
```

## Assumptions

SUTVA:

- no interference,
- consistency / no hidden versions of treatment.

Consistency:

```latex
T=1 \Rightarrow Y=Y(1),
\qquad
T=0 \Rightarrow Y=Y(0)
```

Unconfoundedness for ATE:

```latex
(Y(1),Y(0))\perp T\mid X
```

Weaker unconfoundedness for ATT:

```latex
Y(0)\perp T\mid X
```

Positivity:

```latex
0<P(T=1\mid X=x)<1
```

Backdoor adjustment:

```latex
P(Y\mid do(T=t))=
\sum_z P(Y\mid T=t,Z=z)P(Z=z)
```

## Propensity score

```latex
e(X)=P(T=1\mid X)
```

IPTW estimand form:

```latex
E\left[\frac{TY}{e(X)}-\frac{(1-T)Y}{1-e(X)}\right]
```

## Instrumental variables

IV assumptions:

1. relevance: `Z` affects `T`,
2. independence/as-if-random: `Z` independent of potential outcomes/confounders,
3. exclusion: `Z` affects `Y` only through `T`,
4. monotonicity: no defiers.

Wald estimator:

```latex
\tau_{Wald}=
\frac{E[Y\mid Z=1]-E[Y\mid Z=0]}
{E[T\mid Z=1]-E[T\mid Z=0]}
```

Interpretation under IV assumptions:

```latex
LATE = E[Y(1)-Y(0)\mid \text{compliers}]
```

## Difference-in-differences

Observed DiD contrast:

```latex
\widehat{\tau}_{DiD}
=
\left(E[Y\mid G=T,s_1]-E[Y\mid G=T,s_0]\right)
-
\left(E[Y\mid G=C,s_1]-E[Y\mid G=C,s_0]\right)
```

Parallel trends assumption:

```latex
E[Y_0(s_1)-Y_0(s_0)\mid G=T]
=
E[Y_0(s_1)-Y_0(s_0)\mid G=C]
```

Target:

```latex
ATT \text{ for treated group after treatment}
```

## Regression discontinuity

Sharp RD assignment:

```latex
T(W)=\mathbf{1}\{W\ge c\}
```

Local estimand:

```latex
\tau_{SRD}=E[Y(1)-Y(0)\mid W=c]
```

Estimator:

```latex
\hat\tau_{SRD}=
\lim_{w\downarrow c}E[Y\mid W=w]
-
\lim_{w\uparrow c}E[Y\mid W=w]
```

Key assumption:

```latex
\mu_t(w)=E[Y(t)\mid W=w]
\quad \text{is continuous at } c.
```

Why positivity is violated in sharp RD:

```latex
P(T=1\mid W=w)=0 \text{ for } w<c,
\qquad
P(T=1\mid W=w)=1 \text{ for } w\ge c.
```

Fuzzy RD first stage and estimand:

```latex
\tau_{FRD}=
\frac{\lim_{w\downarrow c}E[Y\mid W=w]-\lim_{w\uparrow c}E[Y\mid W=w]}
{\lim_{w\downarrow c}E[T\mid W=w]-\lim_{w\uparrow c}E[T\mid W=w]}
```

Interpretation: LATE for units at the cutoff whose treatment status is changed by crossing it.

## Heterogeneous treatment effects (CATE)

Conditional average treatment effect:

```latex
\tau(x) = E[Y(1)-Y(0)\mid X=x]
```

Relationship to ATE and ATT:

```latex
\ATE = E_X[\tau(X)],
\qquad
\ATT = E[\tau(X)\mid T=1]
```

## Causal graph discovery

Skeleton: undirected graph of conditional dependence.

CPDAG (completed partially directed acyclic graph): represents a Markov equivalence class of DAGs (output of PC / GES).

PAG (partial ancestral graph): output of FCI; allows for latent variables.

Markov condition:

```latex
X \indep \text{NonDescendants}(X) \mid \text{Parents}(X) \quad \text{in every } P \text{ faithful to } G
```

Faithfulness:

```latex
X \indep Y \mid Z \text{ in } P \implies X \indep Y \mid Z \text{ in } G
```

LiNGAM structural equation (linear, non-Gaussian):

```latex
X_j = \sum_{k \in \mathrm{pa}(j)} b_{jk} X_k + \varepsilon_j,
\qquad \varepsilon_j \text{ non-Gaussian, independent}
```

ANM (additive noise model):

```latex
Y = f(X) + \varepsilon, \qquad \varepsilon \indep X
```

Direction identified by asymmetry of residuals.

## LaTeX macros (defined in `SLIDE_TEMPLATE.tex`)

Use these macros consistently across all lectures:

| Macro | Expands to | Use for |
|---|---|---|
| `\E` | `\mathbb{E}` | expectation |
| `\Prob` | `\mathbb{P}` | probability |
| `\indep` | `\perp\!\!\!\perp` | statistical independence |
| `\ATE` | `\mathrm{ATE}` | ATE label in math mode |
| `\ATT` | `\mathrm{ATT}` | ATT label in math mode |
| `\doop` | `\mathrm{do}` | Pearl do-operator |
