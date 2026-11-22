# From Static Ledgers to Living Processes

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](LICENSE)

**Mapping land condition across Australia with one shared AI model — and teaching vision AI to notice what checklists miss.**

- **Presenter:** Dr Peter Scarth (Adjunct Associate Professor, The University of Queensland · Director, Cibo Labs · CTO, Ozius)
- **Event:** GDG AI for Science Asia-Pacific DevFest · Sydney (25 min talk + 5 min Q&A)

---

## View the Presentation

**[https://petescarth.com/multitask-eco-condition](https://petescarth.com/multitask-eco-condition)**

---

## Getting Started (Reproducible Notebook)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/petescarth/multitask-eco-condition/blob/main/examples/getting_started.ipynb)

An end-to-end starter notebook is available in [`examples/getting_started.ipynb`](examples/getting_started.ipynb) (pointing directly to this GitHub repository and public datasets). It covers:

1. **Public Data & AlphaEarth Dequantisation:** Extracting 64-D embeddings (`GOOGLE/SATELLITE_EMBEDDING/V1/ANNUAL`), computing **IBRA v7** subregion centroid similarities (`reference_centroids.json`), and inspecting HCAS vs. Spatial BioCondition disagreement.
2. **4-Head Multi-Task Training:** Building and training `ParametricQuadTaskDNN` from scratch across the **4 public heads** (*Spatial BioCondition*, *HCAS*, *Reference Climax*, *HAVPlot Floristic Nativity*) with spatial blocking and unweighted validation scoring.
3. **80 m Spatial Inference:** Running the self-contained 4-head ONNX model (`examples/data/quadtask_v2_4head.onnx`) across a `128 × 128` Carnarvon Gorge / Buckland Basalts chip.
4. **Verb-Driven Process Prompt (`PROMPT_V5_REFINED`):** Running the inline, noun-blocked Gemini VLM process prompt and Phase 1 rubric check on bundled field photos (`examples/photos/site_185.jpg`, `site_176.jpg`, `site_54.jpg`, with cached offline fallbacks).
5. **Frozen `384-D` Trunk Probing:** Extracting the clean 4-head frozen trunk to measure SVD rank expansion and transfer to downstream ecological targets.

> *Note on data scope:* Proprietary grazing Land Condition (ABCD) and lidar Canopy Cover datasets, weights, and prompts are excluded. Only the first 4 public heads, the clean 4-head frozen trunk, and the verb-driven process prompt are included.

### Upstream Public Datasets

- **AlphaEarth Foundations Satellite Embeddings:** [`GOOGLE/SATELLITE_EMBEDDING/V1/ANNUAL`](https://developers.google.com/earth-engine/datasets/catalog/GOOGLE_SATELLITE_EMBEDDING_V1_ANNUAL)
- **CSIRO HCAS v3.3:** [`data.csiro.au/collection/csiro:65549`](https://data.csiro.au/collection/csiro:65549) (DOIs `10.25919/zhfg-1x80`, `10.25919/jz55-5d44`)
- **HAVPlot Botanical Surveys:** [`doi.org/10.25919/5cex-4s70`](https://doi.org/10.25919/5cex-4s70) (Mokany et al., 2022)
- **Queensland Spatial BioCondition:** [`data.qld.gov.au/dataset/queensland-spatial-biocondition-series`](https://www.data.qld.gov.au/dataset/queensland-spatial-biocondition-series)
- **UN SEEA-EA / FACTE Baselines:** [`csiro:65931`](https://data.csiro.au/collection/csiro:65931) (Owers et al., 2026) · [`csiro:62412`](https://data.csiro.au/collection/csiro:62412) (Yang et al., 2025)
- **IBRA v7 Subregions:** [`data.gov.au/data/dataset/4070b161-1fca-4d23-82ed-ce2659fe8a7a`](https://data.gov.au/data/dataset/4070b161-1fca-4d23-82ed-ce2659fe8a7a) · **ESA WorldCover v200:** `ESA/WorldCover/v200`

---

## Controls & Interactive Features

| Key / Action | Function |
| :--- | :--- |
| `←` / `→` / `Space` | Navigate slides within the current section (main talk stops cleanly on Slide 17) |
| `S` | Toggle slide-synced **Speaker Notes** drawer |
| `G` or `O` | Open the **Slide Overview** grid (main flow + Appendix `A1–A13`) |
| `A` | Jump between the main deck and the **Technical Appendix (`A1–A13`)** |
| `R` | Toggle **Reader Mode** (all 33 slides stacked above their speaker script with **Print / Save PDF**) |
| `1` – `4` | Switch the 4 interactive landscape process regimes on **Slide 13** (*Intact*, *Masked*, *Disrupted*, *Highly disrupted*) |
| `F` | Toggle fullscreen |
| Click figure / video | Fullscreen lightbox zoom on charts/maps/photos; click Slide 5 drive video to pause/resume |

---

## Talk Structure (33 Slides Total)

### Main Flow (`I-1`–`I-3`, Slides `1`–`17`, ~22 min spoken)
- **Intro (`I-1`–`I-3`):** Acknowledgement of Country, overview, and a field-to-orbit background (jackaroo days in bluebush country → Landsat calibration in a rangeland claypan → today).
- **Act 1 · The Problem (`1–2`):** Why separate agency maps (HCAS ecosystem intactness vs. BioCondition structure) disagree on the same hectare across Queensland.
- **Act 2 · The Condition Model (`3–5`):** Compressing multi-sensor satellite data with Google DeepMind **AlphaEarth Foundations** 64-D embeddings (the Earth Engine Satellite Embedding dataset) + bioregion reference lookup into one shared neural trunk predicting consistent maps across **1.2 billion** 80 m pixels, validated along the Eulo–Cunnamulla evaluation drive and 83 unseen South-West Queensland sites.
- **Act 3 · Three Lessons & Results (`6–10`):**
  1. Separating ecological intactness supervision from grazing pasture condition fixes negative baseline correlations and lands 9 in 10 unseen sites within one grazing grade.
  2. Scoring hyperparameter tuning (Bayesian search on Colab GPUs) on an unweighted multi-task error with spatially blocked cross-validation stops optimisers from starving hard heads.
  3. **Rare classes need new data:** **LandLens (Gemini VLM)** grounds paddock photos in date, bioregion, and rainfall context to output auditable `Evidence → Reasoning → Conclusion` JSON — checked against field ecologists at 60 sites (98% within one forage class, r = 0.84, after in-sample calibration) and adding `~5,900` grazing ratings (raising rare Grade D training sites to `~1,100` / `14%`).
  4. Joint multi-task training nearly halves tree-cover error (`−44%` across `~3,600` survey lines) and cuts false native-vegetation alarms on cleared land from `76% → 9%`.
- **Act 4 · Early Research: The Process View (`11–16`):**
  - Slide 11 frames nouns vs. verbs (positioning statement first) and states the hunch; Slide 12 stress-tests it with **Google Hypothesis Generation** (`labs.google.com/science/hypothesis-generation/`), which synthesised `1,985` sources across `10` candidate designs to catch *kinetic conflation* (leading to **Holding** vs. **Losing** verbs) and *geographic mismatch* before building the verb-based experiment.
  - Applied via a two-step verb-centred Gemini VLM prompt across `186` field-photo sites — finding that about two in five (`42%`) Grade A pastures hide a weaker process underneath — mostly missing overstorey, sometimes exotic-grass lock-up (replicated on the 50 newest sites). A satellite-trunk probe predicts these readings with moderate skill across 9 held-out regions (CCC ≈ 0.5, AUC 0.67–0.75) and maps the ~655,000 km² Mitchell corridor with a calibrated 90% uncertainty band per pixel.
- **Close (`17`):** Takeaways, links to slides and code, and acknowledgement of the end-to-end Google AI for Science stack (**Google Hypothesis Generation**, **Gemini VLMs**, **AlphaEarth Foundations**, **Google Antigravity**, and **Google Colab**).

### Technical Appendix (`A1–A13` Backup)
- `A1` Full multi-task architecture · `A2` Bioregion LUT & zero-leakage gradient proof · `A3` Unweighted HPO curve · `A4` Native plant mix vs. climax similarity remediation · `A5` Roadside photo filtering (`80 m` road buffer & perpendicular boundary step) · `A6` 118-photo compass/boundary audit · `A7` Ordered cumulative grazing-grade probabilities · `A8` Shared trunk SVD rank expansion (`5.8×`) · `A9` Production outputs & run times · `A10` Plain-English glossary · `A11` Data sources, AI tools & references · `A12` Next: field tests across Northern Australia · `A13` How good is LandLens? A 60-site field comparison.

---

## Repository Contents

```text
.
├── index.html          # Standalone 33-slide HTML5 presentation (Intro + 17 Main + A1–A13 Appendix)
├── speaker_notes.md    # Complete presenter script with slide timings & rehearsal checkpoints
├── assets/             # Charts, maps, SVG diagrams, field photos, word clouds & drive clip
├── examples/           # End-to-end Colab/Jupyter getting_started.ipynb, 4-head ONNX/PT, centroids & sample photos
├── LICENSE             # Creative Commons Attribution 4.0 International (CC BY 4.0)
├── .gitignore          # Git ignore rules
└── README.md           # This guide
```

---

## License & Third-Party Data Attribution

Unless otherwise noted, the presentation, field photographs, notebook code, verb-driven prompt (`PROMPT_V5_REFINED`), and companion 4-head `QuadTask v2` weights and artefacts in this repository are licensed under the **[Creative Commons Attribution 4.0 International License (CC BY 4.0)](LICENSE)**.

### Third-Party Data Attribution

The companion samples, lookup tables, and references incorporate or build upon third-party public datasets that retain their own licences and attribution requirements:

- **Google DeepMind AlphaEarth Foundations (Satellite Embedding Dataset):** [`GOOGLE/SATELLITE_EMBEDDING/V1/ANNUAL`](https://developers.google.com/earth-engine/datasets/catalog/GOOGLE_SATELLITE_EMBEDDING_V1/ANNUAL) (Google Earth Engine).
- **CSIRO Habitat Condition Assessment System (HCAS v3.3):** Valavi et al. / Williams et al. (2025), [`data.csiro.au/collection/csiro:65549`](https://data.csiro.au/collection/csiro:65549) (DOIs `10.25919/zhfg-1x80`, `10.25919/jz55-5d44`).
- **Harmonised Australian Vegetation Plot Dataset (HAVPlot):** Mokany et al. (2022), [`doi.org/10.25919/5cex-4s70`](https://doi.org/10.25919/5cex-4s70).
- **Queensland Spatial BioCondition Series:** Queensland Department of Environment, Science and Innovation (DESI), [`data.qld.gov.au/dataset/queensland-spatial-biocondition-series`](https://www.data.qld.gov.au/dataset/queensland-spatial-biocondition-series).
- **UN SEEA-EA / FACTE Ecosystem Condition Baselines:** Owers et al. (2026), [`csiro:65931`](https://data.csiro.au/collection/csiro:65931); Yang et al. (2025), [`csiro:62412`](https://data.csiro.au/collection/csiro:62412).
- **Interim Biogeographic Regionalisation for Australia (IBRA v7):** Australian Government Department of Climate Change, Energy, the Environment and Water (DCCEEW), [`data.gov.au/data/dataset/4070b161-1fca-4d23-82ed-ce2659fe8a7a`](https://data.gov.au/data/dataset/4070b161-1fca-4d23-82ed-ce2659fe8a7a).
- **ESA WorldCover v200:** Zanaga et al. (2022), `ESA/WorldCover/v200` (Google Earth Engine).
