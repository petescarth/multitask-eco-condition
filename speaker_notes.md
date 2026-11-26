# Speaker Script — From Static Ledgers to Living Processes

**Presenter:** Dr Peter Scarth (Adjunct Associate Professor, UQ · Director, Cibo Labs · CTO, Ozius)  
**Event:** GDG AI for Science Asia-Pacific DevFest, Sydney · 25 min + 5 min Q&A  
**Shortcuts in Deck:** `←`/`→` navigate · `S` speaker notes · `R` Reader Mode · `G` slide grid · `A` Appendix · `1–4` regimes on Slide 13

**Total script length:** 2,817 words (Main Talk) + 920 words (Appendix) = **3,737 words total**.

**Rehearsal checkpoints** (paced at ~128 wpm + slide changes; slower for the Acknowledgement):

| Act | Finish by |
|---|---|
| Intro | 2:40 |
| Act 1 · The problem | 5:00 |
| Act 2 · The condition model | 8:30 |
| Act 3 · Three lessons & results | 14:25 |
| Act 4 · Early research | 22:15 |
| Close | 23:35 |

---

## Main Talk

### I-1 · Acknowledgement of Country  
*Intro · 0:00–1:05 · ~120 words*

Before we look at any maps or models, I would like to begin with an Acknowledgement of Country. I acknowledge the Gadigal people of the Eora Nation, the Traditional Custodians of the land on which we meet today in Sydney. I come from Meanjin — Brisbane — the lands of the Turrbal and Jagera/Yuggera peoples. The field work you will see in this talk was carried out across southern and inland Queensland — including the lands of the Bidjara, Karingbal, Mandandanji, Gunggari, Kooma, Kunja, Budjiti and Mithaka peoples, and neighbouring First Nations across the Channel Country, Balonne and borderlands. I pay my respects to their Elders past and present, and to all Aboriginal and Torres Strait Islander peoples here today.

### I-2 · From Static Ledgers to Living Processes  
*Intro · 1:05–1:45 · ~74 words*

Thanks everyone for coming along. Today we will travel from continental satellite maps right down to the soil surface in inland Queensland. One shared AI model now answers six different questions about land, consistently, across 1.2 billion pixels of Australia. Yet numbers alone still miss how land actually works — so in the final part of the talk I will share early research where vision AI describes living landscape processes alongside a static checklist.

### I-3 · Long science, grounded in the field  
*Intro · 1:45–2:40 · ~106 words*

A quick bit of context on who I am. I started out as a jackaroo — that's my old motorbike — riding between stations and learning to read the land from the ground up. I then spent years with the Queensland Government surveying woodlands and calibrating Landsat on claypans like this one, so that a satellite pixel means the same thing everywhere. Keep an eye out for claypans — you'll see plenty on the drive in a few minutes. Today I bridge UQ, Cibo Labs and Ozius, still chasing what I call long science: models that stay physically consistent from one paddock to a whole continent.

### 1 · Everyone asks a different question about the same patch of land  
*Act 1 · The problem · 2:40–3:45 · ~130 words*

If you stand in a paddock anywhere in Australia and ask 'Is this land healthy?', the answer depends entirely on who is asking. An ecologist looks up at multi-layered native trees, hollows, and fallen logs. A pastoralist looks down at perennial tussock grasses and whether rain soaks in or runs off. A carbon or fire planner wants accurate tree canopy cover. A botanist wants to know whether the plants are native species or introduced grasses. Historically, each agency built its own single-purpose map, with its own definitions, training sites, and blind spots. That left land managers juggling six separate maps that did not agree with one another. Our first goal was simple to state and tricky to engineer: estimate all six of these plain-English measures from one consistent, shared model.

### 2 · Today's official maps of the same place often disagree  
*Act 1 · The problem · 3:45–5:00 · ~150 words*

