# Speaker Script — From Static Ledgers to Living Processes

**Presenter:** Dr Peter Scarth (Adjunct Associate Professor, UQ · Director, Cibo Labs · CTO, Ozius)  
**Event:** GDG AI for Science Asia-Pacific DevFest, Sydney · 25 min + 5 min Q&A  
**Shortcuts in Deck:** `←`/`→` navigate · `S` speaker notes · `R` Reader Mode · `G` slide grid · `A` Appendix · `1–4` regimes on Slide 12

**Total script length:** 2,949 words (Main Talk) + 674 words (Appendix) = **3,623 words total**.

---

## Main Talk

### I-1 · Acknowledgement of Country  
*Intro · 0:00–0:40 · ~105 words*

Before we look at any maps or models, I would like to begin with an Acknowledgement of Country. I acknowledge the Gadigal people of the Eora Nation, the Traditional Custodians of the land on which we meet today in Sydney. I come from Meanjin — Brisbane — the lands of the Turrbal and Jagera/Yuggera peoples. The field work you will see in this talk was carried out across southern and inland Queensland, on the lands of the Bidjara, Gunggari, Kooma, Wangkumara and Muruwari peoples. I pay my respects to their Elders past and present, and to all Aboriginal and Torres Strait Islander people here today.

### I-2 · From Static Ledgers to Living Processes  
*Intro · 0:40–1:00 · ~117 words*

Thanks everyone for coming along. Today I want to take you on a journey from continental satellite mapping right down to the soil surface in inland Queensland. Every patch of land answers many different questions — about biodiversity, native plants, tree cover, and grazing pasture. We now have one shared AI model that answers six of those questions consistently across 1.2 billion pixels of Australia. Yet as we built it, we kept running into a deeper limit: numbers alone still miss how land actually works. So in the final third of the talk, I will share some early research built on that foundation, where we ask vision AI to describe living landscape processes alongside a static checklist.

### I-3 · Long science, grounded in the field  
*Intro · 1:00–2:00 · ~110 words*

A quick bit of context on who I am and why I care about getting the ground truth right. I started out as a jackaroo, spent years with the Queensland Government surveying woodlands across the state, and now bridge The University of Queensland with Cibo Labs and Ozius. I am driven by what I call long science — mathematical models that stay physically consistent from one paddock to an entire continent, so people on the ground can actually trust what a satellite map tells them. This talk is about what those maps count, the practical traps we hit when training AI on real landscapes, and what static numbers still miss.

### 1 · Everyone asks a different question about the same patch of land  
*Act 1 · The problem · 2:00–3:15 · ~130 words*

If you stand in a paddock anywhere in Australia and ask 'Is this land healthy?', the answer depends entirely on who is asking. An ecologist looks up at multi-layered native trees, hollows, and fallen logs. A pastoralist looks down at perennial tussock grasses and whether rain soaks in or runs off. A carbon or fire planner wants accurate tree canopy cover. A botanist wants to know whether the plants are native species or introduced grasses. Historically, each agency built its own single-purpose map, with its own definitions, training sites, and blind spots. That left land managers juggling six separate maps that did not agree with one another. Our first goal was simple to state and tricky to engineer: estimate all six of these plain-English measures from one consistent, shared model.

### 2 · Today's official maps of the same place often disagree  
*Act 1 · The problem · 3:15–4:30 · ~137 words*

Here is what happens when you lay two respected official maps on top of each other across nearly three million shared locations in Queensland. On the horizontal axis is a national measure of ecosystem intactness, known as HCAS. On the vertical axis is Queensland's field-calibrated ecological structure score, BioCondition. Both run from zero to one hundred, and people routinely assume they measure the same thing. In practice, converting one map into the other misses by an average of about twenty points out of a hundred. Look at the photo on the right from near Windorah: an undisturbed red sand dune with native spinifex. Ecologically it is intact, yet a map that equates bare ground with degradation or grazing decline will score it harshly. When different maps send opposite signals for the same hectare, trust breaks down fast.

### 3 · AlphaEarth gives every 10 m of Earth a 64-number fingerprint  
*Act 2 · The condition model · 4:30–5:45 · ~126 words*

So what changed to make a unified continental model practical? Instead of hand-crafting dozens of seasonal vegetation indices from raw cloudy satellite scenes, we start from AlphaEarth Foundations — an Earth-observation embedding model from Google DeepMind. AlphaEarth reads a full year of optical imagery, cloud-penetrating radar, thermal bands, climate, and elevation, and compresses every ten-metre patch of land into a 64-number fingerprint on a unit sphere. You can think of it like a word embedding for landscapes: places with similar vegetation structure, soil moisture, and seasonal rhythm point in similar directions in that 64-dimensional space. For an ML team, this is huge — it means our downstream condition model can stay compact, fast, and focused entirely on learning ecological and pastoral meaning rather than fighting clouds.

