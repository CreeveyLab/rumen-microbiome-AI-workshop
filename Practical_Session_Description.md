# Practical Session Description
## "From Microbiomes to Predictions: Genomics and AI in Animal Science"

**Contribution to:** Animal Science Module, AI for Animal & Food Science (postgraduate)
**Prepared by:** Prof Chris Creevey, Queen's University Belfast
**Session type:** Computer-based practical (hands-on, self-paced within a guided structure)
**Delivery platform:** Google Colab notebook (`rumen_microbiome_AI_workshop.ipynb`) — browser-based, no installation, no coding required of students
**Duration:** 60 minutes core practical, extensible to 90 minutes with full use of the open-ended exploration section
**Prerequisite:** A 1-hour lecture (see below), delivered immediately before this session

---

## 1. Overview

This practical is the applied, hands-on counterpart to a preceding lecture on rumen microbiology and methane emissions. Where the lecture establishes the biological context, this session lets students *work directly* with a realistic (synthetic) dataset to see how that biology becomes something a computer can learn from — from raw DNA sequence, through numerical representation, to a trained predictive model and an explanation of its reasoning.

Students run a single Google Colab notebook that tells one continuous story: *"We have microbiome samples from ruminant animals — some low methane emitters, some high. Can genomic data from their gut microbiomes predict which is which, and can we explain why?"* No prior coding, Linux, or bioinformatics experience is assumed. Code cells run at the press of a button; the pedagogical content is in the narrative text, the visual outputs, and the discussion questions between them.

The notebook is intentionally structured to resist being rushed: content is revealed progressively as students run each cell (nothing downstream is visible until the relevant cell has been executed), and results, discussion prompts, and a substantial open-ended "try it yourself" section are designed to fill the full session rather than being skimmable in a few minutes.

---

## 2. Assumed Prerequisite Lecture (1 hour)

This practical assumes students arrive having just received a lecture covering the **biological background only** — none of the computational or statistical concepts are assumed; those are taught within the practical itself. The lecture should cover:

- **Ruminant digestion and the rumen** as an anaerobic fermentation chamber, and why ruminants rely on a resident microbial community to digest plant fibre
- **The rumen microbiome**: its major functional groups — fibre-degrading bacteria (e.g. *Fibrobacter*, *Ruminococcus*, *Butyrivibrio*), generalist fermenters (e.g. *Prevotella*), and methanogenic archaea (e.g. *Methanobrevibacter*, *Methanomassiliicoccus*)
- **Methanogenesis**: the basic biochemistry of hydrogen scavenging and interspecies hydrogen transfer that leads to methane production, and why some microbial community compositions favour more or less methane output
- **Why this matters**: methane's potency as a greenhouse gas, livestock's contribution to agricultural emissions, and the practical relevance of identifying low-emitting animals for breeding or management
- **The microbiome as a community property**: that host phenotypes (like methane output) can plausibly be linked to *which* microbes are present and in what proportions, not just host genetics alone

The lecture should stop short of introducing DNA sequencing data formats, k-mers, or any machine learning concepts — the practical builds these up from first principles, deliberately connecting back to the biology just covered.

---

## 3. Learning Objectives

By the end of this practical, students should be able to:

1. **Explain** how a microbial community's DNA can be converted into a numerical representation, from raw sequence through k-mer counting to a compressed "genomic embedding" vector
2. **Describe** how genomic profiles can be compared mathematically (e.g. via similarity of k-mer frequency vectors) to identify or match microbial samples, and relate this to real-world metagenomic classification tools
3. **Interpret** a PCA plot as a way of visualising high-dimensional biological data in two dimensions, and articulate what such a plot can and cannot tell you about the underlying biology
4. **Explain**, in outline, how a Random Forest classifier learns to predict a phenotype from many input features, and **interpret** standard evaluation outputs — accuracy, a confusion matrix, precision, and recall
5. **Critically evaluate** classifier performance, including the practical consequences of false positives versus false negatives, and how adjusting a decision threshold trades one against the other
6. **Use feature importance** to identify which biological signals a model relies on most, and **distinguish** a model's predictive power from a causal biological claim
7. **Reflect** on the limitations of this kind of analysis in real research — small sample sizes, generalisability across breeds/diets/environments, batch effects, and the compositional nature of microbiome data
8. **Investigate**, through guided experimentation, how methodological choices — training set size, model complexity, classification threshold, choice of visualised dimensions — change the outcome of an analysis, building intuition for why a single reported number (e.g. "87% accuracy") is not the whole story

