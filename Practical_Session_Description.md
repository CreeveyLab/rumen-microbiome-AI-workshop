# Session Overview
## Rumen Microbiomes, Methane, and Predictive AI

**Contribution to:** Animal Science Module, AI for Animal & Food Science (postgraduate)
**Delivered by:** Prof Chris Creevey, Queen's University Belfast
**Format:** A 1-hour lecture followed immediately by a 1-hour computer-based practical
**Practical platform:** Google Colab notebook (`rumen_microbiome_AI_workshop.ipynb`) — browser-based, no installation, no coding required of students

---

## 1. Lecture: The Rumen Microbiome — Biology, Function, and Management (1 hour)

This lecture introduces the biology underpinning the practical that follows. It covers:

- **Ruminant digestion and the rumen**: the four-chambered stomach as an anaerobic fermentation system, with the rumen itself as the primary fermentation chamber; a brief comparative note on other foregut-fermenting animals (e.g. the hoatzin, colobine monkeys) as examples of convergent evolution
- **The rumen microbiome**: its scale and composition — each millilitre of rumen content holds roughly 10–50 billion bacteria and archaea, around a million protozoa, and variable numbers of yeasts and fungi — illustrated with micrographs of the microbial community attached to plant fibre
- **Rumen function**: how microbial fermentation converts dietary sugars into volatile fatty acids (acetate, propionate, butyrate) that the host absorbs and uses for meat, milk, and wool production, and how methanogenesis runs alongside this process, with methane ultimately released via eructation
- **Why this matters**: livestock agriculture's contribution to global greenhouse gas emissions (FAO estimates ~18%, mainly as methane), international climate commitments (the Paris Agreement, the US–EU methane pledge, Northern Ireland's 46% reduction target), and the resulting drive to find ways of lowering ruminant methane output
- **How the microbiome is studied**: the distinction between genomics (sequencing an isolated, cultured organism), meta-taxonomics (amplicon sequencing of a marker gene such as 16S rRNA), metagenomics (sequencing all DNA in a community sample), and meta-transcriptomics (sequencing expressed mRNA) — and what each approach can and cannot tell us
- **What is already known about the rumen microbiome globally**: findings from the Global Rumen Census (a core microbiome recognisable across host species and geography) and the Hungate1000 genome collection (over 400 sequenced rumen bacterial and archaeal genomes)
- **Managing the rumen microbiome**: two broad strategies — breeding low-methane-emitting animals (host genetics and rumen microbiome composition are linked) and dietary/feed additive interventions (legumes, oils, nitrate, seaweed and microalgae, and commercial products such as Bovaer®, Mootral, and Agolin Ruminant)
- **Case study — Bovaer®**: the mechanism of action (3-nitrooxypropanol inhibiting methyl-coenzyme M reductase, the enzyme catalysing the final step of methanogenesis), and the public controversy that followed its introduction, used as a short case study in the gap between scientific mechanism and public communication
- **An open question to close the lecture**: could the rumen microbiome be shifted into a stable, low-methane state that persists without ongoing additives? This question is left open deliberately — it motivates the shift, in the practical that follows, from *describing* the microbiome to *predicting* a host phenotype from it computationally

---

## 2. Practical: From Microbiomes to Predictions — Genomics and AI in Animal Science (1 hour)

Where the lecture establishes the biology, this practical lets students work directly with a realistic (synthetic) dataset to see how that biology becomes something a computer can learn from — from raw DNA sequence, through numerical representation, to a trained predictive model and an explanation of its reasoning.

Students run a single Google Colab notebook that tells one continuous story: *"We have microbiome samples from ruminant animals — some low methane emitters, some high. Can genomic data from their gut microbiomes predict which is which, and can we explain why?"* No prior coding, Linux, or bioinformatics experience is required. Code cells run at the press of a button; the pedagogical content is in the narrative text, the visual outputs, and the discussion questions between them.

