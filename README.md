<div align="center">

# FalLess

### AI-Assisted, Gamified Fall-Risk Assessment for Adults with Intellectual Disability

**A Cyber-Physical AI screening and prevention platform for supported-living and adult disability home settings**

Republic Polytechnic · Biologic Technik · Metta Welfare Association

</div>

---

> **Prototype notice.** This repository contains a **front-end, single-file demonstration prototype**. It uses **synthetic data for 60 fictitious residents** and does not connect to any live capture device, database, or clinical system. All scores, metrics, and recommendations shown are illustrative. Nothing in this prototype is a medical device or a validated clinical instrument, and no clinical decision should be made on the basis of its output. See [§9 Limitations & Governance](#9-limitations-governance-and-responsible-use).

---

## Table of Contents

1. [Overview](#1-overview)
2. [Clinical & Scientific Basis of the Intervention](#2-clinical--scientific-basis-of-the-intervention)
3. [The Four Gamified Assessment Stations — Scientific Basis](#3-the-four-gamified-assessment-stations--scientific-basis)
4. [The FalLess Risk Model](#4-the-falless-risk-model)
5. [Comprehensive Data Dictionary](#5-comprehensive-data-dictionary)
6. [Prototype Architecture & Feature Walkthrough](#6-prototype-architecture--feature-walkthrough)
7. [Cyber-Physical AI — Technical Roadmap](#7-cyber-physical-ai--technical-roadmap)
8. [Deploying to GitHub Pages](#8-deploying-to-github-pages)
9. [Limitations, Governance & Responsible Use](#9-limitations-governance-and-responsible-use)
10. [References](#10-references)

---

## 1. Overview

**FalLess** is a fall-risk assessment and prevention platform designed specifically for **adults with intellectual disability (ID)** living in supported or residential care. It reframes assessment as a short, gamified session of four validated movement and cognitive tasks. The movement data captured by those tasks is fused, on-device, with caregiver-reported clinical and behavioural information into a single **explainable risk profile**, which in turn drives a **personalised, staff-light prevention plan**. Because the session is gamified and repeatable, it also serves as a longitudinal monitoring tool rather than a one-off test.

### Why this population needs a purpose-built tool

Standard geriatric fall-risk instruments (e.g. Berg Balance Scale, Timed Up-and-Go, Morse Fall Scale) assume a level of verbal comprehension, instruction-following and compliance that many adults with intellectual disability do not have. A 2023 systematic review of fall interventions in community-dwelling adults with ID found **no interventions in the literature that used falls-risk or environmental-falls-risk assessment tools with this population**, and evidence-based fall-prevention programmes are validated only for people with typical cognition. FalLess is designed to close this gap: a tool built for the ID population, using accessible, non-verbal, game-based tasks, and validated on an ID cohort.

### The end-to-end cycle

```
  ┌─────────────┐    ┌─────────────┐    ┌──────────────┐    ┌─────────────┐    ┌────────────┐
  │  1. ONBOARD │ ─► │ 2. PLAY &   │ ─► │ 3. AI RISK   │ ─► │ 4. REVIEW & │ ─► │ 5. REPEAT  │
  │  Consent,   │    │   ASSESS    │    │   FUSION     │    │  PERSONALISE│    │ (weekly →  │
  │  comms      │    │  4 gamified │    │  on-device,  │    │  staff-light│    │ continuous │
  │  profile,   │    │  stations   │    │  explainable │    │  prevention │    │ monitoring)│
  │  risk facts │    │             │    │  score       │    │  plan       │    │            │
  └─────────────┘    └─────────────┘    └──────────────┘    └─────────────┘    └────────────┘
        ▲                                                                              │
        └──────────────────────────── continuous reassessment ────────────────────────┘
```

---

## 2. Clinical & Scientific Basis of the Intervention

### 2.1 The anchoring evidence — an ID-specific risk model

The FalLess risk model is anchored on the first peer-reviewed study to develop and validate fall/injury-risk assessment tools **specifically for adults with intellectual disability in supported living**:

> **Petropoulou, E., Skelton, D. A., & Finlayson, J. (2026).** *Predicting Injuries in Adults With Intellectual Disabilities in Supported Living: Development and Validation of Risk Assessment Tools.* **Journal of Applied Research in Intellectual Disabilities (JARID), 39(3), e70253.** https://doi.org/10.1111/jar.70253

In that study, the **independent predictors** of injury were:

| Predictor | Direction | How FalLess captures it |
|---|---|---|
| **Poor balance or coordination** | ↑ risk | *Steady Stand* station (BalanceVision) — the single strongest predictor, weighted highest |
| **Polypharmacy** | ↑ risk | Onboarding — regular-medication count |
| **Antiepileptic medication** | ↑ risk | Onboarding — clinical flag |
| **Antipsychotic medication** | ↑ risk | Onboarding — clinical flag |
| **Restlessness** | ↑ risk | Caregiver observation + *Quick Reflex* processing-speed proxy |
| **Family co-residence** | ↓ risk (protective) | Onboarding — reduces composite score |
| **Diagnosed heart condition** | ↓ risk (protective) | Onboarding — reduces composite score |

FalLess encodes every one of these predictors, including the two protective factors, which subtract from the composite score. This direct traceability from a published, ID-specific model is the scientific backbone of the platform.

### 2.2 Why gamification is clinical, not cosmetic

Gamification in FalLess is a deliberate design decision grounded in two converging evidence bases:

1. **Exergaming reduces falls.** Meta-analyses of randomised controlled trials in older adults show exergaming interventions are associated with a **lower overall fall rate** than comparator interventions, with gamified elements (real-time feedback, progress tracking) improving motivation and adherence.
2. **Gamified exercise works in the ID population specifically.** A pilot study of gamified exercise in adults with intellectual disability found real functional gains — increased strength, reduced fall risk on the Tinetti scale, improved quality of life and executive function — with **high adherence and no adverse events**.

Because adherence is the primary barrier to fall prevention in this population, making the *assessment itself* the *exercise session* solves the adherence problem and turns a one-off test into a longitudinal trend. The same physical action is simultaneously the game mechanic, the sensor input, and the clinical measurement — the essence of the Cyber-Physical AI framing.

### 2.3 Accessible, consent-first assessment

The onboarding stage is built on supported decision-making principles: a person is assumed to have capacity unless proven otherwise, and needing support to decide does not remove the ability to consent. FalLess records a **per-resident communication profile** (Easy Read, verbal, Talking Mats, or behavioural/non-verbal), captures **resident assent and caregiver-reported data on separate tracks**, and logs the reasonable adjustments made — producing the auditable evidence trail that IRB review and Metta's own quality standards require.

### 2.4 Intervention basis

The prevention plans generated by FalLess draw on a **modified Otago Exercise Programme adapted for intellectual and developmental disability** (progressive strength and balance training), rather than generic elderly-population exercise plans, plus medication-review, environmental and behavioural interventions mapped one-to-one to the flagged risk factors. Every recommendation names the finding it answers, and staff review and approve before anything enters a care plan — the system proposes, it never decides.

---

## 3. The Four Gamified Assessment Stations — Scientific Basis

FalLess integrates four browser-based, computer-vision-assisted or timing-based assessment applications, each mapping to a distinct fall-risk domain. All four run entirely **on-device** (camera frames and timing are processed in the browser; **no video or image is ever stored or uploaded** — only numeric results leave the device). The technical detail below is drawn from the source applications' own system manuals.

### 3.1 Steady Stand — postural control & balance
*Powered by **BalanceVision** · Single-Leg Balance test*

| | |
|---|---|
| **Fall-risk domain** | Postural control / balance & coordination — **the strongest predictor** in Petropoulou et al. (2026) |
| **Task** | Single-leg stance (hands on hips), held up to a chosen maximum (30/45/60 s) |
| **Technology** | Google MediaPipe Pose Landmarker (lite, float16), 33 body landmarks per frame, on-device (GPU/WASM) |
| **Primary output** | Balance duration + composite **Stability Score (0–100)** |
| **Movement metrics** | Mediolateral (lateral) sway (mean/max/RMS/SD), torso tilt (mean/max/SD), torso angular velocity (mean/peak/RMS), support-knee angle & variability, pelvic (hip-line) tilt & variability, raised-leg positional variability, corrective-movement count, sway classification |

**Scientific note.** All "sway" values are **camera-derived body-landmark displacement proxies, not force-platform Centre-of-Pressure (COP)**. The composite Stability Score is a weighted sum of six sub-scores (duration 50%, torso 15%, angular 10%, knee 10%, pelvic 10%, corrective movements 5%). Age-referenced single-leg-stance comparison values are provided for context. The 10-second single-leg-stance threshold relates to functional/health indicators reported in the literature (Araujo et al., 2022). The Stability Score is an application-generated indicator and is **not clinically validated**.

### 3.2 Strength Circuit — functional endurance
*Powered by **SilverHYROX** · 30-second Sit-to-Stand + Seated Row*

| | |
|---|---|
| **Fall-risk domain** | Lower- and upper-body functional endurance (relates to balance/coordination predictor) |
| **Task** | Two 30-second seated stations: chair Sit-to-Stand (lower body) and Seated Row (upper body) |
| **Technology** | MediaPipe Pose Landmarker; automatic repetition counting via per-station state machines with temporal persistence |
| **Primary output** | Combined score = STS reps + Row reps |
| **Subsidiary metrics** | Per station: elapsed time, average / fastest / slowest rep time, consistency band (CV), and (row only) average forward reach normalised to torso length |

**Scientific note.** The Sit-to-Stand station is inspired by the widely used **30-second chair-stand** construct (lower-body functional endurance). Rep detection is based on vertical rise of shoulder/hip landmarks from a calibrated seated baseline; the Seated Row detector is intentionally lenient (horizontal wrist displacement, no form enforcement). The combined score is an application-specific challenge score, not a validated clinical scale.

### 3.3 Quick Reflex — processing speed & reactive control
*Powered by **Virtual BlazePod** · Reaction-time game*

| | |
|---|---|
| **Fall-risk domain** | Processing speed / reactive stepping — relates to the **restlessness** predictor |
| **Task** | Fast, non-verbal tap-to-target reaction game (red → green stimulus paradigm) |
| **Primary output** | Best reaction time (ms) + accuracy |
| **Metrics** | Best / mean / median reaction time, SD (variability), range, slowest trial, false starts (impulsivity/anticipation indicator), per-attempt raw times |

**Scientific note.** Reaction time is measured with the browser's `performance.now()` and therefore includes display, input and OS-scheduling latency in addition to psychomotor time. Values are relative within the same device and should not be compared across devices without calibration. False starts (taps during the red phase) provide an impulsivity/anticipation signal directly relevant to the restlessness construct.

### 3.4 Puzzle Focus — attention & visuospatial processing
*Powered by **CognitiveChallenge** · Reaction + picture-tile tasks only (2 of 4)*

| | |
|---|---|
| **Fall-risk domain** | Executive attention / visuospatial processing (supporting domain) |
| **Task** | Visuospatial 3×3 picture-tile reconstruction (plus the reaction task shared with Quick Reflex) |
| **Primary output** | Puzzle completion time (s) |
| **Metrics** | Completion time, total moves, unproductive moves (swaps that reduce correctly-placed tiles), first-move accuracy |

**ID-specific adaptation — important.** CognitiveChallenge natively offers four stations. For the FalLess ID pilot, **two are deliberately removed**:
- **Serial-7 subtraction (Attention & Calculation)** — removed. It measures numeracy far more than attention in this population; a resident who cannot subtract will floor-score regardless of true fall risk, adding noise to the model and creating a poor experience.
- **5-item picture-sequence memory** — held out of the composite (available only as an optional bonus round for higher-functioning residents), because for lower-functioning residents it measures short-term memory capacity unrelated to falls.

Only the **Reaction Time** and **Visuospatial (picture-tile)** tasks feed the risk model. During the visuospatial task, the visible timer and any "unproductive moves" framing are hidden from the resident — completion is the resident-facing outcome; the move/time data is captured for staff analysis only.

---

## 4. The FalLess Risk Model

FalLess computes six **domain risk scores (0–100, higher = worse)**, then combines them into a single weighted composite, adjusted for protective factors.

### 4.1 Domain scores

| Domain | Primary inputs | Source station / onboarding |
|---|---|---|
| **Balance** | Stability score, mediolateral sway | Steady Stand |
| **Strength** | Sit-to-stand reps, seated-row reps | Strength Circuit |
| **Reflex / Speed** | Mean reaction time, accuracy | Quick Reflex |
| **Attention** | Puzzle completion time, unproductive moves | Puzzle Focus |
| **Clinical / Meds** | Falls history, polypharmacy, antiepileptic, antipsychotic | Onboarding |
| **Caregiver obs.** | Unsteadiness, restlessness, hazards, decline | Onboarding |

### 4.2 Composite weighting *(placeholder — see note)*

```
composite_raw =  0.24 × Balance
              +  0.16 × Strength
              +  0.12 × Reflex
              +  0.10 × Attention
              +  0.22 × Clinical
              +  0.16 × Caregiver

protective    =  (family co-residence ? 7 : 0) + (no heart-condition exclusion ? 6 : 0)

composite     =  clamp( composite_raw − protective , 0 , 100 )
```

**Risk bands:** Low (0–44) · Moderate (45–69) · High (70–100). Reassessment interval follows the band (High → 2 weeks, Moderate → 4 weeks, Low → 12 weeks).

> ⚠️ **The weights above are engineering placeholders**, chosen to reflect the relative importance of predictors in Petropoulou et al. (2026) (balance weighted highest). They are **not validated coefficients**. Final weights must be derived empirically from the Metta pilot cohort and the needs assessment before the model informs any real decision.

### 4.3 Explainability

Every point in the composite is traceable to a named factor. The Risk Profile screen lists the **top contributing factors** with their point contributions, shows the six domain bars, and states the protective-factor adjustment (including what the score *would* have been without protectives). This satisfies the "explainable, staff-has-final-say" requirement — the model recommends, it never decides.

---

## 5. Comprehensive Data Dictionary

This section documents **every data element** in the FalLess platform: (A) the fields the prototype captures/derives itself, and (B–E) the complete set of fields produced by each of the four underlying capture applications (transcribed from their published system manuals), which the production system will ingest.

### 5.A FalLess platform fields (this prototype)

#### 5.A.1 — Resident record (onboarding)

| Field | Type | Values / Unit | Description |
|---|---|---|---|
| `id` | String | `MW-####` | Resident identifier |
| `name` | String | free text | Resident full name |
| `unit` | Categorical | Block A/B/C, Hostel 1/2 | Ward / living unit |
| `age` | Integer | years | Resident age |
| `disability` | Categorical | Intellectual / Physical / Multiple | Primary disability type |
| `commMode` | Categorical | Easy Read / Verbal / Talking Mats / Behavioural–Non-verbal | Primary communication mode |
| `followInstr` | Categorical | Reliably / With prompting / Rarely | Instruction-following ability |
| `falls` | Ordinal | 0 = none, 1 = one, 2 = two+ | Falls in last 12 months |
| `meds` | Ordinal | 0 = <5, 1 = 5–8, 2 = 9+ | Regular-medication count (polypharmacy) |
| `antiepileptic` | Boolean | 0/1 | Antiepileptic prescribed |
| `antipsychotic` | Boolean | 0/1 | Antipsychotic prescribed |
| `heartCond` | Boolean | 0/1 | Diagnosed heart condition (protective) |
| `familyCo` | Boolean | 0/1 | Family co-residence (protective) |
| `unsteady` | Ordinal | 0/1/2 | Seen unsteady (last 2 weeks) |
| `restless` | Ordinal | 0/1/2 | Restlessness / impulsivity |
| `hazard` | Boolean | 0/1 | Footwear / room hazard flagged |
| `decline` | Boolean | 0/1 | Decline since last review |
| `staff` | String | free text | Assigned reviewer |

#### 5.A.2 — Derived risk output (per assessment)

| Field | Type | Unit | Description |
|---|---|---|---|
| `domains.balance` | Integer | 0–100 | Balance domain risk |
| `domains.strength` | Integer | 0–100 | Strength domain risk |
| `domains.reflex` | Integer | 0–100 | Reflex/speed domain risk |
| `domains.attention` | Integer | 0–100 | Attention domain risk |
| `domains.clinical` | Integer | 0–100 | Clinical/medication domain risk |
| `domains.caregiver` | Integer | 0–100 | Caregiver-observation domain risk |
| `score` | Integer | 0–100 | Composite fall-risk score |
| `rawNoProt` | Integer | 0–100 | Composite before protective adjustment |
| `protective` | Integer | points | Protective-factor deduction |
| `band` | Categorical | Low / Moderate / High | Risk band |
| `hist[]` | Integer[] | 0–100 | Composite score for last 6 sessions |
| `dates[]` | String[] | dd Mon | Session dates for the history series |
| `nextStr` | Date | dd Mon yyyy | Next reassessment date |

### 5.B — Steady Stand (BalanceVision) — full result object *(31 fields)*

| Field | Type | Unit | Description |
|---|---|---|---|
| `id` | String | base36 | Unique record identifier |
| `participantId` | String | text | Participant ID / nickname |
| `age` | Integer | years | Participant age |
| `sex` | Categorical | male/female/other/'' | Participant sex (optional) |
| `participantType` | Categorical | adult/older_adult/child | Participant category |
| `supportLeg` | Categorical | left/right | Support (standing) leg |
| `trialNumber` | Integer | count | Trial index |
| `duration` | Numeric | s (1 dp) | Balance duration held |
| `terminationReason` | String | text | Why the test ended |
| `meanTorsoTilt` | Numeric | ° (1 dp) | Mean trunk deviation from vertical |
| `maxTorsoTilt` | Numeric | ° (1 dp) | Peak torso tilt |
| `sdTorsoTilt` | Numeric | ° (2 dp) | SD of torso tilt |
| `meanLateralSway` | Numeric | norm. ratio (3 dp) | Mean absolute mediolateral hip displacement |
| `maxLateralSway` | Numeric | norm. ratio (3 dp) | Max mediolateral displacement |
| `rmsLateralSway` | Numeric | norm. ratio (3 dp) | RMS of mediolateral displacement |
| `sdLateralSway` | Numeric | norm. ratio (3 dp) | SD of mediolateral displacement |
| `swayClassification` | Categorical | Low/Moderate/High | Sway band (from RMS sway) |
| `meanAngularVelocity` | Numeric | °/s (1 dp) | Mean rate of torso-tilt change |
| `peakAngularVelocity` | Numeric | °/s (1 dp) | Max instantaneous angular velocity |
| `rmsAngularVelocity` | Numeric | °/s (1 dp) | RMS angular velocity |
| `meanKneeAngle` | Numeric | ° (1 dp) | Mean support-knee angle |
| `kneeVariability` | Numeric | ° (2 dp) | SD of support-knee angle |
| `maxKneeDeviation` | Numeric | ° (1 dp) | Max knee-angle deviation from baseline |
| `meanPelvicTilt` | Numeric | ° (1 dp) | Mean absolute hip-line angle |
| `maxPelvicTilt` | Numeric | ° (1 dp) | Max hip-line angle |
| `pelvicVariability` | Numeric | ° (2 dp) | SD of hip-line angle |
| `raisedLegVariability` | Numeric | norm. (3 dp) | Positional variability of raised-leg ankle |
| `correctiveMovements` | Integer | count | Distinct balance corrections |
| `stabilityScore` | Integer | 0–100 | Composite stability score |
| `performanceLabel` | String | text | Verbal performance band |
| `timestamp` | DateTime | ISO 8601 | Time saved |

*Per-frame time-series arrays (torso tilts, hip/shoulder midpoints, angular velocities, knee/pelvic angles, raised-leg positions) drive the charts and aggregates but are **not** persisted or exported.*

### 5.C — Strength Circuit (SilverHYROX) — export payload *(18 fields)*

| Field | Type | Unit | Description |
|---|---|---|---|
| `timestamp` | DateTime | ISO 8601 | When the result was built |
| `nickname` | String | text | Participant nickname/ID |
| `gender` | Categorical | as entered | Participant gender |
| `age` | Integer | years | Participant age |
| `totalScore` | Integer | reps | Combined score (STS + Row reps) |
| `stsReps` | Integer | reps | Sit-to-Stand repetitions |
| `stsElapsed` | Numeric | s (1 dp) | Sit-to-Stand elapsed time |
| `stsAvgRepTime` | Numeric | s (2 dp) | Mean time per STS rep |
| `stsFastestRep` | Numeric | s (2 dp) | Fastest STS rep |
| `stsSlowestRep` | Numeric | s (2 dp) | Slowest STS rep |
| `stsConsistency` | Categorical | Excellent/Good/Variable/N/A | STS tempo consistency (CV band) |
| `rowReps` | Integer | reps | Seated Row repetitions |
| `rowElapsed` | Numeric | s (1 dp) | Seated Row elapsed time |
| `rowAvgRepTime` | Numeric | s (2 dp) | Mean time per Row rep |
| `rowFastestRep` | Numeric | s (2 dp) | Fastest Row rep |
| `rowSlowestRep` | Numeric | s (2 dp) | Slowest Row rep |
| `rowConsistency` | Categorical | Excellent/Good/Variable/N/A | Row tempo consistency (CV band) |
| `rowAvgReach` | Numeric | norm. ratio (2 dp) | Mean max forward reach ÷ torso length |

*A display-only fitness profile (lower-body / upper-body / consistency bands) and per-rep time/reach arrays are computed internally but not exported.*

### 5.D — Quick Reflex (Virtual BlazePod / CognitiveChallenge reaction task)

| Field | Type | Unit | Description |
|---|---|---|---|
| `reactionBest` | Integer | ms | Fastest of 3 valid attempts (primary) |
| `reactionMean` | Integer | ms | Mean of attempts |
| `reactionMedian` | Integer | ms | Median of attempts |
| `reactionSD` | Numeric | ms | SD of attempts (variability) |
| `reactionRange` | Integer | ms | Slowest − fastest |
| `reactionSlowest` | Integer | ms | Slowest attempt |
| `reactionFalseStarts` | Integer | count | Premature (red-phase) taps — impulsivity |
| `reactionAttempt1/2/3` | Integer | ms | Raw valid attempts |

### 5.E — Puzzle Focus (CognitiveChallenge visuospatial task)

| Field | Type | Unit | Description |
|---|---|---|---|
| `puzzleId` | Categorical | puzzle1–4 | Which puzzle image |
| `puzzleCompletionTime` | Numeric | s | Time to solve |
| `puzzleMoves` | Integer | count | Total tile swaps |
| `puzzleUnproductiveMoves` | Integer | count | Swaps that reduced correct placements |
| `puzzleFirstMoveAccuracy` | Categorical | Yes/No | First swap increased correct placements |

> *The full CognitiveChallenge application also produces memory (5-item recall) and calculation (serial-7) fields — 36 fields in total. As described in §3.4, these two stations are **excluded** from the FalLess ID pilot and are therefore not part of the FalLess risk model.*

---

## 6. Prototype Architecture & Feature Walkthrough

### 6.1 What this prototype is

A **single, self-contained `index.html` file** — no build step, no backend, no installation. All logic is vanilla JavaScript; charts use Chart.js from a CDN; fonts from Google Fonts; the two photographs are embedded as base64. It runs by double-clicking the file or by hosting it on any static host (GitHub Pages).

### 6.2 Screens

| Screen | Purpose |
|---|---|
| **Onboarding** | Select any of 60 synthetic residents from a dropdown; the whole form repopulates with that resident's identity, communication profile, clinical/medication risk and caregiver observations. "Save & Start Assessment" carries that resident into the session. |
| **Play & Assess** | Displays all four stations with completed results for the selected resident, including the full per-station metric panels (each with a *vs-norm* tag). Clicking a station opens an interpretation modal. |
| **Risk Profile** | The selected resident's explainable risk profile: composite score ring, six domain bars, top contributing factors, protective-factor adjustment, personalised prevention plan, and an aggregate score-history chart (6 dated sessions, latest = current). Consistency is guaranteed — the profile is derived from the same resident's station metrics and onboarding factors. |
| **Residents** | The full synthetic database as a searchable, filterable table (by name/ID and risk band). |
| **Dashboard** | Population overview: risk distribution, average-score trend, domain radar, top population predictors, urgent-review and most-improved lists. |
| **Monitoring** | Session activity: individual trajectories, completion by block, population sit-to-stand trend, and a recent-session activity log. |
| **Prevention Plans** | Card view of active intervention plans across at-risk residents. |

### 6.3 State model

A single `current` resident object drives Play & Assess and Risk Profile. To assess a different resident, the user returns to Onboarding and re-selects — this is intentional, to keep the session state coherent and prevent the profile from de-synchronising from the assessment.

### 6.4 Synthetic data

Sixty residents are generated **deterministically** from a seeded pseudo-random function, so the same resident always shows the same values across reloads. Scores are spread across all three risk bands for a realistic population demonstration.

---

## 7. Cyber-Physical AI — Technical Roadmap

The prototype is the **cyber** (digital) half of a Cyber-Physical System. This section describes how the **physical** half (sensing devices) connects during production development.

### 7.1 Definition of the loop

A Cyber-Physical System (CPS) closes a loop between the physical world and computation. In FalLess:

```
 PHYSICAL                        SENSING / EDGE AI                 CYBER (FalLess)                ACTION
 ┌──────────┐   camera / timing  ┌────────────────┐   numeric      ┌──────────────┐   plan       ┌──────────┐
 │ Resident │ ─────────────────► │ MediaPipe Pose │ ─ results ───► │ Risk-fusion  │ ──────────►  │  Staff / │
 │ performs │   (on-device)      │ Landmarker +   │  (no video)    │ model +      │  explainable │ resident │
 │ the games│ ◄───────────────── │ station engine │ ◄───────────── │ dashboards   │ ◄─────────── │  act on  │
 └──────────┘   difficulty adapts└────────────────┘   next session └──────────────┘   feedback   └──────────┘
```

The resident's physical movement is sensed, turned into numbers on the edge device, fused into a risk profile in the cyber layer, and fed back as a personalised plan and an adapted next session — a continuously closing physical↔digital loop.

### 7.2 From prototype to connected system

| Layer | Prototype (now) | Production (next) |
|---|---|---|
| **Capture** | Synthetic values | Four live apps (BalanceVision, SilverHYROX, BlazePod, CognitiveChallenge) run MediaPipe Pose Landmarker on-device |
| **Identity** | Local dropdown | Shared `residentId` across all four apps so sessions link to one person |
| **Transport** | None | Each app already POSTs a JSON result object to a Google Apps Script webhook → Google Sheet (existing capability) |
| **Ingestion** | In-memory JS objects | A backend (or serverless function) reads the four sheets/streams, joins on `residentId` + session, and computes the composite server-side |
| **Model** | Fixed placeholder weights | Weights re-tuned on the Metta pilot cohort; stored in editable config, not code |
| **Storage** | None (synthetic) | Resident records + longitudinal results in a database with PDPA-compliant access control |
| **Privacy** | N/A | Pose landmarks and derived metrics only — **video is discarded on-device and never transmitted** |

### 7.3 The single most important integration step

Today, each of the four capture apps writes to its **own** Google Sheet keyed by a free-text nickname. The fastest path to a fully automatic pipeline is:

1. Add a common **`residentId`** field to each app's participant-setup screen.
2. Point all four apps' `googleSheetsWebhookUrl` at **one shared Apps Script endpoint**.
3. That endpoint writes to one consolidated store keyed by `residentId` + session timestamp.
4. FalLess reads that store and computes the composite automatically — no manual entry.

This is a small, low-risk change per app (all four already emit `nickname`/`participantId`), not a rebuild.

### 7.4 Edge-AI and adaptive difficulty (future)

Because inference already runs on-device, the CPS loop can be closed physically: the risk profile can feed the *next* session's difficulty and station emphasis (e.g. more balance challenge for a balance-flagged resident), making the assessment adaptive rather than fixed — the literal Cyber-Physical AI vision in the proposal.

### 7.5 Privacy & data-protection architecture

- **On-device inference** — camera frames never leave the device; only numeric landmarks/metrics are produced.
- **No biometric storage** — no face images, no raw video, no identifiable imagery is retained.
- **Minimal transmission** — only the numeric result object is transmitted, and only where a webhook is configured.
- **PDPA alignment** — resident records and results held under access control; consent and communication-profile records maintained as part of onboarding.

---

## 8. Deploying to GitHub Pages

The prototype is a static site, so GitHub Pages hosts it for free. There are two ways: the web UI (no tools needed) and the command line.

### 8.1 Repository layout

```
falless-prototype/
├── index.html      ← the prototype (rename falless-prototype.html to index.html)
└── README.md       ← this file
```

> **Important:** GitHub Pages serves `index.html` by default, so **rename `falless-prototype.html` to `index.html`**. Everything else (Chart.js, fonts, images) loads from CDNs or is embedded, so no other files are needed.

### 8.2 Option A — via the GitHub website (no tools required)

1. **Create the repository.** Sign in to GitHub → click **+** (top-right) → **New repository**. Name it e.g. `falless-prototype`, set it **Public**, and click **Create repository**.
2. **Upload the files.** On the new repo page click **Add file → Upload files**. Drag in your `index.html` (renamed) and `README.md`. Click **Commit changes**.
3. **Enable Pages.** Go to **Settings** (top tab) → **Pages** (left sidebar). Under **Build and deployment → Source**, choose **Deploy from a branch**. Under **Branch**, pick **`main`** and **`/ (root)`**, then click **Save**.
4. **Wait ~1 minute.** Refresh the Pages settings screen; a green banner will show your live URL:
   ```
   https://<your-username>.github.io/falless-prototype/
   ```
5. **Share the link.** That URL is the working prototype. It updates automatically whenever you commit a new `index.html`.

### 8.3 Option B — via the command line (Git)

```bash
# 1. Create a folder and add your files (index.html renamed, README.md)
mkdir falless-prototype && cd falless-prototype
#   ... copy index.html and README.md into this folder ...

# 2. Initialise and commit
git init
git add index.html README.md
git commit -m "FalLess prototype: initial deploy"

# 3. Create the repo on GitHub first (via the website), then connect it:
git branch -M main
git remote add origin https://github.com/<your-username>/falless-prototype.git
git push -u origin main

# 4. Enable Pages: repo → Settings → Pages → Source: Deploy from a branch
#    → Branch: main / (root) → Save. Live in ~1 minute at:
#    https://<your-username>.github.io/falless-prototype/
```

### 8.4 Updating the prototype

Any time you change the HTML, just commit and push (or re-upload via the website). GitHub Pages redeploys automatically within a minute. If you don't see the change, hard-refresh the browser (Ctrl/Cmd + Shift + R) to bypass the cache.

### 8.5 Optional — a custom domain

In **Settings → Pages → Custom domain**, enter a domain you own (e.g. `falless.metta.org.sg`), then add a `CNAME` DNS record at your registrar pointing to `<your-username>.github.io`. GitHub will provision HTTPS automatically.

### 8.6 Troubleshooting

| Symptom | Fix |
|---|---|
| Blank page / 404 | Ensure the file is named exactly `index.html` and is in the repo **root** (not a subfolder). |
| Charts don't render | The page needs internet access to load Chart.js and fonts from their CDNs — check the connection; corporate firewalls may block `cdnjs.cloudflare.com`. |
| Old version still shows | Hard-refresh (Ctrl/Cmd + Shift + R); Pages caches aggressively. |
| Images missing | The photos are embedded as base64 in the HTML, so they travel with the file — if they vanish, the HTML was truncated on upload; re-upload the full file. |

---

## 9. Limitations, Governance and Responsible Use

- **Prototype only.** Synthetic data, no live devices, no persistence. Not a medical device.
- **Not clinically validated.** The composite score, domain weights, station scores (stability score, combined challenge score, cognitive metrics) are application-generated indicators, not validated clinical scales. The Petropoulou et al. (2026) tool is the validated anchor for *predictors*; the *fusion weighting* in FalLess is not yet validated.
- **Camera-derived proxies.** Balance "sway" is a body-landmark proxy, not force-platform COP. Reaction times include device latency.
- **Staff decide.** FalLess recommends; qualified staff review and approve every action before it enters a care plan.
- **Consent-first.** Deployment requires supported-decision-making consent, accessible (Easy Read) materials, and IRB/ethics approval.
- **Weights must be re-tuned** on the Metta cohort before informing any real decision.

---

## 10. References

1. Petropoulou, E., Skelton, D. A., & Finlayson, J. (2026). Predicting Injuries in Adults With Intellectual Disabilities in Supported Living: Development and Validation of Risk Assessment Tools. *Journal of Applied Research in Intellectual Disabilities, 39*(3), e70253. https://doi.org/10.1111/jar.70253

2. Lalor, A. et al. Interventions to reduce falls in community-dwelling adults with intellectual disability: a systematic review. Journal of Intellectual Disability Research (2023) doi:10.1111/jir.13066. Available from: https://onlinelibrary.wiley.com/doi/full/10.1111/jir.13066

3. Eost-Telling, C., McGarrigle, L., Shi, C., Money, A., Yang, Y., Lazo Green, K., Ahmed, S., Christie, R., Aminu, A., Delbaere, K., de Bruin, E. D., Stanmore, E., & Todd, C. (2026). Exergaming Interventions for Preventing Falls and Injurious Falls in Older People: Systematic Review and Meta-Analysis of Randomized Controlled Trials. JMIR aging, 9, e89807. https://doi.org/10.2196/89807

4. Turgeon, S., MacKenzie, A., Batcho, C. S., & D'Amour, J. (2024). Making physical activity fun and accessible to adults with intellectual disabilities: A pilot study of a gamification intervention. Journal of Applied Research in Intellectual Disabilities, 37(3), e13213. https://doi.org/10.1111/jar.13213

5. Renfro M, Bainbridge DB and Smith ML (2016) Validation of Evidence-Based Fall Prevention Programs for Adults with Intellectual and/or Developmental Disorders: A Modified Otago Exercise Program. Front. Public Health 4:261. doi: 10.3389/fpubh.2016.00261

6. Araújo , C. G. S., de Souza e Silva, C. G., Laukkanen, J. A., Singh, M. A. F., Kunutsor, S. K., Myers, J., Franca, J. F., & Castro, C. L. (2022). Successful 10-second one-legged stance performance predicts survival in middle-aged and older individuals. British Journal of Sports Medicine, 56(17), 975-980. Article bjsports-2021-105360. https://doi.org/10.1136/bjsports-2021-105360

7. **Source application system manuals** (data dictionaries transcribed in §5):
   - BalanceVision — System, Data & Analytical Manual · https://github.com/aaron-chen-angus/BalanceVision
   - Silver HYROX Home Challenge — System, Data, Scientific & Analytical Manual · https://github.com/aaron-chen-angus/SilverHYROX
   - Cognitive Performance Challenge — System, Data, Scientific & Analytical Manual · https://github.com/aaron-chen-angus/CognitiveChallenge

---

<div align="center">

**FalLess** · Republic Polytechnic × Biologic Technik × Metta Welfare Association
*Prototype for demonstration and research development. Not for clinical use.*

</div>
