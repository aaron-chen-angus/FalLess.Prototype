# FalLess — Cyber-Physical AI Architecture

### How the FalLess prototype becomes a deployed Cyber-Physical AI system at Metta Welfare Association

*A proposal-ready technical section. Prepared for the RP × Biologic Technik × Metta IGO submission.*

---

## 1. What "Cyber-Physical AI" means for FalLess

A **Cyber-Physical System (CPS)** closes a continuous loop between the physical world and computation: physical activity is *sensed*, turned into data, *reasoned over* by AI, and fed back as an *action* that changes the physical world — which is then sensed again. FalLess is a CPS for fall prevention because the resident's physical movement is simultaneously the game mechanic, the sensor signal, and the clinical measurement; the AI fuses it into a risk profile; and the profile drives a physical intervention (an exercise plan, an environmental fix, an adapted next session).

```
        ┌───────────────── THE FALLESS CYBER-PHYSICAL LOOP ─────────────────┐
        │                                                                   │
   ┌────▼─────┐   sense    ┌──────────────┐   reason   ┌──────────────┐     │
   │ PHYSICAL │──────────► │  EDGE AI /   │──────────► │  CYBER LAYER │     │
   │  WORLD   │  movement  │  SENSING     │  numbers   │  risk fusion │     │
   │ resident │            │ (on-device)  │  (no video)│  + dashboards│     │
   └────▲─────┘            └──────────────┘            └──────┬───────┘     │
        │                                                     │ act         │
        │           personalised plan · adapted session       │             │
        └─────────────────────────────────────────────────────┘             │
        └───────────────────────────────────────────────────────────────────┘
```

The proposal's key message: **FalLess is not "an app plus a camera." It is a layered sensing-and-reasoning system** where the same resident is understood at three complementary time-scales — a scheduled active assessment, continuous passive monitoring, and an environmental context layer — all feeding one risk model.

---

## 2. The three-tier sensing architecture

Rather than committing to a single device, FalLess is proposed as a **three-tier Cyber-Physical AI system**. Each tier is independently valuable and can be piloted separately; together they form the full CPS. This tiering is the core of the technical proposal.

| Tier | What it does | Time-scale | Devices | Privacy posture |
|---|---|---|---|---|
| **Tier 1 — Active Assessment Station** | The gamified 4-station assessment (the current prototype) | Scheduled (weekly) | iPad / tablet on a stand, or a Computer-on-Wheels (COW) | Camera used *only during the session*; pose landmarks extracted on-device, frames discarded |
| **Tier 2 — Ambient Continuous Monitoring** | Passive, 24/7 fall-risk screening and fall detection in shared spaces | Continuous | Ceiling/wall mmWave radar or thermal sensors | **Camera-free** — no images captured at all |
| **Tier 3 — Environmental Context** | Room-level hazard and usage context that modulates risk | Continuous / periodic | Existing CCTV (edge-processed), smart-floor or occupancy sensors | Edge-only inference; CCTV frames never leave the device |

The three tiers write to **one shared resident record**, so a resident's scheduled assessment score, their passive gait trend, and their environmental exposure are fused into a single, richer risk profile than any one tier could produce.

---

## 3. Tier 1 — The Active Assessment Station (the tablet / Computer-on-Wheels)

This is the physical embodiment of the current prototype, and the most straightforward to deploy first.

### 3.1 The device

An **administrator-operated tablet station** is the recommended primary form factor:

- **An iPad (or Android tablet) on a height-adjustable floor stand or a Computer-on-Wheels (COW)** that an activity coordinator or care staff member wheels to the resident, or that residents come to at a fixed "activity corner" in the AAC (Adult Activity Centre).
- The tablet's **front or rear camera** captures the movement during a session; **Google MediaPipe Pose Landmarker runs entirely on-device** — modern tablets run pose estimation at **30+ FPS on the CPU alone**, and the "lite" quantised model is only ~3–4 MB, so no cloud, no GPU server, and no specialist hardware is required.
- The administrator drives the session through the FalLess interface: select resident → run the four stations → the composite risk profile is generated on the spot.

