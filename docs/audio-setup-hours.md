# Audio Setup Hours Model – Base Unit Justification (v1)

Purpose  
This document defines the base workload units used to calculate Audio setup hours in the BidWave logic engine. The goal is to model real technician workload in a way that is explainable, scalable, and resistant to edge cases.

Setup hours represent work to be performed, independent of crew size. Tech count is derived later.

---

## Core Principles

- Workload first, staffing second
- Setup hours are additive, not flat
- Complexity compounds time, not people
- Rush compresses time windows, not workload
- Push increases friction and therefore hours
- No audio event has zero setup cost

This model mirrors the proven LED Wall and Screen logic architecture.

---

## Base Setup Units

### Base Audio Setup

Every audio deployment includes non-zero overhead such as rack prep, console boot, patching, and signal verification.

Base unit  
- 0.5 hours flat

Rationale  
Prevents unrealistic sub-hour audio setups and reflects real A1 prep even for minimal systems.

---

### Microphones

Microphone work includes deployment, testing, gain staging, labeling, and verification.

Base unit  
- 0.25 hours per microphone (15 minutes)

Modifier  
- Multiplied by micComplexityScore

Examples  
- Handheld: approximately 15 minutes  
- Lavaliere: approximately 18 minutes  
- Headset or earworn: approximately 22 to 25 minutes  

Concept  
micSetupHours = micCount × 0.25 × micComplexityScore

---

### Zones

Zones require routing, EQ, delay alignment, and testing.

Base unit  
- 0.33 hours per zone (20 minutes)

Rationale  
Zones introduce routing and tuning overhead that scales linearly and never disappears.

---

### Playback Sources

Each playback source requires routing, gain staging, testing, and redundancy checks.

Base unit  
- 0.17 hours per source (10 minutes)

Rationale  
Playback is quick individually but accumulates with multiple sources.

---

### Monitors

Monitor systems require placement, routing, ring-out, and performer confirmation.

Base unit  
- 0.25 hours per monitor (15 minutes)

Rationale  
Monitors are deceptively time-intensive and scale with performer expectations.

---

### Live Performance Overhead

Live performance introduces rehearsal, coordination, and iteration cycles.

Flat add  
- +0.5 hours

Rationale  
Even a simple live act adds coordination overhead beyond static playback or speech.

---

### Rigging Overhead

Rigged audio systems introduce safety checks, coordination with rigging teams, lift timing, and access constraints.

Flat add  
- +1.0 hour

Rationale  
Rigging consistently adds significant friction and waiting time beyond ground-supported systems.

---

## Total Audio Setup Hours (Pre-Modifiers)

Conceptual formula  

audioSetupHours =  
- baseAudioSetup  
+ micSetupHours  
+ zoneSetupHours  
+ playbackSetupHours  
+ monitorSetupHours  
+ livePerformanceAdd  
+ riggingAdd  

This total represents raw workload before time compression or friction modifiers.

---

## Modifiers Applied After Base Workload

### Setup Time Window and Rush

Rush logic reduces available setup time, increasing crew density but not reducing workload.

Applied via  
- setupTimeWindow  
- setupTimeShortfall  
- setupRushModifier  

---

### Push Modifier

Push accounts for access difficulty, late access, overnight load-ins, or venue constraints.

Applied multiplicatively after rush logic.

---

## Safeguards

- Per-tech setup hours should not fall below approximately 2 hours
- 5/8/10 rule caps excessive crew inflation
- Labor minimums affect quoting, not workload calculation

---

## Intended Use

This model is designed to:
- Produce realistic proposals
- Scale from breakouts to live performances
- Be explainable to clients if challenged
- Be adjustable without architectural refactor

This is a working model and may be tuned as real-world data accumulates.

---

## Change Log

- v1: Initial Audio setup workload model aligned to LED Wall architecture