Here is what happens when you lay two respected official maps on top of each other across nearly three million shared locations in Queensland. On the horizontal axis is a national measure of ecosystem intactness, known as HCAS. On the vertical axis is Queensland's field-calibrated ecological structure score, BioCondition. Both run from zero to one hundred, and people routinely assume they measure the same thing. In practice, converting one map into the other misses by an average of about twenty points out of a hundred. Look at the photo on the right from near Windorah: an undisturbed red sand dune with native spinifex. Ecologically it is intact, yet a map that equates bare ground with degradation or grazing decline will score it harshly — keep this dune in mind, because you will meet it twice more. When different maps send opposite signals for the same hectare, trust breaks down fast.

### 3 · AlphaEarth gives every 10 m of Earth a 64-number fingerprint  
*Act 2 · The condition model · 5:00–6:10 · ~146 words*

So what changed to make a unified continental model practical? Instead of hand-crafting dozens of seasonal vegetation indices from raw cloudy satellite scenes, we start from AlphaEarth Foundations — an Earth-observation embedding model from Google DeepMind. AlphaEarth reads a full year of optical imagery, cloud-penetrating radar, thermal bands, climate, and elevation, and compresses every ten-metre patch of land into a 64-number fingerprint on a unit sphere. You can think of it like a word embedding for landscapes: places with similar vegetation structure, soil moisture, and seasonal rhythm point in similar directions in that 64-dimensional space. For an ML team, this is huge — it means our downstream condition model can stay compact, fast, and focused entirely on learning ecological and pastoral meaning rather than fighting clouds. And you can try this yourself: the embeddings are freely available as the Satellite Embedding dataset in Google Earth Engine.

### 4 · One shared network learns all six maps at once  
*Act 2 · The condition model · 6:10–7:15 · ~135 words*

Here is the heart of the condition model in three steps. On the left, every pixel brings two things: its 64-number AlphaEarth fingerprint, and how similar that fingerprint is to undisturbed reference sites inside its own bioregion. That local benchmark matters enormously in Australia, because a healthy arid woodland looks nothing like a coastal rainforest. In the middle, a single shared neural network trunk compresses those inputs into a common internal representation of the landscape. On the right, six specialised heads branch off to predict Ecological Structure, Ecosystem Intactness, Climax Similarity, Native Plant Mix, Grazing Condition, and Tree Canopy Cover. Notice the amber firewall on the grazing branch: ecological climax benchmarks are strictly blocked from training the grazing head. In a moment you will see why that single architectural rule saved the entire continental map.

### 5 · We check the model against what people see on the ground  
*Act 2 · The condition model · 7:15–8:30 · ~135 words*

Satellite maps are only as trustworthy as the boots-on-the-ground checks behind them. On the left is a looping clip from an evaluation drive along Adventure Way between Eulo and Cunnamulla in South-West Queensland. The dashcam view at the top moves in lockstep with the yellow vehicle marker on our predicted tree canopy map underneath — light grey and orange over open claypans, shifting into rich green as we drive through mulga and box woodlands. On the right is our independent field validation across South-West Queensland: 83 paddock sites assessed on the ground, every single one at least fifteen kilometres away from any site used to train the model. We pair those paddock checks with roughly three thousand six hundred field canopy transects and national botanical survey plots, so every head faces an honest out-of-sample test.

### 6 · Lesson 1 — A pristine ecosystem is not necessarily good pasture  
*Act 3 · Three lessons & results · 8:30–9:40 · ~141 words*

That brings us to three hard-won ML lessons from building this at continental scale. Lesson one is a domain truth that broke our earliest prototypes: a pristine ecosystem is not the same thing as good grazing pasture. Look at the two photos on the left. That same Windorah dune scores near the top for ecological intactness, but it is not Grade A grazing land. Conversely, an open grass paddock can carry stock well while having far fewer trees than a climax woodland. When we tested existing national ecological maps against those 83 unseen grazing sites in South-West Queensland, both maps actually correlated negatively — they rated better pasture lower! Once we quarantined grazing supervision exclusively to real paddock assessments, the model flipped to the right direction, removed systematic bias, and landed nine out of ten unseen sites within one grazing grade.

### 7 · Lesson 2 — Optimisers cheat unless you stop them  
*Act 3 · Three lessons & results · 9:40–10:45 · ~136 words*

