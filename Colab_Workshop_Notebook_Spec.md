# Specification: Interactive Google Colab Workshop Notebook
## "From Microbiomes to Predictions: Genomics and AI in Animal Science"

**Prepared for:** Claude Code  
**Purpose:** Build a self-contained, interactive Google Colab notebook for use as a taught workshop session with students who have no prior bioinformatics, Linux, or coding experience.

---

## 1. Overview and Goal

Build a single `.ipynb` Jupyter notebook that runs on Google Colab without modification. The notebook tells a complete biological story — from raw genomic representations of microbial community samples through to an AI-based prediction of a host phenotype, with explainability — using pre-generated synthetic data embedded directly in the notebook.

The student experience is: open the notebook in Colab, run cells sequentially (or "Run all"), read the narrative, look at the outputs, and answer guided discussion questions. No coding, no installation, no data upload required.

---

## 2. Target Audience

- Primarily computer science background students at the start of a postgraduate programme in AI for animal/food science
- Some students from biology backgrounds with no computational training
- No assumed knowledge of: Linux, Python, bioinformatics tools, or microbiology
- CS students will be comfortable with the idea of a notebook but should not need to read or understand the code
- Biology students should be able to follow the biological narrative without engaging with the code

The notebook must work for both groups simultaneously. Biological concepts are explained in plain language. Code cells are collapsed or clearly marked as "run this cell" with no expectation of understanding the code itself.

---

## 3. Technical Constraints (Critical)

- **Single file**: one `.ipynb` file, no external data files, no companion scripts
- **Zero pip installs**: use only libraries pre-installed in Google Colab's standard environment. Permitted libraries: `numpy`, `pandas`, `matplotlib`, `seaborn`, `scikit-learn`, `scipy`. Do not use `umap-learn`, `torch`, `tensorflow`, or any other library requiring `!pip install`
- **Self-contained data**: all data is generated programmatically within the notebook using `numpy` with a fixed random seed, so results are identical every time
- **No user input required**: all cells run to completion without user interaction
- **Colab-compatible**: no local file system dependencies; no widgets requiring ipywidgets installation beyond what Colab provides
- **Runtime**: full notebook should run to completion in under 3 minutes on a free Colab CPU instance
- **Reproducibility**: set `numpy.random.seed(42)` at the top; all stochastic steps must use this seed

---

## 4. Narrative Arc and Pedagogical Goals

The notebook follows a single research question from start to finish:

> **"We have microbiome samples from ruminant animals. Some animals are low methane emitters, some are high. Can we use genomic data from their gut microbiomes to predict which is which — and can we explain why?"**

### Pedagogical goals (in order):

1. Introduce the idea that microbial communities can be represented as numbers (genomic embeddings / k-mer frequency vectors) — bridge from biology to data
2. Show that biological similarity is visible in data space (visualisation of embeddings)
3. Show that a machine learning model can learn to classify samples by phenotype from this data
4. Show that the model's decisions can be explained biologically (explainability / feature importance)
5. Prompt critical thinking about what the model can and cannot tell us

Each section should end with 1–2 **"Discussion Questions"** rendered as formatted markdown that students discuss with a neighbour or the group. These should not have single correct answers — they should prompt genuine reflection.

---

## 5. Synthetic Data Specification

Generate a synthetic dataset that is biologically realistic in structure, even though it is simulated. The data represents rumen microbiome samples characterised by k-mer frequency profiles, reduced to a set of named "genomic features" that correspond to biologically plausible microbial signals.

### Dataset parameters:
- **N = 120 samples** (80 training, 40 test — split within the notebook)
- **M = 30 features** representing named genomic embedding dimensions
- **Binary phenotype label**: `low_emitter` (0) or `high_emitter` (1), approximately 60/40 split
- **Continuous phenotype**: methane emissions value in g/day (low emitters: mean 180, SD 25; high emitters: mean 310, SD 35)

### Feature naming convention:
Name the 30 features to feel biologically real. Use names like:

- `Butyrivibrio_cluster` — cellulolytic bacteria associated with low emissions
- `Methanobrevibacter_cluster` — primary methanogen, associated with high emissions
- `Ruminococcus_cluster` — fibre degrader
- `Prevotella_cluster` — generalist fermenters
- `Fibrobacter_cluster` — cellulolytic
- `Methanomassiliicoccus_cluster` — secondary methanogen
- `Lachnospiraceae_cluster`
- `Treponema_cluster`
- `Succiniclasticum_cluster`
- `Clostridium_cluster`
- And 20 further generic features named `genomic_feature_11` through `genomic_feature_30`