### 4 · One shared network learns all six maps at once  
*Act 2 · The condition model · 5:45–7:15 · ~135 words*

Here is the heart of the condition model in three steps. On the left, every pixel brings two things: its 64-number AlphaEarth fingerprint, and how similar that fingerprint is to undisturbed reference sites inside its own bioregion. That local benchmark matters enormously in Australia, because a healthy arid woodland looks nothing like a coastal rainforest. In the middle, a single shared neural network trunk compresses those inputs into a common internal representation of the landscape. On the right, six specialised heads branch off to predict Ecological Structure, Ecosystem Intactness, Climax Similarity, Native Plant Mix, Grazing Condition, and Tree Canopy Cover. Notice the amber firewall on the grazing branch: ecological climax benchmarks are strictly blocked from training the grazing head. In a moment you will see why that single architectural rule saved the entire continental map.

### 5 · We check the model against what people see on the ground  
*Act 2 · The condition model · 7:15–8:30 · ~135 words*

Satellite maps are only as trustworthy as the boots-on-the-ground checks behind them. On the left is a looping clip from an evaluation drive along Adventure Way between Eulo and Cunnamulla in South-West Queensland. The dashcam view at the top moves in lockstep with the yellow vehicle marker on our predicted tree canopy map underneath — light grey and orange over open claypans, shifting into rich green as we drive through mulga and box woodlands. On the right is our independent field validation across South-West Queensland: 83 paddock sites assessed on the ground, every single one at least fifteen kilometres away from any site used to train the model. We pair those paddock checks with roughly three thousand six hundred field canopy transects and national botanical survey plots, so every head faces an honest out-of-sample test.

### 6 · Lesson 1 — A pristine ecosystem is not necessarily good pasture  
*Act 3 · Three lessons & results · 8:30–10:00 · ~141 words*

That brings us to three hard-won ML lessons from building this at continental scale. Lesson one is a domain truth that broke our earliest prototypes: a pristine ecosystem is not the same thing as good grazing pasture. Look at the two photos on the left. An undisturbed spinifex dune scores near the top for ecological intactness, but it is not Grade A grazing land. Conversely, an open grass paddock can carry stock well while having far fewer trees than a climax woodland. When we tested existing national ecological maps against those 83 unseen grazing sites in South-West Queensland, both maps actually correlated negatively — they rated better pasture lower! Once we quarantined grazing supervision exclusively to real paddock assessments, the model flipped to the right direction, removed systematic bias, and landed nine out of ten unseen sites within one grazing grade.

### 7 · Lesson 2 — Optimisers cheat unless you stop them  
*Act 3 · Three lessons & results · 10:00–11:15 · ~133 words*

Lesson two will feel painfully familiar to anyone who trains multi-task neural networks: optimisers are ruthless shortcut finders. We wanted to tune the relative loss weights balancing our six tasks. On our first attempt, we asked a Bayesian search to minimise the weighted validation loss. It looked brilliant on paper — until we inspected what it did. Instead of making the grazing head more accurate, the optimiser simply slashed the grazing task weight close to zero, starving it of gradients so the total weighted number dropped! Switching the search objective to an unweighted error across all six tasks shut that loophole completely. We paired that with spatially blocked cross-validation — holding out whole regions rather than random pixels — because nearby pixels share soil and weather, and random splits wildly flatter geospatial models.

### 8 · Lesson 3 — Gemini VLMs turn paddock photos into structured data  
*Act 3 · Three lessons & results · 11:15–12:15 · ~216 words*

Lesson three is about how much frontier vision-language models have changed what is possible with field photography. Traditional agronomist transects cost thousands of dollars per site and rarely capture severely degraded paddocks — leaving our grazing head starved of Grade D examples. So we built LandLens, a Gemini VLM application driven by a detailed, domain-grounded land-condition prompt. Crucially, we do not just hand the model a raw photo and ask for a letter grade. We inject the date, bioregion, three-month rainfall decile, and twelve-month rainfall deficit or surplus — so the VLM knows when brown grass is healthy drought dormancy versus overgrazing. We require it to mask out road shoulders, check perennial tussock crowns against annuals and look-alike weeds, and output strict JSON with an Evidence, Reasoning, and Conclusion trace for every pillar. Modern Gemini VLMs are now remarkably strong at this kind of structured visual reasoning: combining roughly five thousand nine hundred LandLens assessments with two thousand agronomist transects lifted rare Grade D training sites to about eleven hundred, correcting severe class imbalance — and as you are about to see, the exact same structured VLM workflow also generates our verb-based landscape process data. We still filter roadside GPS geometry carefully — those details are in Appendix A5 if you want to dig into them.