Lesson two will feel painfully familiar to anyone who trains multi-task neural networks: optimisers are ruthless shortcut finders. We wanted to tune the relative loss weights balancing our six tasks. On our first attempt, we asked a Bayesian search on Colab GPUs to minimise the weighted validation loss. It looked brilliant on paper — until we inspected what it did. Instead of making the grazing head more accurate, the optimiser simply slashed the grazing task weight close to zero, starving it of gradients so the total weighted number dropped! Switching the search objective to an unweighted error across all six tasks shut that loophole completely. We paired that with spatially blocked cross-validation — holding out whole regions rather than random pixels — because nearby pixels share soil and weather, and random splits wildly flatter geospatial models.

### 8 · Lesson 3 — Rare classes need new data: grounded VLMs can supply it  
*Act 3 · Three lessons & results · 10:45–12:10 · ~173 words*

Lesson three: rare classes need new data, and grounded vision-language models can now supply it. Agronomist transects are expensive and rarely capture badly degraded paddocks, so our grazing head was starved of Grade D examples. So we built LandLens, a Gemini VLM app driven by a detailed land-condition prompt. We don't just ask for a letter grade: we inject the date, bioregion and rainfall history so it can tell drought dormancy from overgrazing, make it ignore road verges and weed look-alikes, and demand an Evidence, Reasoning, Conclusion trace in strict JSON. Roughly five thousand nine hundred LandLens ratings plus two thousand transects lifted Grade D training sites to about eleven hundred. And we checked it: on sixty independent sites scored by field ecologists, the field-calibrated prompt landed within one class ninety-eight percent of the time for forage and every time for erosion — calibrated on those same sites, so held-out testing is next. It even caught errors in the human field workbooks. The same workflow drives our verb-based readings later in the talk.

### 9 · Training six tasks together beats six separate models  
*Act 3 · Three lessons & results · 12:10–13:20 · ~142 words*

A natural ML question is: why not just train six separate specialist models? We ran a head-to-head comparison giving every model the exact same satellite inputs. On the left, evaluated across roughly three thousand six hundred field canopy survey lines, average tree-cover error drops from six point one percent for the national map and four point nine percent for a single-task gradient-boosted decision tree down to three point four percent for our shared model — nearly halving the error, a forty-four percent cut. On the right, look at false native-vegetation alarms on cleared paddocks and urban land. A single-task GBDT trained only on botanical survey plots over-predicts seventy-six percent native cover on cleared ground because botanists rarely survey car parks! Sharing a trunk with canopy cover and intactness teaches the network what clearing looks like, knocking false alarms down to nine percent.

### 10 · Six continental maps from one GPU run  
*Act 3 · Three lessons & results · 13:20–14:25 · ~132 words*

Put all of those fixes together and here is the continental output: six aligned eighty-metre maps covering 1.2 billion valid pixels of Australia, produced in about forty minutes on a single Colab GPU from a small, portable model. Since our abstract we have added a sixth task head and moved to a ten-member ensemble — a little slower than the sixteen minutes quoted there, but more accurate. Top row, left to right: Ecological Structure, Ecosystem Intactness, and Climax Similarity. Bottom row: Native Plant Mix, Grazing Condition, and Tree Canopy Cover. Notice the contrast across the arid interior: the desert dunes remain ecologically intact without falsely lighting up as prime Grade A grazing pasture. Every layer shares the same spatial grammar — and the whole pipeline was built and iterated with Google Antigravity.

### 11 · Nouns count things; verbs describe what land is doing  
*Act 4 · Early research · 14:25–15:50 · ~171 words*

Now I want to pivot — and be upfront that this final part of the talk is early research built on top of the condition model. The condition model gives us consistent numbers. Here is where numbers alone still fall short. Before going further, I want to be clear about what this work is and what it is not. This work is inspired by verb-centred grammar. It does not represent or speak for First Nations knowledge. It looks at how verb-centred and noun-centred languages frame environmental and landscape processes differently. That contrast is the same as the difference between a checklist view of the land and a process view. Most monitoring is noun-heavy: count trees, measure grass percent, tally bare soil — a snapshot, not what water, soil and shade are actually doing. Our hunch was to ask the vision model for verbs instead. On the left are the checklist nouns we block; on the right, Holding verbs, where water, soil and shade are kept, and Losing verbs, where they drain away.

