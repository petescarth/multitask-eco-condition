# From Static Ledgers to Living Processes

**Mapping land condition across Australia with one shared AI model — and teaching vision AI to notice what checklists miss.**

- **Presenter:** Dr Peter Scarth (Adjunct Associate Professor, The University of Queensland · Director, Cibo Labs · CTO, Ozius)
- **Event:** GDG AI for Science Asia-Pacific DevFest · Sydney (25 min talk + 5 min Q&A)

---

## View the Presentation

**[https://petescarth.com/multitask-eco-condition](https://petescarth.com/multitask-eco-condition)**

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

Only the minimal files required for the deck to render and run offline are tracked:

```text
.
├── index.html          # Standalone 33-slide HTML5 presentation (Intro + 17 Main + A1–A13 Appendix)
├── speaker_notes.md    # Complete presenter script with slide timings & rehearsal checkpoints
├── assets/             # 42 charts, maps, SVG diagrams, field photos, word clouds & drive clip
├── .gitignore          # Excludes local reference/ materials from version control
└── README.md           # This guide
```

> Local background documents, raw source videos, prompts, and legacy assets kept in `reference/` are excluded via `.gitignore`.