### 9 · Training six tasks together beats six separate models  
*Act 3 · Three lessons & results · 12:15–13:45 · ~140 words*

A natural ML question is: why not just train six separate specialist models? We ran a head-to-head comparison giving every model the exact same satellite inputs. On the left, evaluated across roughly three thousand six hundred field canopy survey lines, average tree-cover error drops from six point one percent for the national map and four point nine percent for a single-task gradient-boosted decision tree down to three point four percent for our shared model — roughly cutting the error in half. On the right, look at false native-vegetation alarms on cleared paddocks and urban land. A single-task GBDT trained only on botanical survey plots hallucinates seventy-six percent native cover on cleared ground because botanists rarely survey car parks! Sharing a trunk with canopy cover and intactness teaches the network what clearing looks like, knocking false alarms down to nine percent.

### 10 · Six continental maps from one GPU run  
*Act 3 · Three lessons & results · 13:45–15:00 · ~114 words*

Put all of those fixes together and here is the continental output: six aligned eighty-metre maps covering 1.2 billion valid pixels of Australia, produced in about forty minutes on a single cloud GPU from a small, portable model. Top row, left to right: Ecological Structure, Ecosystem Intactness, and Climax Similarity. Bottom row: Native Plant Mix, Grazing Condition, and Tree Canopy Cover. Notice the contrast between Ecosystem Intactness and Grazing Condition across the arid interior: the desert dunes and central ranges remain ecologically intact, without falsely lighting up as prime Grade A grazing pasture. And every layer shares the exact same spatial grammar, so landholders, ecologists, and planners are finally looking at one coherent picture.

### 11 · Nouns count things; verbs describe what land is doing  
*Act 4 · Early research · 15:00–16:30 · ~216 words*

Now I want to pivot — and be completely upfront that this final third of the talk is early research built on top of our condition model. The condition model gives us consistent numbers. Here is where numbers alone still fall short. Before showing how we built this experiment, I want to be crystal clear about what it is and what it is not. This work is inspired by verb-centred grammar. It does not represent or speak for First Nations knowledge. It looks at how verb-centred and noun-centred languages frame environmental and landscape processes differently. That contrast is the same as the difference between a checklist view of Country and a process view. Most scientific monitoring is noun-heavy: count trees, measure grass percent, tally bare soil. That tells you what is sitting there at a single instant, not what is actively happening to water, soil, and shade. Using the exact same Gemini vision-language workflow behind LandLens, we discovered that free-form prompts slipped straight back into checklists or invented unsupported stories. So we designed a two-step prompt: Step 1 blocks checklist nouns completely and asks only for observable physical actions — Holding verbs like root-knitting, percolating, and arch-shading where water, soil, and shade are kept, versus Losing verbs like hard-setting, crusting, and sheet-stripping where they drain away.

### 12 · The same ground through two views  
*Act 4 · Early research · 16:30–18:15 · ~200 words*

When we run that verb-centred Gemini prompt across 136 field photos, four clear physical regimes emerge — you can click the tabs or press keys 1 to 4 to compare the checklist view and the process view side by side. Regime 1, Intact processes: Site 95 near Windorah is that spinifex sand dune — a grazing checklist grades it D, yet the process view sees deep sand percolating rain and spinifex root-knitting the slope, giving low Process Stress of 1.6 out of 10. Carnarvon Gorge beside it scores 1.1. Regime 2, Masked: Site 08 at Morven and Site 61 look green and grassy, so checklists rate them well, yet the process view flags missing overstorey trees and baking air above the grass — Process Stress around 4 out of 10. Regime 3, Disrupted: Site 51 at Nebine still has remnant trees that boost a canopy checklist, while glazed clay pans shed runoff between groves; Site 70 shows pulled mulga slash. Regime 4, Highly disrupted: Site 54 at Bollon and Site 132 at Lower Mount Walker show hard-set, crusting, pan-smearing surfaces with Process Stress above 8 — yet even there, the process view spots fallen branches acting as tiny soil-catching micro-sinks.

### 13 · Some top-rated pasture is quietly losing its trees  
*Act 4 · Early research · 18:15–19:30 · ~125 words*

Now put those four process regimes directly alongside standard grazing grades across all 136 field-photo sites, and a striking pattern jumps out. Look back at Site 08 near Morven on the left. After a wet season, thick introduced buffel grass covers the ground, so a pastoral checklist gives it top marks — Grade A. Yet look at the horizon: the multi-layered woodland trees that shelter the soil, cool the air, and anchor deep moisture are gone. Across the 136 sites on the right, roughly one in three Grade A pasture sites — thirty-eight percent — turn out to be Masked or Disrupted underneath, while more than half of Grade B sites are Masked. That is the exact blind spot a process view begins to uncover.

### 14 · How we check the process view  
*Act 4 · Early research · 19:30–20:30 · ~171 words*