### Signal structure:
Design the data so that:
- `Butyrivibrio_cluster`, `Fibrobacter_cluster`, and `Ruminococcus_cluster` are elevated in low emitters (biologically: efficient fermenters that compete with methanogens)
- `Methanobrevibacter_cluster` and `Methanomassiliicoccus_cluster` are elevated in high emitters (biologically: methanogens)
- `Prevotella_cluster` shows moderate elevation in low emitters
- All other features are largely noise (normally distributed, no strong phenotype association)
- Add Gaussian noise throughout so the clusters are not perfectly separable — classification accuracy should land around 80–88%, not 100%

Include a brief comment in the data generation cell explaining the biological rationale for each signal direction, so an instructor reading the code understands what the data represents.

---

## 6. Notebook Structure

Structure the notebook with the following sections, each introduced by a markdown header and explanatory text. Code cells should have minimal inline comments (they will be hidden or ignored by students).

---

### Section 0: Title and Introduction (markdown only)

- Title: "From Microbiomes to Predictions: Genomics and AI in Animal Science"
- One paragraph: what the session is about, the biological question, and what students will do
- A note: "You do not need to understand or modify any code in this notebook. Run each cell and read the outputs."
- A "how to run" instruction: shift+enter to run a cell, or use Runtime > Run all

---

### Section 1: The Biology — What Are We Looking At? (markdown + 1 code cell)

**Markdown:** Explain in plain language:
- What ruminants are and why methane emissions matter (climate, agriculture)
- What a microbiome is — the community of microbes living in the rumen
- The key idea: different microbial communities are associated with different levels of methane emissions
- That we can represent a microbial community as a set of numbers — a "genomic embedding" — by counting characteristic DNA sequence patterns (k-mers) and grouping similar ones
- One sentence: "This is the bridge between biology and machine learning."

**Code cell:** Generate and display the synthetic dataset as a pandas DataFrame (first 10 rows). Show sample ID, phenotype label, methane value, and the first 5 features. This should feel like "here is our data."

**Discussion question:**
> "Before we look at the data, what do you think the microbiome of a low methane cow might look like compared to a high methane cow? What types of microbes might be different?"

---

### Section 2: Visualising the Data — Can We See the Difference? (markdown + 2 code cells)

**Markdown:** Explain:
- We have 30 numbers per sample — too many dimensions to visualise directly
- PCA (Principal Component Analysis) is a technique that compresses many dimensions into two, preserving as much variation as possible
- If low and high emitters are different in their microbiome, we should see them separate in this 2D view
- This is not a biological method — it is a mathematical one. We are asking: "does the biology show up in the maths?"

**Code cell 1:** Run PCA (scikit-learn `PCA(n_components=2)`). Plot PC1 vs PC2 as a scatter plot, coloured by phenotype label (low = one colour, high = another). Use a clean matplotlib figure. Include a legend, axis labels ("Principal Component 1", "Principal Component 2"), and title ("PCA of Rumen Microbiome Genomic Embeddings"). Mark the percentage of variance explained on each axis.

**Code cell 2:** Plot a second figure — a simple bar chart of the top 10 features by their loading on PC1 (i.e. which genomic features drive the main axis of variation). This directly shows which microbial signals are most important for separating the groups.

**Discussion questions:**
> "Do the low and high emitters separate clearly? What would it mean if they overlapped completely?"  
> "Which microbial features appear to drive the separation? Do these make biological sense based on what you read in the introduction?"

---

### Section 3: Training a Classifier — Can a Model Learn This? (markdown + 2 code cells)

**Markdown:** Explain:
- A classifier is a mathematical model that learns to assign a label (low or high emitter) based on input data
- We train it on some samples and test it on samples it has never seen — this tells us whether it has learned something genuinely useful or just memorised the training data
- We are using a Random Forest: an ensemble of many decision trees, each making simple yes/no splits on the features
- No need to understand the maths — focus on what it learns and how well it performs

**Code cell 1:** Train a `RandomForestClassifier` (scikit-learn, 100 trees, `random_state=42`) on 80% of the data. Evaluate on 20% held-out test set. Print:
- Accuracy (as a percentage, rounded to 1 decimal place)
- A simple confusion matrix rendered as a clean heatmap using seaborn (labels: "Low Emitter", "High Emitter")
- Precision and recall for each class

**Code cell 2:** Plot the methane emission values for correctly vs incorrectly classified samples as overlapping histograms or a strip plot. This shows whether misclassifications cluster near the decision boundary (i.e. animals that are genuinely ambiguous).