The notebook is structured to resist being rushed: content is revealed progressively as students run each cell (nothing downstream is visible until the relevant cell has been executed), and results, discussion prompts, and a substantial open-ended "try it yourself" section are designed to fill the full session rather than being skimmable in a few minutes.

### Session structure

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

### Technical requirements

- A Google account (to open and run the notebook in Google Colab) and a web browser
- No local software installation, no coding experience, and no prior use of Jupyter/Colab required
- The notebook is fully self-contained: all data is synthetic and generated within the notebook itself using a fixed random seed, so — aside from the deliberately non-deterministic "bonus" and exploration cells — results are reproducible across runs and across students
- Total automated runtime (`Runtime > Run all`) is under one minute on a free Colab CPU instance

### Link to wider research context

The practical closes by connecting explicitly back to real research: the same question posed in the exercise — using explainable AI to identify which microbial drivers of a host phenotype are genuinely robust, rather than artefacts of a single study or dataset — is presented as the kind of question motivating current PhD research in this space (e.g. James Barnard's work), giving students a concrete sense of how the skills practised in this session scale up into ongoing research questions in the department.

---

## 3. Learning Objectives

By the end of the lecture and practical together, students should be able to:

**Biology (lecture)**
1. **Describe** the anatomy of ruminant digestion and the role of the rumen as an anaerobic fermentation chamber
2. **Explain** the major functional groups of the rumen microbiome (fibre-degrading bacteria, generalist fermenters, methanogenic archaea) and their role in fermentation and methanogenesis
3. **Explain** why ruminant methane emissions matter environmentally and the main strategies (breeding, dietary/feed additives) being pursued to reduce them
4. **Distinguish** between genomics, meta-taxonomics, metagenomics, and meta-transcriptomics as approaches to studying a microbial community

**Computation and AI (practical)**
5. **Explain** how a microbial community's DNA can be converted into a numerical representation, from raw sequence through k-mer counting to a compressed "genomic embedding" vector
6. **Describe** how genomic profiles can be compared mathematically (e.g. via similarity of k-mer frequency vectors) to identify or match microbial samples, and relate this to real-world metagenomic classification tools
7. **Interpret** a PCA plot as a way of visualising high-dimensional biological data in two dimensions, and articulate what such a plot can and cannot tell you about the underlying biology
8. **Explain**, in outline, how a Random Forest classifier learns to predict a phenotype from many input features, and **interpret** standard evaluation outputs — accuracy, a confusion matrix, precision, and recall
9. **Critically evaluate** classifier performance, including the practical consequences of false positives versus false negatives, and how adjusting a decision threshold trades one against the other
10. **Use feature importance** to identify which biological signals a model relies on most, and **distinguish** a model's predictive power from a causal biological claim
11. **Reflect** on the limitations of this kind of analysis in real research — small sample sizes, generalisability across breeds/diets/environments, batch effects, and the compositional nature of microbiome data
12. **Investigate**, through guided experimentation, how methodological choices — training set size, model complexity, classification threshold, choice of visualised dimensions — change the outcome of an analysis, building intuition for why a single reported number (e.g. "87% accuracy") is not the whole story

---

## 4. Facilitation Notes

- **Pairs or small groups** are recommended for the practical over solo working — the discussion questions are designed to be talked through, and Section 7's exercises invite comparing results across groups (e.g. different random splits will genuinely disagree on exact accuracy, which is itself a teaching point).
- The facilitator's main role during Sections 1–4 of the practical is to **circulate and prompt discussion** at the marked questions rather than to explain code — students are explicitly told they do not need to understand or modify it.
- During **Section 7**, the facilitator's role shifts to **coaching exploration**: encouraging students to form a hypothesis before changing a variable ("what do you think will happen if...?"), rather than just changing values and observing.
- Groups that move quickly through Sections 1–6 should be directed to spend the remaining time in Section 7 rather than finishing early — the practical is designed so that genuine engagement with the exploration exercises fills the full hour.
- No student output needs to be collected for the session to be effective, but Section 7 could double as the basis for a short follow-up discussion or a brief written reflection if the module requires an assessed component.