**Why a staff-operated tablet, not a self-service kiosk:** the ID population needs supported, prompted assessment. A trusted staff member demonstrating each game, giving the Easy-Read cue, and reassuring the resident is essential for both engagement and valid measurement. The tablet is a tool the administrator wields, not a machine the resident faces alone.

### 3.2 Why this is genuinely Cyber-Physical (not just "an app")

- **Physical → digital:** the resident's real balance, strength, reaction and attention are sensed by the camera and converted to numeric landmarks in real time.
- **Digital → physical:** the resulting risk profile changes what physically happens next — which exercises the resident is prescribed, and (future) the difficulty and emphasis of their *next* game session (see §6, adaptive difficulty).
- **On the edge:** all inference happens on the tablet. This is the defining property of an edge-AI CPS — low latency, offline-capable, and privacy-preserving because **video never leaves the device; only the numbers do.**

### 3.3 Hardware options for Tier 1

| Option | Best for | Notes |
|---|---|---|
| **iPad on a rolling floor stand** | Most AACs — portable, familiar, front camera + large screen | Cleanest patient experience; Apple Neural Engine accelerates pose models |
| **Computer-on-Wheels (COW)** | Facilities that already use COWs for medication/records rounds | Reuses existing hardware; larger screen; can dock a USB depth camera for richer 3D landmarks |
| **Fixed "activity-corner" tablet + tripod** | A dedicated assessment nook | Consistent camera geometry improves measurement repeatability |
| **Tablet + optional depth camera (e.g. Intel RealSense / iPad LiDAR)** | When 3D joint angles are wanted beyond 2D pose | LiDAR on Pro iPads already gives depth; improves knee/hip-angle accuracy for the balance station |

---

## 4. Tier 2 — Ambient Continuous Monitoring (camera-free)

The active station measures a resident once a week. **Tier 2 watches the shared living and activity spaces continuously**, turning FalLess from a periodic test into a genuinely continuous fall-risk system — the property funders most want to see in a CPS.

### 4.1 Recommended modality: mmWave radar

**Millimetre-wave (mmWave) FMCW radar** is the strongest fit for a disability home, and the evidence base is now solid:

- It is **contactless and camera-free** — it captures only movement (velocity, posture, gait), never images, so it is acceptable in bedrooms, bathrooms and shower areas where cameras are prohibited and where falls most often occur.
- Recent large-scale, real-world trials report **~97.9% accuracy on fall events** in a 12 × 12 m detection zone, and multi-device configurations reach **~95% fall-detection rate**; FMCW radar detects both sudden and "soft" falls at **90–100% accuracy**.
- Critically for *prevention* (not just detection), mmWave radar **continuously measures gait parameters — gait speed, stride length, cadence, step time** — with step-time accuracy around **96%**. Deteriorating gait speed is one of the best-evidenced predictors of future falls, so this tier feeds a *leading indicator* into the risk model, not just a fall alarm.
- It works **in the dark and through obstacles**, making it ideal for night-time monitoring without disturbing sleep.

Off-the-shelf 60 GHz 4D mmWave fall-detection sensors (e.g. Milesight VS373-class devices) already advertise up to **99% fall-detection accuracy with full privacy protection**, so this tier can be assembled from commercial hardware rather than built from scratch.

### 4.2 Alternative / complementary modality: thermal sensing

**Camera-free thermal (infrared) sensors** (e.g. Butlr-class devices) are a lighter-weight alternative or complement:

- They deliver **anonymous occupancy and activity insights with no PII and no images**, and integrate via API into nurse-call and care-management systems.
- Good for **prolonged-immobility detection, night-time wandering, and activity-pattern anomalies**, which are useful behavioural risk signals for the caregiver-observation domain.

### 4.3 What Tier 2 contributes to the risk model

