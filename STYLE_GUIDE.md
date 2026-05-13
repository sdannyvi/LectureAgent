# STYLE_GUIDE.md — Beamer and Teaching Style

## Slide design goals
Slides should be mathematically serious but easy to teach from. They should support live explanation, not replace it.

## Frame structure
Use short frames. A good frame usually has:

- one main idea,
- one equation or diagram,
- two to four short bullets,
- enough white space for live annotation.

Avoid dense textbook paragraphs.

## Recommended frame types

### 1. Story frame
Use before formal definitions.

Example title:

> Why before-after is not enough

Content:

- outcome changed after treatment,
- but maybe it would have changed anyway,
- need a control group.

### 2. Formal frame
Introduce notation and estimand.

Example:

```latex
\[
ATT = E[Y(1)-Y(0)\mid T=1]
\]
```

### 3. Identification frame
State assumption + formula.

Example:

```latex
\[
(Y(1),Y(0))\perp T\mid X
\]

\[
ATE=E_X\left[E[Y\mid T=1,X]-E[Y\mid T=0,X]\right]
\]
```

### 4. Pitfall frame
Explain a common wrong move.

Example:

> Wrong: condition on everything.

Then show collider or mediator problem.

### 5. Recap frame
Use at the end of each section.

## Beamer conventions
Use simple Beamer themes unless instructed otherwise.

Recommended packages:

```latex
\usepackage{amsmath,amssymb,bm}
\usepackage{tikz}
\usetikzlibrary{arrows.meta,positioning,calc,decorations.pathreplacing}
\usepackage{booktabs}
```

## TikZ DAG style
Use consistent node styling (matches `SLIDE_TEMPLATE.tex` exactly):

```latex
\tikzset{
  var/.style={circle, draw, thick, minimum size=8mm, align=center},
  obs/.style={circle, draw, thick, fill=blue!8, minimum size=8mm, align=center},
  treat/.style={circle, draw, thick, fill=blue!15, minimum size=8mm, align=center},
  out/.style={circle, draw, thick, fill=orange!20, minimum size=8mm, align=center},
  conf/.style={circle, draw, thick, fill=purple!12, minimum size=8mm, align=center},
  hidden/.style={circle, draw, dashed, thick, fill=gray!10, minimum size=8mm, align=center},
  arrow/.style={-Latex, thick},
  badpath/.style={-Latex, thick, red!70},
  note/.style={rectangle, rounded corners, draw, fill=yellow!12, align=left},
}
```

Node style semantics:

| Style | Colour | Use for |
|---|---|---|
| `treat` | blue!15 | treatment node `T` |
| `out` | orange!20 | outcome node `Y` |
| `conf` | purple!12 | observed confounder/covariate `X` |
| `obs` | blue!8 | generic observed variable |
| `hidden` | dashed gray!10 | unobserved / latent variable |
| `note` | yellow!12 | annotation box beside a diagram |
| `arrow` | thick | causal edge |
| `badpath` | red!70 | backdoor / problematic path |

## LaTeX macros (defined in `SLIDE_TEMPLATE.tex`)
Always use these macros instead of raw LaTeX:

| Macro | Expands to | Use for |
|---|---|---|
| `\E` | `\mathbb{E}` | expectation |
| `\Prob` | `\mathbb{P}` | probability |
| `\indep` | `\perp\!\!\!\perp` | statistical independence |
| `\ATE` | `\mathrm{ATE}` | ATE label in math |
| `\ATT` | `\mathrm{ATT}` | ATT label in math |
| `\doop` | `\mathrm{do}` | Pearl do-operator |

Example usage:

```latex
\E[Y(1)-Y(0)] = \ATE
\quad (Y(1),Y(0)) \indep T \mid X
\quad \Prob(T=1\mid X=x) > 0
\quad P(Y\mid \doop(T=t))
```

## Notation style
Prefer one notation style per lecture.

- If using `T`, do not switch to `W` unless necessary.
- If using `Y(1),Y(0)`, do not switch to `Y_1,Y_0` mid-lecture.
- If using time in DiD, use `s_0, s_1` or `t=0,t=1`, but not both.

## Progressive reveal
For fake animation in PDF slides, use repeated frames or Beamer overlays. Repeated frames are safer for PDF presentation on iPad/Notability.

Example repeated frame approach:

```latex
\begin{frame}{Building the adjustment formula}
\[
E[Y(1)-Y(0)]
\]
\end{frame}

\begin{frame}{Building the adjustment formula}
\[
E_X\{E[Y(1)-Y(0)\mid X]\}
\]
\end{frame}
```

## Language style
Use direct, plain English:

- “We observe this.”
- “This is the missing counterfactual.”
- “This equality uses consistency.”
- “This equality uses unconfoundedness.”
- “This is an identification statement, not an estimator.”

Avoid vague wording:

- “The model controls for everything.”
- “The effect is proven.”
- “The graph gives the truth.”

## Equations
When deriving formulas, label the reason for key steps:

```latex
\[
E[Y(1)\mid X]
= E[Y(1)\mid T=1,X]
\quad \text{(unconfoundedness)}
\]

\[
= E[Y\mid T=1,X]
\quad \text{(consistency)}
\]
```

## Tables
Use small tables only. For computations, use 2–4 rows when possible.

## Humor / visuals
Light humor is welcome when it clarifies concepts:

- collider as “two suspects explaining the same alarm,”
- backdoor as “a thief sneaking through a back entrance,”
- DiD as “training + protein vs training only.”

Do not let visuals replace the formal definition.