### 12 · Stress-testing the hunch with Google Hypothesis Generation  
*Act 4 · Early research · 15:50–16:45 · ~114 words*

Before building the verb-based experiment, we stress-tested that hunch with Google Hypothesis Generation. It read nearly two thousand arXiv and bioRxiv papers and compared ten candidate research designs against our criteria. It flagged two failure modes and one design principle. First, kinetic conflation: if you only ban nouns, a VLM scores gullying and scouring as healthy simply because they are active — so we split verbs into Holding versus Losing. Second, stripping landscape nouns can break arid-zone intuition, so every reading is anchored in local physical and climate context. And the design principle: keep rich verb prompting offline on field photos, then probe our shared AlphaEarth satellite trunk rather than guessing beneath tree canopies.

### 13 · The same ground through two views  
*Act 4 · Early research · 16:45–18:15 · ~152 words*

When we run that two-step Gemini prompt across 186 field sites, four physical regimes emerge. Let me show two of them live. Regime 1, Intact processes: Site 185 near Weribone is grassy box woodland — tall trees and a full perennial grass layer — so canopies filter the rain while grass roots knit the soil, for a Process Stress of just 1.3 out of 10. [Press 2] Regime 2, Masked: good ground cover earns both sites Grade A, yet something else is quietly failing. Site 176 near Oberina has lost its brigalow overstorey. Site 60 near Dirranbandi still has its trees, but unburnt buffel grass has locked up the ground layer — Process Stress around 3 to 4. The other two tabs, Disrupted and Highly disrupted, show glazed clay pans shedding runoff and hard-set, crusting surfaces above 8 out of 10 — yet even there, fallen branches act as tiny soil-catching micro-sinks.

### 14 · Some top-rated pasture is quietly losing a process  
*Act 4 · Early research · 18:15–19:35 · ~163 words*

Now put those four process regimes directly alongside standard grazing grades across all 186 field-photo sites, and a striking pattern jumps out. Look back at Site 176 near Oberina on the left. Thick grass covers the ground, so a pastoral checklist gives it top marks — Grade A. Yet look at the horizon: that wall of brigalow is what the whole paddock used to be. The trees that shelter the soil, cool the air, and anchor deep moisture are gone. Across the 186 sites on the right, about two in five Grade A pasture sites — forty-two percent — turn out to be Masked or Disrupted underneath. Most have lost their trees, like this one; about one in six still has them, with buffel locking up the ground layer. And it held up on the fifty sites we added in the latest run: eleven of the twenty-one new Grade A sites. That is the exact blind spot a process view begins to uncover.

### 15 · How we check the process view  
*Act 4 · Early research · 19:35–21:05 · ~181 words*

Can satellites actually see this, and how honest is the check? We trained a lightweight probe on the shared internal features of the same condition model — deliberately withholding the six condition maps so it could not take shortcuts — to predict the photo-based Process Stress at 186 sites. Tested on nine held-out regions, agreement is moderate: a concordance of about 0.5 — 0.49 raw, 0.53 after a simple spread calibration — and an AUC of 0.67 to 0.75 for flagging Masked and Highly disrupted sites, where 0.5 is chance. It is strong on the eastern escarpment and close to zero in the far-west Channel Country — remember the Windorah dune? When the far west is held out, the probe reads it as stressed. One honest ML footnote: on our original 136 sites the new backbone alone did no better — the gain came from fifty more field sites. On the right, every reading is anchored to four physical planes — soil, surface water, tree canopy and fire — with guardrails that stop the model inventing cultural, ceremonial or ownership claims.

### 16 · Mapping Process Stress across 655,000 km²  
*Act 4 · Early research · 21:05–22:15 · ~146 words*