---

## 4. Session Structure

The notebook is organised into seven sections, released progressively as students work through it:

| Section | Content | Approx. time |
|---|---|---|
| **1. The Biology — What Are We Looking At?** | Recaps the biological question; introduces k-mers and genomic embeddings from scratch with an interactive sliding-window animation; demonstrates matching an unknown sequence to reference genomes by k-mer profile similarity; shows an actual genomic embedding as a vector of numbers; explores microbial community diversity and raw data | ~15 min |
| **2. Visualising the Data** | PCA reduces 30 genomic features to 2 dimensions; students assess whether phenotype groups separate, and which features drive the separation | ~7 min |
| **3. Training a Classifier** | Trains a Random Forest on 80% of samples, evaluates on the held-out 20%; confusion matrix, precision/recall; examines where the model gets it wrong; a re-runnable "bonus" cell shows how much a single random train/test split affects the reported accuracy | ~10 min |
| **4. Explainability** | Feature importance ranks which genomic signals the model relied on; individual predictions are explained sample-by-sample | ~8 min |
| **5. What This Means — and What It Doesn't** | A reflective landing section on the limits of the analysis: prediction vs causation, generalisability, real-world data challenges | ~3 min |
| **6. Summary and Key Concepts** | Recap of the five core concepts covered, with further reading | ~2 min |
| **7. Explore the Data — Try It Yourself** | Seven self-contained, editable exercises revisiting each part of the notebook (k-mer length, GC content and genome matching, single-feature inspection, PCA component choice, classifier hyperparameters, decision threshold, explaining individual — including misclassified — samples) | ~15–25 min, expandable |

Each guided step (Sections 1–4) follows the same pattern: a short explanation of the biological or statistical reasoning, a stated expectation of what the output should show, the code cell itself (run, not written, by students), and — where appropriate — an open discussion question with no single correct answer.

---

## 5. Facilitation Notes

- **Pairs or small groups** are recommended over solo working — the discussion questions are designed to be talked through, and Section 7's exercises invite comparing results across groups (e.g. different random splits will genuinely disagree on exact accuracy, which is itself a teaching point).
- The facilitator's main role during Sections 1–4 is to **circulate and prompt discussion** at the marked questions rather than to explain code — students are explicitly told they do not need to understand or modify it.
- During **Section 7**, the facilitator's role shifts to **coaching exploration**: encouraging students to form a hypothesis before changing a variable ("what do you think will happen if...?"), rather than just changing values and observing.
- Groups that move quickly through Sections 1–6 should be directed to spend the remaining time in Section 7 rather than finishing early — the session is designed so that genuine engagement with the exploration exercises fills the full hour.
- No student output needs to be collected for this session to be effective, but Section 7 could double as the basis for a short follow-up discussion or a brief written reflection if the module requires an assessed component.

---

## 6. Technical Requirements

- A Google account (to open and run the notebook in Google Colab) and a web browser
- No local software installation, no coding experience, and no prior use of Jupyter/Colab required
- The notebook is fully self-contained: all data is synthetic and generated within the notebook itself using a fixed random seed, so — aside from the deliberately non-deterministic "bonus" and exploration cells — results are reproducible across runs and across students
- Total automated runtime (`Runtime > Run all`) is under one minute on a free Colab CPU instance

---

## 7. Link to Wider Research Context

The practical closes by connecting explicitly back to real research: the same question posed in the exercise — using explainable AI to identify which microbial drivers of a host phenotype are genuinely robust, rather than artefacts of a single study or dataset — is presented as the kind of question motivating current PhD research in this space (e.g. James Barnard's work). This is intended to give students a concrete sense of how the skills practised in this one-hour session scale up into ongoing research questions in the department.
