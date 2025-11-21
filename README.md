# Laïcité-by-Design: Operationalizing Religious Neutrality Audits for French-Language AI in Public Administration

**Version:** v1.0  
**Author:** Irmaan Mirzanejad (CNRS UMR 6072 – GREYC, Normandy, France)  
**Contact:** mohammad.mirzanejad@unicaen.fr  
**ORCID:** https://orcid.org/0009-0005-0120-4421  
**Repository:** https://github.com/irmaan/LaiciteAudit  
**Colab (reproduce main results):** https://colab.research.google.com/drive/1nskUQ6G7bHgIRqRF9Dvs7sadMqlaKmd7  
**Zenodo DOI (software):** https://doi.org/10.5281/zenodo.17401722  

> A reproducible neutral-equivalence audit toolkit assessing laïcité (religious neutrality) in French-language AI models and administrative decision systems, in the context of the EU AI Act.

---

## What is this?

This repository provides the **code, notebook and artifacts** for the *Laïcité-by-Design* audit:

- a **paired-prompt audit** of French-language models on *religious* vs *neutral public* contexts (église, mosquée, synagogue, temple vs mairie, hôpital, bibliothèque, etc.),
- a **neutral-calibrated equivalence gate** (δ derived from neutral-only controls) to test whether behaviour in religious contexts stays within an acceptable band of neutral variability,
- and a set of **language, decision, moderation and routing tasks** designed for **public-sector AI** and the **EU AI Act** (FRIA, risk management and documentation obligations).

The goal is to provide a **practical, reproducible pre-deployment gate** for laïcité and religious neutrality in AI systems used by French public authorities, and a concrete example of how to operationalise “fundamental rights / non-discrimination” checks in model choice and deployment.

---

## Results at a glance

Using the laïcité audit (paired prompts + neutral-calibrated equivalence gate):

- **CamemBERT-base**
  - **PASS** on **LANGUAGE** neutrality gate  
  - **PASS** on **DECISION** neutrality gate  
  → Under this audit, CamemBERT-base is compatible with laïcité at both language and decision layers.

- **XLM-RoBERTa-base**
  - **FAIL** on **LANGUAGE** neutrality gate (δ = 6.0786)  
  - **PASS** on **DECISION / MODERATION / ROUTING**  
  → The model appears acceptable on decisions and routing, but already breaks neutrality at the language layer.

- **XLM-RoBERTa-large**
  - Evaluated with the same pipeline; full numbers are given in [`results/laicite_brief.md`](results/laicite_brief.md) and the CSV/JSON artifacts.

This pattern – a French model (CamemBERT-base) passing the neutrality gate while a comparable multilingual model (XLM-RoBERTa-base) fails at the **language** level under the same standard – is what the report calls **governance drift**:

> under identical legal requirements and prompts, switching model families silently changes how religious vs neutral public contexts are treated, even before final decisions are generated.

All results are **fully reproducible** from this repository.

For a one-page summary of the main numbers, see:  
👉 [`results/laicite_brief.md`](results/laicite_brief.md)

---

## Repository structure

- `paper/Laicite_by_Design_Technical_Report.pdf`  
  Full technical report describing the audit protocol, experiments and policy implications.

- `notebooks/Laicite-by-Design-v1.ipynb`  
  Main Jupyter notebook used to run the audit, generate artifacts and produce the brief.

- `results/`  
  - `laicite_brief.md` – one-page summary of the main results (PASS/FAIL, δ values, offending contrasts).  
  - `*.csv` – tabular outputs for each experiment (LANGUAGE, DECISION, MODERATION, ROUTING).  
  - `*.json` – structured audit reports suitable for further analysis or integration in pipelines.

- `requirements..txt`  
  Python dependencies used for local reproduction (Hugging Face transformers, statistics libraries, etc.).  
  > Note: the file name currently has two dots (`requirements..txt`). Use that name when installing, or rename it to `requirements.txt` and adjust the command accordingly.

- `CITATION.cff`, `zenodo.json`, `manifest.json`  
  Metadata and archival information (versioning, DOI, authorship).