**Discussion questions:**
> "The model is not perfect. What are the consequences of a false positive (predicting low emitter when the animal is actually high)? What about a false negative?"  
> "The model was trained on 96 samples. Do you think this is enough? What might change with 10,000 samples?"

---

### Section 4: Explainability — Why Did the Model Decide That? (markdown + 2 code cells)

**Markdown:** Explain:
- A model that makes accurate predictions is useful, but in science and in real-world applications, we also need to know *why* it made a prediction
- Random Forests provide a built-in measure called "feature importance" — which input features did the model rely on most heavily?
- This is a simple form of explainable AI (XAI): making the model's reasoning transparent
- If the most important features make biological sense, that gives us more confidence in the model — and generates hypotheses for further research

**Code cell 1:** Extract feature importances from the trained Random Forest. Plot as a horizontal bar chart (top 15 features by importance, sorted descending). Use colour to highlight the features known to be biologically relevant (Methanobrevibacter, Butyrivibrio etc.) versus the noise features. Include a legend.

**Code cell 2:** For a single sample from the test set (choose one correctly classified low emitter and one correctly classified high emitter), display the top 5 features that pushed the prediction in each direction. Render as a simple formatted table or bar chart. Label clearly: "Why the model said LOW EMITTER" and "Why the model said HIGH EMITTER."

**Discussion questions:**
> "The model identified Methanobrevibacter as a key predictor of high emissions. Does this mean Methanobrevibacter *causes* high emissions? How would you test this?"  
> "If a model is accurate but its top features make no biological sense, what would you conclude?"

---

### Section 5: What This Means — and What It Doesn't (markdown only)

**Markdown:** A short reflective section covering:
- What we have demonstrated: that genomic representations of microbial communities carry predictive signal for a host phenotype, and that a simple ML model can extract and explain that signal
- What this does not prove: causality, generalisability across different breeds/diets/environments, or readiness for use as a management tool
- The data challenges that real research faces: small sample sizes, batch effects across studies, compositional data constraints, and the difficulty of multi-study integration
- One sentence connecting back to the research programme: this is the kind of question that motivated projects like James Barnard's PhD — using explainable AI to understand which microbial drivers are genuinely robust across datasets

**No code cell. No discussion question.** This is a landing section — give students a moment to absorb before the group discussion.

---

### Section 6: Summary and Key Concepts (markdown only)

A bullet-point recap of the key concepts introduced:
- Genomic embeddings (k-mer frequency vectors as numerical representations of microbial communities)
- Dimensionality reduction (PCA)
- Classification (Random Forest)
- Feature importance as a form of explainable AI
- The distinction between prediction and causal explanation

Include a "Further Reading" box with 2–3 accessible references (not paywalled where possible).

---

## 7. Visual Style Requirements

- Use a consistent, clean matplotlib style throughout (`plt.style.use('seaborn-v0_8-whitegrid')` or equivalent available in Colab)
- Colour palette for phenotype: use `#2196F3` (blue) for low emitters and `#F44336` (red/orange) for high emitters — consistent across all plots
- All figures: minimum `figsize=(8, 5)`, `dpi=100`, clear titles, labelled axes, legends where needed
- No interactive widgets — static matplotlib figures only
- All figures rendered inline (standard Colab behaviour)

---

## 8. Notebook Formatting Conventions

- Each section header in markdown uses `##` (H2)
- Code cells that students should run are preceded by a markdown cell containing: **▶ Run the cell below**
- Biological terms introduced for the first time are bolded in markdown
- Discussion questions are rendered in a markdown blockquote (`>`) with the label **Discussion** in bold before each question
- Keep markdown cells concise — no paragraph longer than 5 sentences

---

## 9. Testing Requirements

Before delivering the notebook, verify:
- `Runtime > Run all` completes without errors on a fresh Colab session (no pre-existing variables)
- All figures render correctly
- Random seed produces identical outputs on repeated runs
- Total runtime under 3 minutes
- No cells require user input to proceed
- Notebook renders correctly when viewed on GitHub (i.e. valid JSON, no binary blobs)

---

## 10. Deliverable

A single file: `rumen_microbiome_AI_workshop.ipynb`

The file should be ready to share as a GitHub link or direct Colab link. Include a comment at the top of the first code cell:

```python
# Workshop notebook: "From Microbiomes to Predictions: Genomics and AI in Animal Science"
# Prof Chris Creevey, Queen's University Belfast
# Run all cells in order. No modifications required.
# All data is synthetic and generated within this notebook.
```
