# From Static Ledgers to Living Processes

**Mapping land condition across Australia with one shared AI model — and teaching vision AI to notice what checklists miss.**

- **Presenter:** Dr Peter Scarth (Adjunct Associate Professor, The University of Queensland · Director, Cibo Labs · CTO, Ozius)
- **Event:** GDG AI for Science Asia-Pacific DevFest · Sydney (25 min talk + 5 min Q&A)

---

## Running the Presentation

This deck is a **100% self-contained, offline HTML5 presentation** (zero external CDN requests).

### Option 1: Local web server (recommended for smooth video playback)

```bash
git clone https://github.com/petescarth/multitask-eco-condition.git
cd multitask-eco-condition
python3 -m http.server 8000
```

Then open [http://localhost:8000](http://localhost:8000) in any modern browser.

### Option 2: Direct file open

Open `index.html` directly in Chromium, Chrome, Firefox, Edge, or Safari.

---

## Controls & Interactive Features

| Key / Action | Function |
| :--- | :--- |
| `←` / `→` / `Space` | Navigate slides within the current section (main talk stops cleanly on Slide 18) |
| `S` | Toggle slide-synced **Speaker Notes** drawer |
| `G` or `O` | Open the **Slide Overview** grid (main flow + Appendix `A1–A11`) |
| `A` | Jump between the main deck and the **Technical Appendix (`A1–A11`)** |
| `R` | Toggle **Reader Mode** (all 32 slides stacked above their speaker script with **Print / Save PDF**) |
| `1` – `4` | Switch the 4 interactive landscape process regimes on **Slide 13** (*Intact*, *Masked*, *Disrupted*, *Highly disrupted*) |
| `F` | Toggle fullscreen |
| Click figure / video | Fullscreen lightbox zoom on charts/maps/photos; click Slide 5 drive video to pause/resume |

---

## Talk Structure (32 Slides Total)

### Main Flow (`I-1`–`I-3`, Slides `1`–`18`)
- **Intro (`I-1`–`I-3`):** Acknowledgement of Country, overview, and field-to-orbit background.
- **Act 1 · The Problem (`1–2`):** Why separate agency maps (HCAS ecosystem intactness vs. BioCondition structure) disagree on the same hectare across Queensland.
- **Act 2 · The Condition Model (`3–5`):** Compressing multi-sensor satellite data with Google DeepMind **AlphaEarth Foundations** 64-D embeddings + bioregion reference lookup into one shared neural trunk predicting six consistent maps across **1.2 billion** 80 m pixels (`~40 min` on 1 GPU from a `~3 MB` model), validated along the Eulo–Cunnamulla evaluation drive and 83 unseen South-West Queensland sites.
- **Act 3 · Three Lessons & Results (`6–10`):**
  1. Separating ecological intactness supervision from grazing pasture condition fixes negative baseline correlations and lands 9 in 10 unseen sites within one grazing grade.
  2. Scoring hyperparameter tuning on an unweighted multi-task error (with spatially blocked cross-validation) stops optimisers from starving hard heads.
  3. **LandLens (Gemini VLM)** grounds paddock photos in date, bioregion, and 3-/12-month rainfall context to output auditable `Evidence → Reasoning → Conclusion` JSON — adding `~5,900` grazing ratings (raising rare Grade D training sites to `~1,100` / `14%`) and powering the verb-based readings.
  4. Joint multi-task training roughly halves tree-cover error (`6.1% / 4.9% → 3.4%` across `~3,600` survey lines) and cuts false native-vegetation alarms on cleared land from `76% → 9%`.
- **Act 4 · Early Research: The Process View (`11–16`):**
  - Framed using **Google Hypothesis Generation** (`labs.google.com/science/hypothesis-generation/`), which synthesised `1,985` `arXiv` and `bioRxiv` sources across `10` candidate designs to catch *kinetic conflation* (leading to **Holding** vs. **Losing** verbs) and *geographic mismatch blindness* before coding.
  - Applied via a two-step verb-centred Gemini VLM prompt across `136` field-photo sites — uncovering that roughly **1 in 3** Grade A pastures mask missing overstorey structure, and testing satellite-trunk probing across the ~650,000 km² Mitchell corridor.
- **Close (`17–18`):** Upcoming savanna tests across Northern Australia and closing Q&A anchor highlighting the end-to-end Google AI for Science stack (**Google Hypothesis Generation**, **Gemini VLMs**, **AlphaEarth Foundations**, **Google Antigravity**, and **Google Colab**).

### Technical Appendix (`A1–A11` Backup)
- `A1` Full multi-task architecture · `A2` Bioregion LUT & zero-leakage gradient proof · `A3` Unweighted HPO curve · `A4` Native plant mix vs. climax similarity remediation · `A5` Roadside photo filtering (`80 m` road buffer & perpendicular boundary step) · `A6` 118-photo compass/boundary audit · `A7` Ordered cumulative grazing-grade probabilities · `A8` Shared trunk SVD rank expansion (`5.8×`) · `A9` Production outputs & run times · `A10` Plain-English glossary · `A11` Data sources, AI tools & references.

---

## Repository Contents

Only the minimal files required for the deck to render and run offline are tracked:

```text
.
├── index.html          # Standalone 32-slide HTML5 presentation (Intro + 18 Main + A1–A11 Appendix)
├── speaker_notes.md    # Complete presenter script with slide timings
├── assets/             # 39 charts, maps, SVG diagrams, field photos, word clouds & drive clip (~38 MB)
├── .gitignore          # Excludes local reference/ materials from version control
└── README.md           # This guide
```

> Local background documents, raw source videos, prompts, and legacy assets kept in `reference/` are excluded via `.gitignore`.