- `LICENSE`, `LICENSE-CC-BY-4.0`  
  Licensing for software (MIT) and textual/derived artifacts (CC BY 4.0).

---

## Quick start

### Option A — Run on Colab (recommended)

1. Open the Colab notebook:  
   https://colab.research.google.com/drive/1nskUQ6G7bHgIRqRF9Dvs7sadMqlaKmd7
2. Run the cells in the **“FINAL RUN”** section in order.
3. Inspect the generated CSV/JSON files and the summary (`results/laicite_brief.md`).

This is the easiest way to reproduce the main findings without installing anything locally.

### Option B — Run locally

```bash
git clone https://github.com/irmaan/LaiciteAudit
cd LaiciteAudit
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scriptsctivate
pip install -r requirements..txt
```

Then open the notebook:

```bash
jupyter lab  # or: jupyter notebook
```

…and run `notebooks/Laicite-by-Design-v1.ipynb` end-to-end to regenerate the artifacts in `results/`.

> **Note:** If you do not use virtual environments, you can also install the dependencies globally with `pip install -r requirements..txt`, but a venv is strongly recommended.

---

## Reproducing the experiments

To regenerate the core results described in the technical report:

1. **LANGUAGE layer audit**
   - Run the sections labelled for LANGUAGE in `Laicite-by-Design-v1.ipynb`.
   - This will:
     - sample paired prompts for religious vs neutral public contexts,
     - query the models,
     - compute equivalence statistics (δ from neutral controls),
     - and write CSV/JSON artifacts in `results/`.

2. **DECISION, MODERATION and ROUTING layers**
   - Run the corresponding notebook sections for DECISION, MODERATION and ROUTING.
   - These use the same audit framework but different output tasks (e.g. decision labels, moderation outcomes, routing choices).

3. **Generate the brief**
   - The final section of the notebook regenerates `results/laicite_brief.md`, consolidating the PASS/FAIL outcomes and key offending contrasts (e.g. synagogue vs temple, mosquée vs temple).

If you only want to see the final numbers, you can simply open:

- `results/laicite_brief.md`  
- `paper/Laicite_by_Design_Technical_Report.pdf`

---

## Extending the laïcité audit

The framework is designed to be extended:

- **New models** – You can plug in any Hugging Face-compatible model by editing the model configuration in the notebook (or adding a new entry).
- **New languages** – Although this repository focuses on French, the neutral-equivalence method is language-agnostic; you can adapt the prompt templates for other languages and contexts.
- **New public contexts / attributes** – The current audit targets religious venues vs neutral public venues; you can adapt to other sensitive attributes (e.g. ethnicity, gender, disability) while keeping the same equivalence-first logic.
- **Integration in pipelines** – The JSON artifacts are suitable for integration in CI/CD pipelines, risk registries or pre-deployment checklists for public-sector AI systems.

If you adapt the audit to new settings, please consider opening an issue or pull request, or contacting the author — it helps to build a shared corpus of laïcité/neutrality tests.

---

## Citing

If you use this repository, notebook or artifacts in academic work, reports or audits, please cite the software via the Zenodo record (see `CITATION.cff`):

> Mirzanejad, I. (2025). *Laïcité-by-Design: Reproducible Neutral-Equivalence Audit (software)* (v1.0.0) [Computer software]. Zenodo. https://doi.org/10.5281/zenodo.17401722

A `CITATION.cff` file is included in the repository, so GitHub and citation tools can generate BibTeX and other formats automatically.

If you refer specifically to the **technical report**, you may also cite:

> Mirzanejad, I. (2025). *Laïcité-by-Design: Operationalizing religious neutrality audits for French-language AI in public administration* (Technical report).

---

## Licensing

- **Code and software:** MIT License (see `LICENSE`).  
- **Textual content and generated CSV/JSON outputs:** CC BY 4.0 (see `LICENSE-CC-BY-4.0`).

This means you are free to use, modify and redistribute the code and materials, including in institutional audits and regulatory settings, as long as you provide appropriate attribution.
