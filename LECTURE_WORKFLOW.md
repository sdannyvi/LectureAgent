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

The slides should:
1. Start with one "motivation" frame: what problem does the paper solve and why should a
   causal inference student care?
2. Cover only the concepts a student needs to understand the paper's contribution —
   do not reproduce the full paper.
3. Use the course notation from COURSE_NOTATION.md (e.g. T, Y, X, e(X), CATE).
4. Include one frame that connects the paper back to course fundamentals
   (e.g. how positivity appears here, how this relates to the adjustment formula).
5. Include one "common mistake or misconception" frame relevant to the paper.
6. End with a "take-away" recap frame: one equation + two bullets.

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
