# LECTURE_WORKFLOW.md — Agentic Workflow for Preparing Beamer Lectures

## Goal
Use an agentic coding assistant to prepare high-quality Beamer slides for causal inference lectures.

## Recommended workflow

### Step 1: Start with a lecture brief
Create or provide a short brief:

```text
Topic:
Audience level:
Lecture length:
Previous lecture:
Next lecture:
Must-cover concepts:
Examples to use:
Common misconceptions to target:
Desired output filename:
```

### Step 2: Ask for a slide outline first
Before generating full LaTeX, ask the agent for:

- lecture goal,
- section breakdown,
- slide titles,
- key equations,
- planned examples,
- where diagrams are needed.

### Step 3: Generate Beamer code
Ask for a compilable `.tex` file using `SLIDE_TEMPLATE.tex` conventions.

### Step 4: Compile and inspect
Compile with:

```bash
latexmk -pdf lecture_file.tex
```

or:

```bash
pdflatex lecture_file.tex
pdflatex lecture_file.tex
```

### Step 5: Pedagogical review
Ask the agent to review:

- Is the order teachable?
- Are assumptions stated before use?
- Are equations too dense?
- Are examples concrete?
- Are there common mistakes included?
- Are there slides suitable for live annotation?

### Step 6: Export and present
For iPad/Notability workflows, export as PDF. If using fake animations, prefer repeated frames rather than complex Beamer overlay behavior.

## Prompt template for a new lecture

```text
Use CLAUDE.md, STYLE_GUIDE.md, COURSE_NOTATION.md, and SLIDE_TEMPLATE.tex.
Prepare Beamer slides for the next lecture on [TOPIC].

Audience: undergraduate/graduate students in Causal Inference in the AI Era.
Length: [X] minutes.
Previous lecture covered: [PREVIOUS].
Next lecture will cover: [NEXT].

Main goals:
1. ...
2. ...
3. ...

Use a slow teaching style: intuition, example, notation, identification formula, common mistake, recap.

First give a slide-by-slide outline. Then generate compilable LaTeX Beamer code.
```

## Prompt template for improving existing slides

```text
Review this Beamer lecture for causal-inference correctness and teachability.

Check:
- Are estimand, assumptions, and estimator separated?
- Are potential outcomes and observed outcomes not confused?
- Are conditioning sets valid?
- Are colliders/mediators not adjusted for incorrectly?
- Are equations introduced slowly enough?
- Are slides too dense?

Then propose edits. Do not rewrite the whole file unless necessary.
```

## Prompt template for adding fake animations

```text
Convert this frame into a sequence of 3–5 repeated Beamer frames suitable for PDF presentation on iPad/Notability. Each frame should add one conceptual step. Avoid overlay-only commands if they make the PDF harder to present.
```

## Prompt template for generating diagrams

```text
Create a simple TikZ DAG for the following story: [STORY].
Use the TikZ styles from SLIDE_TEMPLATE.tex.
Make treatment blue, outcome orange, confounders purple, hidden variables dashed gray.
```

## Prompt template for turning a paper into slides

Use when asked to create a lecture or discussion slot based on a reading from `readings/`.

```text
Read readings/READINGS_INDEX.md to find the entry for [PAPER FILENAME].
Then read the paper itself.

Create Beamer slides for a [X]-minute paper discussion slot in Module [N].

Structure the slides in two parts.

### Part 1 — Understanding the paper (roughly 2/3 of slides)

1. "Motivation" frame: what problem does the paper solve and why should a causal inference
   student care? State the gap the paper fills in one sentence.
2. Cover only the concepts a student needs to understand the paper's contribution —
   do not reproduce the full paper.
3. Use course notation from COURSE_NOTATION.md (T, Y, X, e(X), CATE, \indep, etc.).
4. One frame that explicitly connects the paper back to course fundamentals:
   which assumptions from the course does this paper rely on, relax, or reframe?
   (e.g. positivity, unconfoundedness, SUTVA, consistency.)
5. One "common mistake or misconception" frame relevant to the paper's method.

### Part 2 — Critical evaluation (roughly 1/3 of slides)

6. "Assumptions the paper makes" frame: list every causal assumption the paper relies on
   (unconfoundedness, positivity, SUTVA, correct model specification, etc.) and state
   explicitly whether the paper tests or justifies each one.
7. "What the paper does not address" frame: pick 2–3 honest limitations from this list
   and state them clearly:
   - hidden confounding / unconfoundedness not tested on real data,
   - sensitivity analysis absent or limited,
   - experiments on semi-synthetic benchmarks only (IHDP, ACIC, CEMNIST) —
     ground truth CATE is never observable in real-world data,
   - positivity violations detected but unconfoundedness still assumed,
   - the model may flag uncertainty correctly yet still be biased if confounding is present.
8. "How does this compare to classical methods?" frame: contrast the paper's approach
   with at least one classical causal inference method covered in the course
   (e.g. IPTW trimming, Rosenbaum sensitivity bounds, matching).
   Which problems does the paper solve better? Which does it not solve at all?
9. "Discussion questions" frame: 3–5 pointed questions suitable for live class discussion.
   Questions should require students to reason about assumptions, not just recall facts.
   Examples of good question types:
   - "The paper assumes unconfoundedness throughout. What would need to change if there
     were hidden confounders?"
   - "The benchmarks use semi-synthetic data. Can you trust the PEHE metric on real data?
     Why or why not?"
   - "When would you prefer propensity trimming over uncertainty-based rejection?"
   - "Is epistemic uncertainty about CATE the same as uncertainty about the causal effect?
     What is missing?"
10. Final "Take-away" frame: one key equation from the paper in course notation + two
    bullets: what the paper contributes and what remains open.

Do not include proofs or derivations unless they are pedagogically essential.
Use SLIDE_TEMPLATE.tex conventions throughout.
Save output to lectures/lecNN_paper_shortname.tex.
```

## Quality checklist before accepting a lecture

- [ ] Compiles without errors.
- [ ] No frame is too dense.
- [ ] Every causal formula has its assumption nearby.
- [ ] Estimand vs estimator are separated.
- [ ] At least one example is concrete.
- [ ] At least one common mistake is included.
- [ ] TikZ graphs are readable.
- [ ] The final recap is useful.

### Additional checklist for paper-based slides

- [ ] Every assumption the paper makes is listed and labelled (tested / untested).
- [ ] At least one limitation about real-world data or unconfoundedness is stated explicitly.
- [ ] The paper is compared to at least one classical method from the course.
- [ ] Discussion questions require causal reasoning, not just paper recall.
- [ ] No slide oversells the paper's conclusions beyond what identification justifies.
