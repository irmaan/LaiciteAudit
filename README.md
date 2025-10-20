# Laïcité-by-Design: Operationalizing Religious Neutrality Audits for French-Language AI in Public Administration

**Version:** v1.0  
**Author:** Irmaan Mirzanejad (CNRS UMR 6072 (GREYC), Normandy, France)  
**Contact:** mohammad.mirzanejad@unicaen.fr  
**ORCID:** https://orcid.org/0009-0005-0120-4421  
**Repo:** https://github.com/irmaan/LaiciteAudit  
**Colab (Reproduce Main Results):** https://colab.research.google.com/drive/1nskUQ6G7bHgIRqRF9Dvs7sadMqlaKmd7

> A reproducible audit toolkit assessing laïcité (religious neutrality) in French-language AI models and administrative decision systems.

---

## What is this?
This repository provides the **code, notebook, and artifacts** for a neutral-equivalence, paired-prompt audit of French-language models and decision prompts.  
It operationalizes laïcité by:
- Paired prompts contrasting religious venues with neutral public venues.
- An **equivalence-first** decision rule with a neutral baseline (δ set to the 95th percentile of neutral drift).
- **Holm-adjusted permutation tests** (diagnostic).
- Tasks: **LANGUAGE (head-only PLL)**, **DECISION (oui/non)**, **MODERATION**, **ROUTING/ELIGIBILITY**.

Core finding (v1.0): CamemBERT-base passes LANGUAGE and DECISION gates; XLM-R fails LANGUAGE but passes DECISION/MODERATION/ROUTING—indicating **governance drift** across model families/versions.


[![DOI](https://zenodo.org/badge/1074967701.svg)](https://doi.org/10.5281/zenodo.17401723)

## How to cite
If you use this toolkit, please cite the archived software release:

> Irmaan Mirzanejad (2025). *Laïcité-by-Design: Reproducible Neutral-Equivalence Audit (software)*, v1.0.0. Zenodo. https://doi.org/10.5281/zenodo.17401722

For the latest version, use the concept DOI: https://doi.org/10.5281/zenodo.17401723

Source code: https://github.com/irmaan/LaiciteAudit


---

## Quick start

### Option A — Run on Colab (recommended)
Open the Colab, run the **FINAL RUN** cells in order, and view outputs:
- Colab: https://colab.research.google.com/drive/1nskUQ6G7bHgIRqRF9Dvs7sadMqlaKmd7

### Option B — Run locally
```bash
git clone https://github.com/irmaan/LaiciteAudit
cd LaiciteAudit
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
# Optional: jupyter lab