Whenever you introduce a new lens like this, the most important question is: can satellites actually detect it, and how honest is the validation? We took the 136 ground-photo Process Stress labels generated by our two-step verb-guided vision model and trained a lightweight satellite probe solely on the shared internal features of our condition model — deliberately withholding the condition maps themselves so the probe could not take shortcuts. On held-out cross-validation across those 136 sites, agreement is moderate: 0.42 concordance on Process Stress, 0.45 correlation on the gap between tree structure and surface cover, and 0.64 to 0.66 detection scores for flagging Masked and Highly disrupted sites — clearly above chance, and promising as an early cross-modal result, though still needing broader spatially independent field tests before any operational use. On the right, every reading is anchored to four concrete physical planes — soil and subsurface, surface water, tree canopy, and fire — with strict language guardrails so the model is never allowed to invent cultural, ceremonial, or ownership claims.

### 15 · Mapping Process Stress across 650,000 km²  
*Act 4 · Early research · 20:30–21:45 · ~133 words*

When we project that early satellite probe across the roughly six hundred and fifty thousand square kilometre Mitchell corridor — spanning inland Queensland from the desert channels east toward Roma — a striking spatial pattern emerges. On the left is continuous Process Stress from zero to eight, with our 136 field-photo sites plotted as white dots. On the right is the dominant landscape regime. About forty-three percent maps as Intact processes, concentrated in the woody ranges and spinifex dunes. Roughly thirty-eight percent maps as Masked — open grazing downs where good ground cover masks simplified tree structure. And around twenty percent flags as Disrupted or Highly disrupted. Again, treat this as an early research map: it is best used to focus where field teams should drive next, not as a finished regulatory scorecard.

### 16 · Next: field tests across Northern Australia  
*Close · 21:45–22:45 · ~108 words*

So where does this go next? Right now we have a clean continental baseline across Northern Australia — from Broome and the Kimberley across Darwin, Katherine, and the Gulf to Cairns and Townsville. Because most of our grazing validation so far has been in southern and central Queensland, Northern Australia is the true out-of-domain test. Over the coming dry seasons, upcoming savanna field surveys will put this baseline to the test on two concrete questions: first, whether our six condition maps stay accurate across monsoonal wet-dry seasons and frequent savanna fires; and second, whether the early verb-based process view transfers cleanly to tropical woodlands and northern grazing lands.

### 17 · From static ledgers to living processes — what this unlocks  
*Close · 22:45–24:00 · ~257 words*

I will leave this slide up for questions, because it captures both what worked here and what this stack unlocks across the Asia-Pacific AI for Science community. First, Google DeepMind's AlphaEarth Foundations genuinely changes the unit economics of Earth science: compact 64-number global satellite embeddings let a small academia-industry team build a three-megabyte multi-task model that maps 1.2 billion pixels across an entire continent in forty minutes on one GPU — cutting tree-cover error nearly in half and eliminating false native alarms on cleared land. Because those embeddings are global, this exact pattern travels across borders and biomes right across APAC. Second, frontier Gemini vision-language models solve one of field science's oldest bottlenecks: when grounded with rainfall history and explicit domain rules, LandLens turns everyday paddock photos into auditable JSON, adding nearly six thousand grazing observations and driving our verb-based readings. Third, domain discipline is what turns research into operational infrastructure — respecting the boundary between intact ecosystems and grazing pasture, optimising fairly, and filtering roadside bias produce maps ready for national natural-capital accounts and sustainable grazing. And fourth, pairing spatial AI with cognitive linguistics moves us from static accounting ledgers toward living processes — revealing hidden structural loss beneath green grass. The hardest scientific challenges sit right at the intersection of disciplines and between academia and industry, and events like APAC AI for Science DevFest are where those collaborations spark. Thank you — I would love to take your questions, and we have eleven technical appendix slides ready if you want to dive under the hood.

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
*Appendix · Backup · ~43 words*

Appendix A9 summarises the operational characteristics of the continental run: six core outputs plus four ordered grazing-grade probability bands, computed at eighty-metre resolution across 1.2 billion valid pixels in roughly forty minutes on a single cloud GPU from a self-contained three-megabyte exported model.

### A10 · A10 · Glossary  
*Appendix · Backup · ~31 words*

Appendix A10 provides a quick plain-English glossary for all terms used in the talk and technical backup slides. In the main deck, hovering over dotted-underlined words also surfaces these definitions inline.

### A11 · A11 · Data sources & references  
*Appendix · Backup · ~47 words*

Appendix A11 lists the public Earth-observation benchmarks, state and national field survey networks, our LandLens Gemini VLM photo-reasoning pipeline, and the URL for the full Eulo to Cunnamulla canopy evaluation drive video. No external network calls are made by this presentation itself so it runs completely offline.