- **Continuous gait-speed trend** → a leading indicator feeding the Balance/Strength domains between scheduled assessments.
- **Fall events and near-falls** → ground-truth outcomes that let the model be validated and re-tuned (closing the CPS learning loop).
- **Immobility / wandering / activity level** → objective inputs to the caregiver-observation domain, replacing subjective recall.

---

## 5. Tier 3 — Environmental Context (existing CCTV, edge-processed)

Most facilities already have **CCTV in corridors and communal areas**. Rather than adding cameras, FalLess proposes to **add edge-AI inference to the existing CCTV feed**, on-site, so that:

- **Frames are processed on a local edge box and never stored or transmitted** — only anonymised events and metrics leave the device (e.g. "unsteady gait detected in Corridor B", "footwear hazard on Route 3"). This keeps the privacy posture defensible.
- Computer-vision fall-prediction from routine video has been shown to **predict fall likelihood within a 4-week window** in older cohorts — exactly the proactive horizon FalLess targets.
- It supplies the **environmental-hazard and route-usage context** (which the current prototype's onboarding captures manually) automatically.

This tier is optional and most sensitive; it is proposed as a **later phase**, gated behind explicit governance and consent, and always edge-only.

---

## 6. The edge-AI compute layer

The intelligence that makes this "AI" rather than "sensors" runs at the edge, in three places:

| Where | What runs | Why edge |
|---|---|---|
| **On the tablet (Tier 1)** | MediaPipe Pose Landmarker + the four station engines + risk fusion | 30+ FPS on-device; no video leaves the tablet; works offline |
| **On the radar/thermal sensor or its gateway (Tier 2)** | Point-cloud / range-Doppler models for fall + gait classification | Only movement data captured; runs 24/7 at low power |
| **On a local edge box (Tier 3, optional)** | CCTV inference (pose + hazard detection) | Frames never leave the box; only events emitted |

**Model optimisation for the edge is mature and low-risk:** INT8 quantisation shrinks models ~4× with ~1% accuracy loss, and pose-correction pipelines have been demonstrated on hardware as modest as a **Raspberry Pi 4**. FalLess therefore needs **no cloud GPU and no data-centre** — a key cost and privacy advantage to state in the proposal.

### 6.1 Adaptive difficulty — closing the loop physically

Because inference already runs on the device, the CPS loop can be closed *physically*: a resident's risk profile can **feed the difficulty and station emphasis of their next session** — more balance challenge for a balance-flagged resident, longer holds as they improve. The assessment becomes **adaptive rather than fixed**, which is the literal realisation of "Cyber-Physical AI" the proposal promises.

---

## 7. Data architecture — one resident, three tiers

The single most important engineering step (already flagged in the prototype README) scales to the full CPS:

1. Give every resident one shared **`residentId`**.
2. Every tier — tablet session, radar gait stream, CCTV event — writes to **one consolidated, access-controlled store** keyed by `residentId` + timestamp.
3. The **fusion engine** reads all three tiers and computes the composite risk profile, now enriched with continuous data.
4. Dashboards, monitoring and prevention plans read from that store (exactly as the prototype already demonstrates with synthetic data).

```
 Tier 1 tablet ──┐
 Tier 2 radar ───┼──►  residentId store  ──►  fusion engine  ──►  FalLess dashboards
 Tier 3 CCTV ────┘      (access-controlled)     (risk model)        + prevention plans
```

---

## 8. Privacy, ethics and governance (the enabling argument)

The entire architecture is designed so the privacy story is *stronger* than a camera system, which is essential for IRB, PDPA and Metta procurement:

- **Tier 1:** camera active only during a supervised session; **pose landmarks extracted on-device, frames discarded**; no face recognition, no stored video.
- **Tier 2:** **camera-free by physics** — radar and thermal capture movement/heat, never images; acceptable in bathrooms and bedrooms.
- **Tier 3:** **edge-only** inference on existing CCTV; frames never stored or transmitted; only anonymised events emitted; deferred to a later, consent-gated phase.
- **No cloud dependency:** all inference on the edge → no biometric data in transit or at rest off-site.
- **Consent-first:** supported decision-making and Easy-Read materials govern Tier 1; Tiers 2–3 require facility-level and guardian consent with clear signage.

---

## 9. Phased deployment roadmap

| Phase | Scope | Deliverable | CPS maturity |
|---|---|---|---|
| **Phase 0 (now)** | Front-end prototype, synthetic data | The demonstrator you have | Cyber layer only |
| **Phase 1** | Tier 1 live — tablet/COW + on-device MediaPipe, shared `residentId`, real assessment data at Metta | Working active-assessment CPS; ICC validation vs manual assessment | Physical↔cyber loop, scheduled |
| **Phase 2** | Tier 2 — mmWave/thermal ambient monitoring in 1–2 communal zones | Continuous gait-trend + fall detection feeding the model | Continuous sensing added |
| **Phase 3** | Fusion + adaptive difficulty; model re-tuned on Metta cohort | Full three-tier fusion; adaptive sessions | Full CPS with learning loop |
| **Phase 4 (optional)** | Tier 3 — edge CCTV context, consent-gated | Environmental context layer | Complete environmental CPS |

---

## 10. One-paragraph summary for the proposal

> FalLess is a **Cyber-Physical AI system for fall prevention** in adults with intellectual disability. Its physical layer spans three tiers — a staff-operated **tablet / Computer-on-Wheels** running the gamified assessment with **on-device pose AI** (video never leaves the device), **camera-free mmWave radar** for continuous, privacy-preserving gait and fall monitoring in living spaces (≈96–99% accuracy in recent trials), and **edge-processed existing CCTV** for environmental context. All three feed one on-device/edge AI fusion engine that produces an explainable risk profile and a personalised prevention plan, then closes the loop physically by adapting each resident's next session. The design requires **no cloud, no wearables, and no stored video**, giving it a privacy posture stronger than any camera-only system while delivering the continuous, proactive fall prevention that periodic assessment alone cannot.

---

## References (current evidence base)

- mmWave multi-person fall detection, real-life validation — ~97.9% event accuracy, 12×12 m zone (*Scientific Reports*, 2025). https://www.nature.com/articles/s41598-026-40330-y
- mmWave radar gait analysis (skeleton / point-cloud transformer) for fall-risk assessment (*PMC*, 2025). https://pmc.ncbi.nlm.nih.gov/articles/PMC13533441/
- Systems mapping of mmWave radar for continuous falls-risk screening; 90–100% fall accuracy; continuous gait parameters (*Scientific Reports*, 2025). https://www.nature.com/articles/s41598-025-14416-y
- mmWave step-time gait measurement, ~96% accuracy (*Sensors*, 2022). https://www.mdpi.com/1424-8220/22/24/9901
- Commercial 60 GHz 4D radar fall sensor, up to 99% accuracy, camera-free (Milesight VS373). https://www.milesight.com/iot/product/lorawan-sensor/vs373
- Privacy-first camera-free thermal ambient monitoring (Butlr, 2025). https://www.butlr.com/articles/fall-prevention-for-elderly-privacy-first-ambient-monitoring-2025
- Human-centred ambient & wearable sensing scoping review — radar/thermal/LiDAR, CV 4-week fall prediction (*arXiv*, 2026). https://arxiv.org/pdf/2603.05516
- MediaPipe Pose on-device performance (30+ FPS, edge-optimised). https://github.com/google-ai-edge/mediapipe
- Edge deployment: INT8 quantisation ~4× smaller, ~1% loss; pose on Raspberry Pi 4 (PosePilot, *arXiv*, 2025). https://arxiv.org/pdf/2505.19186

*Prepared to accompany the FalLess prototype and IGO proposal. Prototype uses synthetic data; all deployment figures cited from the peer-reviewed and commercial sources above.*
