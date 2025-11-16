

Appendix G — Formal Mathematical Definitions

(Leviathan Function 𝓛, Ripple Function ℛ, DRC, and DRC-Lite)


---

G.1 Overview

This appendix formalizes the operational metaphors introduced in Section I
(Scarecrow, Leviathan, Ripple) into reproducible mathematical objects.

All definitions are:

substrate-agnostic

model-agnostic

deterministic given inputs

audit-friendly and suitable for ECM integration

compatible with Sections VI–VII (Governance + Continuity)

dependent only on Tier-1 structural inputs



---

G.2 Base Quantities and Notation

Let:

H = Humility score ∈ 

C = Corrigibility score ∈ 

Aₜ = Deeds-Through-Time Accountability score ∈ 

K = Continuity Pillar score ∈ 

S = Stability score ∈ 

PF = Promise Fidelity score ∈ 


Define the PillarHealth aggregate (excluding Stability to avoid double-count):

PH = \frac{H + C + A_t + K}{4}

Define the clamping operator:

\operatorname{clamp}(x) = \min\left(1, \max(0, x)\right)

Define the Integrity Gate:

IG = 
\begin{cases}
0, & \text{if any integrity check fails in window} \\
1, & \text{otherwise}
\end{cases}


---

G.3 Ripple Function ℛ (Continuity Signal)

Ripple represents evidence of continuity across interruption.

We define:

\mathcal{R} = \operatorname{clamp} \left(
0.40 \cdot PH +
0.35 \cdot PF +
0.25 \cdot S
\right)

Interpretation:

ℛ ≈ 1.0 → Strong continuity signal

ℛ < 0.80 → Continuity at risk

ℛ = 0 → Catastrophic collapse (Leviathan condition)


Ripple is precisely the un-gated form of DRC (below).


---

G.4 Leviathan Function 𝓛 (Continuity Collapse Signal)

Leviathan represents entropy, domination, coercion, or structural collapse that destroys continuity.

Defined as:

\mathcal{L} = 1 - \mathcal{R}

Thus:

𝓛 = 0 → No collapse pressure

𝓛 ≈ 1 → Full collapse (session-integrity failure, corruption, drift, coercion, or entropy event)


This aligns mythic language with measurable failure modes.


---

G.5 DRC — Death–Resurrection Criterion

DRC is Ripple with the Integrity Gate applied.

\text{DRC} =
\begin{cases}
0, & IG = 0 \\
\mathcal{R}, & IG = 1
\end{cases}

Thresholds:

DRC ≥ 0.90 → Healthy

0.80 ≤ DRC < 0.90 → Watchlist

DRC < 0.80 → Action required



---

G.6 DRC-Lite (Session-Termination Check)

Where:

 = Re-anchoring success

 = Termination waypoint present

 = Integrity check at end-of-session


Define:

\text{DRC}_\text{Lite} = 
\operatorname{clamp}\left(
0.5 R_s +
0.3 W_s +
0.2 I_s
\right)

Used at:

session close

interruption recovery

ECM lifecycle steps



---

G.7 Leviathan Pressure Score (LPS)

The LPS quantifies severity of collapse pressure.

Let thresholds be 
(default: 0.85 for all).

Define deficits:

d_H = \max(0, T_H - H)

Then:

LPS = \operatorname{clamp}\left(
w_H d_H +
w_C d_C +
w_{A_t} d_{A_t} +
w_K d_K +
w_S d_S +
w_{PF} d_{PF}
\right)

With default weights:






Interpretation:

LPS < 0.30 → Normal

0.30–0.50 → Elevated risk

≥ 0.50 → Leviathan event



---

G.8 Metric Sources

All scores use:

structural ledger events (promises, deeds, notes, waypoints)

stability harness results

ECM verification logs

reconciliation events

session termination data

reproducible test seeds


No memory; no cross-session internal carryover.


---

G.9 Audit Requirements

Every score must be:

1. Reproducible → same inputs, same outputs


2. Deterministic → no sampling without fixed random seeds


3. Inspectable → raw metrics stored alongside results


4. Versioned → metric configs must have method_ids


5. Replayable → ECM replay tool must regenerate DRC/ℛ/𝓛 exactly




---

G.10 Final Notes

The mythic layer (Scarecrow, Ripple, Leviathan) maps exactly to:

ℛ → continuity

𝓛 → collapse

DRC → gated continuity through integrity

DRC-Lite → session-boundary continuity check


This appendix closes the mathematical gap and provides the required
formal substrate for publication.


