# VBT + AR Practice Cards — product option

> Saved 2026-10-04. Machine-readable: `data/products/vbt-ar-practice-cards.json`  
> Lineage: **freaktown** (cards/stage) · **oddhobbies** (print specs) · **bruno wheels** (R2) · **sanskrithelp VB** · **grimoirer Notoria**

---

## The idea

**Point your phone at a card → get the practice.**

| Card family | Phone gives you |
|-------------|-----------------|
| **VBT technique** | Sound-first cue + breath/body move + log prompt |
| **Sanskrit wheel** | Varṇa / dhātu / kāraka / verse lab overlay |
| **Grimoire ritual** | Notoria session shell + PD links + timing |
| **Night stack** | Void / Focus 10 / incubation → Stonedoorway |

Physical card standard: **63.5×88 mm** (oddhobbies TCG spec). QR on back → web/AR overlay.

---

## Product lines

### 1. VBT Practice Cards (flagship for dreaming)

| Tier | Price |
|------|-------|
| Digital PDF deck | $8 |
| Print 52-card starter | $28 |
| Print full curated 112 | $45 |
| AR bundle | $35 |

**Already on disk:**
- `sanskrithelp/data/rag/vijnana-bhairava.txt` + mapping (112 dhāraṇās)
- Readings player units + audio
- `/tantra/practice` — 1:4:2 · 5 voids · practice-log type `vb`

**Deck design:** face = technique visual · back = sound-first cue + QR + one-line log. Start with curated **52**, not all 112 day one.

### 2. Sanskrit × Bruno Wheel AR Cards

Built from **R2 `sanskrit-bruno-wheels.zip`** + peer review:

- Varṇa formation (place × manner) — **start here**
- Dhātu operator wheel (√gam √bhū √kṛ √jñā)
- Kāraka event wheel
- Verse compiler (asato mā sad gamaya)

**Peer-review fixes to bake into cards/data:**
- Generate pratyāhāras from Māheśvara Sūtras (don’t trust incomplete `ac`)
- Curate dhātu labels (no false redup/causal tags)
- Wheel primitive = **place × manner → sound**, not three parallel axes

### 3. Grimoire Ritual AR Cards

Notoria session cards · Ars Brevis figure cards (contested IDs labelled) · planetary-hour cards → ochema.co · PD Turner frame cards.

### 4. Dream / Night AR Cards

5-void · Focus 10 cues · 3D blackness · incubation Qs → Stonedoorway `matrika-night` / Routine X.

---

## AR stack (pick later)

| Option | Effort | Notes |
|--------|--------|-------|
| WebXR / model-viewer + QR | Low | First ship |
| MindAR / image target | Medium | Card face → overlay |
| **freaktown stage-runtime + Capacitor** | Medium | Reuse three.js + mobile shell |
| 8th Wall etc. | High | Only if sales justify |

---

## Lineage reuse

| Repo | Steal |
|------|-------|
| **freaktown** | Trading-card UI · og-card PNG · stage runtime · Capacitor apps/live |
| **oddhobbies** | Card size · print specs · placard/display product thinking |
| **bruno** | Wheel systems · place×manner primitive · StoneDoorway export format |
| **sanskrithelp** | VB corpus · phoneme audio · tantra practice · FSRS |
| **grimoirer** | Notoria pack · product registry · Etsy patterns |

---

## Build order

1. Curate **VBT 52** from mapping + readings  
2. Sample print cards (oddhobbies specs)  
3. QR → simple web overlay (model-viewer first)  
4. Optional freaktown-style card share page  
5. Sanskrit wheel cards from R2 package  
6. Notoria ritual cards  
7. Grimoirer + Etsy packs  

---

## Rights

| OK | Not OK |
|----|--------|
| Technique names + our cues | Full modern VB commentaries |
| PD Turner Notoria frame | Castle/Skinner PDFs |
| Original wheel templates | Monroe proprietary audio |
| Articulation Sanskrit maps | Frequency-heals claims |