When we project that early satellite probe across the roughly six hundred and fifty-five thousand square kilometre Mitchell corridor, a striking spatial pattern emerges. On the left is continuous Process Stress, with our 186 field-photo sites as white dots; on the right, the dominant landscape regime. Just over half maps as Intact processes, in the far-west channel country, the woody ranges and intact mulga. About a third maps as Masked — good ground cover hiding a weaker process, mostly missing overstorey trees, in places exotic grass locking up the ground layer. And about one in seven flags as Disrupted or Highly disrupted. Every pixel now carries a calibrated ninety-percent uncertainty band, and that matters: between model versions the Intact share moved by more than ten points. Treat this as an early research map: it tells field teams where to drive next, not a finished regulatory scorecard.

### 17 · From static ledgers to living processes — what this unlocks  
*Close · 22:15–23:35 · ~169 words*

I will leave this up for questions. Four quick take-homes. First, AlphaEarth's global embeddings let a small team train one compact multi-task model that maps 1.2 billion pixels of Australia in about forty minutes, nearly halving tree-cover error — and the same pattern travels anywhere in APAC. Second, grounded Gemini VLMs turn field photos into auditable scientific data, landing within one class of field ecologists ninety-eight percent of the time once calibrated. Third, domain discipline — separating ecology from pasture and scoring the optimiser fairly — is what makes continental AI trustworthy. Fourth, an early process view, shaped with Google Hypothesis Generation, shows about two in five top-rated pastures quietly losing a key process underneath. Next, savanna field surveys across Northern Australia will test both models out of domain. None of this would have been practical without Google Antigravity for our agentic engineering and Google Colab for the GPU compute. Thank you — the slides and code are at the link on screen, and I would love your questions.

## Technical Appendix (Q&A Backup)

### A1 · A1 · Full model architecture  
*Appendix · Backup · ~66 words*

Appendix A1 shows the full multi-task architecture behind the condition model. Each pixel combines its 64-number AlphaEarth vector with bioregion reference similarity features inside a shared residual trunk. Six specialised heads branch from the trunk: continuous regression heads with outlier-tolerant Huber loss for structure, intactness, climax similarity, native plant mix, and tree canopy cover, alongside an ordered cumulative probability head for grazing grades A through D.

### A2 · A2 · Comparing each pixel with the best sites in its own bioregion  
*Appendix · Backup · ~59 words*

Appendix A2 covers two key engineering pieces. Left: how compact 8-bit stored satellite embeddings are decoded smoothly back onto the unit sphere without losing subtle spectral differences. Right: our mathematical proof of gradient isolation — perturbing local grazing anomaly features produces exactly 0.000 change across all five ecological heads and acts solely on the Grazing Condition head (sensitivity 21.7).

### A3 · A3 · Hyperparameter search: why we optimise a fair objective  
*Appendix · Backup · ~63 words*

Appendix A3 shows the ten-run Bayesian hyperparameter search used to tune learning rate, trunk width, regularisation, and task loss weights under five-fold spatially blocked cross-validation. Because the objective measures the unweighted sum of task errors, the optimiser can only improve by making every head genuinely more accurate. Run 6 reached the minimum unweighted error of 3.23 and was promoted to the final ensemble.

### A4 · A4 · Separating native plant mix from mature-forest similarity  
*Appendix · Backup · ~56 words*

Appendix A4 compares an early prototype against the final model in two regions where early errors showed up clearly. Top row: in south-eastern Australia, adding explicit non-native negative controls cleaned up false native-plant scores across cleared cropping valleys. Bottom row: across arid Australia, expanding undisturbed bioregion reference coverage restored realistic climax similarity in deserts and shrublands.

### A5 · A5 · Photos taken from the road describe the road, not the paddock  
*Appendix · Backup · ~107 words*

Appendix A5 shows the roadside sampling trap we solved when ingesting vehicle-collected paddock photos. Raw GPS points sit on bitumen, gravel shoulders, or bulldozed roadside ditches — which look like severely degraded bare ground from space. Even if you project forty metres along the camera compass bearing, almost half of roadside shots are angled obliquely down the corridor, so you still land inside the paddock only thirty-six percent of the time, with most points stuck in the road reserve. By projecting perpendicular to the actual property boundary on the camera side, inside-paddock placement jumps to fifty-three percent, and our production training pipeline enforces an eighty-metre road buffer.

