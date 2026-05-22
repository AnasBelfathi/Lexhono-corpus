# SCOTUS-LAW Corpus — Construction Pipeline

<p align="center">
  <a href="https://aclanthology.org/2026.eacl-long.137/"><img src="https://img.shields.io/badge/Paper-EACL%202026-blue?style=flat-square&logo=read-the-docs" alt="Paper"></a>
  <a href="https://www.kaggle.com/datasets/gqfiddler/scotus-opinions"><img src="https://img.shields.io/badge/Source-Kaggle%20SCOTUS-20BEFF?style=flat-square&logo=kaggle" alt="Kaggle"></a>
  <a href="https://creativecommons.org/licenses/by/4.0/"><img src="https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey?style=flat-square" alt="License"></a>
  <img src="https://img.shields.io/badge/Conference-EACL%202026-orange?style=flat-square" alt="Conference">
  <img src="https://img.shields.io/badge/Journal-Ib%C3%A9rica%202025-purple?style=flat-square" alt="Ibérica">
</p>

<p align="center">
  <b>Anas Belfathi¹ &nbsp;·&nbsp; Nicolas Hernandez¹ &nbsp;·&nbsp; Laura Monceaux-Cachard¹ &nbsp;·&nbsp; Warren Bonnard²</b><br>
  <b>Mary Catherine Lavissière³ &nbsp;·&nbsp; Christine Jacquin¹ &nbsp;·&nbsp; Richard Dufour¹</b><br>
  <i>¹ Nantes Université, École Centrale Nantes, CNRS, LS2N, UMR 6004, F-44000 Nantes, France</i><br>
  <i>² University of Lorraine, CRINI, France</i><br>
  <i>³ Nantes Université, CRINI, France</i>
</p>

---

## Overview

This repository contains the **data construction and annotation pipeline** for **SCOTUS-LAW**, the first publicly available corpus of U.S. Supreme Court opinions annotated with rhetorical roles at three levels of granularity: *category*, *rhetorical function*, and *step*.

SCOTUS-LAW was introduced as part of the EACL 2026 paper:

> *Coupling Local Context and Global Semantic Prototypes via a Hierarchical Architecture for Rhetorical Roles Labeling*

The corpus covers **180 annotated decisions** spanning **26,328 sentences**, sampled across three dimensions: temporal (1945–2020), authorial (38 justices), and thematic (18 legal domains).

> ⚠️ **Note:** The annotated data is not included in this repository for privacy reasons. This repo focuses on the corpus construction and preparation pipeline.

---

## Repository Structure

```
Lexhono-corpus/
├── datasets/
│   ├── kaggle/                      # Raw opinions downloaded from Kaggle
│   └── opinions-html-format/        # Opinions converted to HTML format (available on request)
├── notebooks/
│   ├── corpus_construction.ipynb         # Sampling strategy & document selection
│   ├── preparation_html_format.ipynb     # HTML conversion & preprocessing
│   ├── formatting_expert_annotation.ipynb # Formatting data for expert annotation
│   └── annotated_corpus_analysis.ipynb   # Corpus statistics & analysis
└── README.md
```

---

## Data Source

Raw opinions were extracted from the Kaggle dataset:

> **SCOTUS Opinions** — [https://www.kaggle.com/datasets/gqfiddler/scotus-opinions](https://www.kaggle.com/datasets/gqfiddler/scotus-opinions)

This dataset provides U.S. Supreme Court decisions in plain text. Our pipeline converts and structures them for rhetorical role annotation.

---

## Corpus Construction Pipeline

### Step 1 — Corpus Construction & Sampling

`notebooks/corpus_construction.ipynb`

Implements the three-dimensional sampling strategy to ensure representativeness:

- **Temporal**: decisions spanning 1945–2020
- **Authorial**: 38 distinct Supreme Court justices
- **Thematic**: 18 legal topic groups (e.g., tax law, criminal law, civil rights)

Representative cases were selected from the most prolific justices in each thematic group, yielding **180 final decisions**.

### Step 2 — HTML Conversion & Preprocessing

`notebooks/preparation_html_format.ipynb`

Converts raw text opinions to a structured HTML format for annotation. This step handles sentence segmentation, text cleaning, and formatting required by the annotation tool.

### Step 3 — Formatting for Expert Annotation

`notebooks/formatting_expert_annotation.ipynb`

Prepares the HTML-formatted documents for the annotation interface used by expert annotators and law students. Outputs are structured to facilitate the double-annotation and adjudication process described in the paper.

### Step 4 — Corpus Analysis

`notebooks/annotated_corpus_analysis.ipynb`

Provides descriptive statistics and analyses of the annotated corpus, including label distributions, inter-annotator agreement, and rhetorical function coverage.

---

## Annotation Scheme

The annotation operates at **three levels of granularity**:

```
Step = Discursive Category + Rhetorical Function + Optional Attributes
```

### Discursive Categories (5)

| Category | Description |
|---|---|
| Setting the scene | Background information and procedural history |
| Analysis | Court's reasoning and justification |
| Resolution | Final ruling and outcome |
| Sources of authority | References to legal sources (precedents, statutes) |
| Announcing | Structural transition markers |

### Rhetorical Functions (13)

`Granting certiorari` · `Presenting jurisdiction` · `Quoting` · `Describing` · `Citing` · `Recalling` · `Accepting arguments` · `Rejecting arguments` · `Stating the Court's reasoning` · `Giving instructions to competent courts` · `Giving the holding of the Court` · `Evaluating the impact of the decision` · `Announcing`

### Optional Attributes

Three optional attributes refine the annotation: **Type** (nature of the content), **Author** (originator of the argument), **Target** (current case vs. referenced precedent).

---

## Corpus Statistics

| Split | Documents | Sentences | Avg. Sentences/Doc | Avg. Tokens/Sentence |
|---|---|---|---|---|
| Train | 144 | 21,396 | 148.58 | 22.95 |
| Dev | 18 | 2,450 | 136.11 | 21.43 |
| Test | 18 | 2,481 | 137.83 | 22.15 |
| **Total** | **180** | **26,327** | — | — |

Top rhetorical functions by frequency:

| Rhetorical Function | Count | % |
|---|---|---|
| Recalling | 8,119 | 30.8% |
| Quoting | 6,441 | 24.5% |
| Presenting jurisdiction | 4,941 | 18.8% |
| Stating the Court's reasoning | 3,198 | 12.1% |
| Describing | 955 | 3.6% |

---

## Annotation Process

The annotation was designed in consultation with **legal experts** (law professors and legal practitioners).

**Annotators**: Two law students, each contributing 240 hours of annotation (compensated at $1,200).

**Calibration**: Annotators first labeled 18 documents pre-annotated by experts. Diverging sentences were reviewed iteratively until expert-level agreement was reached.

**Adjudication**: Each document was double-annotated. Disagreements were resolved by consensus, with unresolved cases escalated to legal experts.

**Inter-annotator agreement**: Fleiss' Kappa improved from 0.67 (initial) to **0.72** after calibration, indicating good consistency.

---

## Related Work

This corpus is used in the following papers for training and evaluating rhetorical role labeling models:

> Belfathi, A., Hernandez, N., Monceaux, L., Bonnard, W., Lavissière, M.C., Jacquin, C., Dufour, R. (2026). *Coupling Local Context and Global Semantic Prototypes via a Hierarchical Architecture for Rhetorical Roles Labeling.* EACL 2026. [[Paper]](https://aclanthology.org/2026.eacl-long.137/) [[Code]](https://github.com/AnasBelfathi/RRL-HierProto)

> Bonnard, W., Lavissière, M.C., Belfathi, A., Hernandez, N., Jacquin, C., Monceaux-Cachard, L. (2025). *"Steps" towards a corpus of SCOTUS opinions annotated using a Swalesian approach.* Ibérica, (50), 45–80.

---

## Citation

If you use this corpus or pipeline, please cite:

```bibtex
@inproceedings{belfathi-etal-2026-coupling,
    title     = "Coupling Local Context and Global Semantic Prototypes via a Hierarchical 
                 Architecture for Rhetorical Roles Labeling",
    author    = "Belfathi, Anas and Hernandez, Nicolas and Laura, Monceaux and
                 Bonnard, Warren and Lavissière, Mary Catherine and
                 Jacquin, Christine and Dufour, Richard",
    booktitle = "Proceedings of the 19th Conference of the European Chapter of the 
                 Association for Computational Linguistics (Volume 1: Long Papers)",
    month     = mar,
    year      = "2026",
    address   = "Rabat, Morocco",
    publisher = "Association for Computational Linguistics",
    url       = "https://aclanthology.org/2026.eacl-long.137/",
    doi       = "10.18653/v1/2026.eacl-long.137",
    pages     = "2986--3004",
    ISBN      = "979-8-89176-380-7"
}

@article{bonnard2025steps,
    title   = {"Steps" towards a corpus of SCOTUS opinions annotated using a Swalesian approach},
    author  = {Bonnard, Warren and Lavissiere, Mary Catherine and Belfathi, Anas and 
               Hernandez, Nicolas and Jacquin, Christine and Monceaux-Cachard, Laura},
    journal = {Ibérica},
    number  = {50},
    pages   = {45--80},
    year    = {2025}
}
```

---

## Contributors

| Name | Affiliation |
|---|---|
| Anas Belfathi | Nantes Université, LS2N |
| Nicolas Hernandez | Nantes Université, LS2N |
| Laura Monceaux-Cachard | Nantes Université, LS2N |
| Christine Jacquin | Nantes Université, LS2N |
| Mary Catherine Lavissière | Nantes Université, CRINI |
| Warren Bonnard | University of Lorraine, CRINI |
| Richard Dufour | Nantes Université, LS2N |

---

## Acknowledgments

This work was granted access to the HPC resources of **IDRIS** under the allocations 2023-AD011014882 and 2023-AD011014767, provided by **GENCI**.

This research was funded in whole or in part by **l'Agence Nationale de la Recherche (ANR)**, project ANR-22-CE38-0004.

---

## License

This work is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).