### A6 · A6 · Camera direction vs. property-boundary geometry  
*Appendix · Backup · ~71 words*

Appendix A6 breaks down our 118-photo roadside geometry audit across six projection methods. Because photographers naturally aim down the fence line or diagonally across a paddock, forty-eight of the 118 shots were aimed sixty degrees or more away from perpendicular. By basic trigonometry, stepping along the compass line barely moves perpendicular to the road reserve, whereas stepping sixty metres perpendicular to the cadastral property boundary lifts inside-paddock placement to fifty-three percent.

### A7 · A7 · Making grade probabilities always add to 100 %  
*Appendix · Backup · ~62 words*

Appendix A7 shows the full continental probability distribution across Grazing Grades A, B, C, and D. Rather than treating grades as unordered categories or noisy independent thresholds, we enforce monotonically non-increasing cumulative cutoffs inside the model graph. Taking differences between consecutive cutoffs guarantees valid, non-negative probabilities summing cleanly to one hundred percent everywhere, while giving land managers a direct view of uncertainty.

### A8 · A8 · Why multi-task training gives a richer internal representation  
*Appendix · Backup · ~69 words*

Appendix A8 explains mathematically why the shared trunk is so useful for downstream research like our early process-view probes. Measuring effective rank via singular value decomposition across 423 held-out grazing sites shows a 5.8-fold expansion in usable dimensionality inside the shared trunk compared with the raw ecological output scores. On the right, a nonlinear probe on the shared trunk beats probing either raw satellite embeddings or ecological outputs alone.

### A9 · A9 · Production outputs and run times  
*Appendix · Backup · ~85 words*

Appendix A9 summarises the operational characteristics of the continental run: six core outputs plus four ordered grazing-grade probability bands, computed at eighty-metre resolution across 1.2 billion valid pixels in roughly forty minutes on a single cloud GPU from a self-contained three-megabyte exported model. The early process-view probe is packaged the same way: a single self-contained 33-megabyte model maps the 655,000 square kilometre corridor in about fifteen minutes, after a 1,008-trial hyperparameter search that took under two and a half hours on a Colab L4 GPU.

### A10 · A10 · Glossary  
*Appendix · Backup · ~31 words*

Appendix A10 provides a quick plain-English glossary for all terms used in the talk and technical backup slides. In the main deck, hovering over dotted-underlined words also surfaces these definitions inline.

### A11 · A11 · Data sources & references  
*Appendix · Backup · ~68 words*

Appendix A11 lists the public Earth-observation benchmarks, the Google AI for Science tools used across the project — AlphaEarth Foundations, Google Hypothesis Generation, Gemini VLMs in LandLens, Google Antigravity, and Google Colab — alongside state and national field survey networks and the URL for the full Eulo to Cunnamulla canopy evaluation drive video. No external network calls are made by this presentation itself so it runs completely offline.

### A12 · A12 · Next: field tests across Northern Australia  
*Appendix · Backup · ~82 words*

Appendix A12 shows the continental baseline across Northern Australia — from Broome and the Kimberley across Darwin, Katherine, and the Gulf to Cairns and Townsville. Because most of our grazing validation so far has been in southern and central Queensland, Northern Australia is the true out-of-domain test. Upcoming savanna field surveys will test whether the six condition maps hold up under monsoonal wet-dry seasons and frequent fire, and whether the early verb-based process view transfers to tropical woodlands and northern grazing lands.

### A13 · A13 · How good is LandLens? A 60-site field comparison  
*Appendix · Backup · ~101 words*

Appendix A13 compares LandLens with field ecologists on sixty independent sites across six pastoral properties in Queensland, New South Wales and South Australia. Out of the box, the cattle-focused prompt landed within one class seventy-eight percent of the time on forage and ninety-two percent on erosion. After adding domain rules — shrub browse, wiregrass palatability and foreground cover checks — forage reached ninety-eight percent within one class with a correlation of 0.84, and erosion one hundred percent. Those calibrated figures are in-sample, so held-out testing is next. Along the way, the comparison also exposed formula errors in the human field workbooks.
