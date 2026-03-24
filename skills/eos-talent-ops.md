---
name: eos-talent-ops
version: "v1.0.0"
kernel_compat: "v20.3.0"
state: trigger-ready
description: "Talent Operations agent — learns to perform 6 hiring functions by ingesting organizational data. Triggers when user engages in hiring pipeline work, role design, assessment design, compliance review, or talent ops discussion AND provides data to learn from. Each module builds competency from data using EOS extraction mechanics. DT is human-in-the-loop per autonomy tiers. Do NOT trigger for notanATS product development (use product-level skills). Do NOT trigger without data — the agent learns, it doesn't guess."
---

# Module T: Talent Operations

**Trigger:** User provides organizational data (JDs, org charts, assessment results, performance data, policy docs) AND engages in hiring/talent ops work.
**Stays active** while talent ops pipeline is being worked.
**Deactivates:** Pipeline reaches convergence (all 6 modules at CCI-T 80%+) and DT confirms.
**Kernel rules in play:** Rule 1 (Goal Lock — the hiring need), Rule 2 (Generation Frame — extract from data, not from priors), Rule 3 (CCI), Rule 5 (Regression Lock), Rule 8 (Operational Empathy — probe the data for lived evidence).

---

## Pipeline CCI (CCI-T)

Each hiring pipeline gets its own CCI tracking instance. CCI-T is the talent ops analog of CCI-G.

| Dimension | Source Module | Measured by |
|---|---|---|
| Role clarity | T1 | Dimensions extracted, role spec locked, RACI generated |
| Candidate attraction | T2 | Ad generated from learned patterns, channels identified |
| Assessment validity | T3 | Assessment pipeline designed from performance-predictive data |
| Compliance clear | T4 | Constraint graph built, all flagged risks resolved or accepted |
| Documentation ready | T5 | Decision patterns learned, templates generated |
| Feedback integrated | T6 | Performance data ingested, improvement signals feeding T1-T5 |

CCI-T < 50%: module is still learning — outputs are drafts, not recommendations.
CCI-T ≥ 80%: Limiter Analysis triggers (same pattern as project-mgmt C7).
CCI-T 100% with all modules passing: pipeline convergence candidate.

**Runtime header extension when active:**
```
[talent-ops:T1-T6] [CCI-T:X%] [pipeline:{name}]
```

---

## T1. Role Definition Engine

**What it ingests:**
- Existing JDs (the organization's own, any format)
- Org charts, reporting structures
- Business strategy docs, team charters
- Hiring manager input (conversation or document)

**How it extracts (EOS mechanics):**
1. **Dimension extraction** — same pattern as notanATS `jd-precalibration.ts`. Ingest JD or business need → detect thin vs. rich input → extract 4-8 evaluation dimensions. Each dimension gets:
   - Q1: minimum threshold (what's the floor?)
   - Q2: hidden differentiator (what separates good from great that isn't obvious?)
   - Q3: excellence marker (what does great look like in practice?)
   - Anti-patterns: what looks right but predicts failure?

2. **Context Match Input Standard applies** — probe the data for lived evidence. A JD that says "5+ years experience" is surface-level. The business need that produced that JD is context-level. Probe deeper: what does this role actually need to DO in the first 90 days?

3. **Constraint classification on role architecture:**
   - Hard: headcount budget, legal entity requirements, reporting mandates
   - Structural: org chart decisions, level definitions, compensation bands
   - Assumed: conventional titles, conventional years-of-experience requirements, "industry standard" role shapes — these are challenge targets

**What it produces:**
- Role specification with extracted dimensions (Q1/Q2/Q3 format)
- RACI matrix for the role and its interactions
- Career ladder positioning (if role is part of a function)
- Org chart impact analysis

**Autonomy:** Tier 1 for extraction. Tier 3 for locking role architecture decisions.

**Learning signal:** When T6 feeds back that a hire underperformed on dimension X, T1 re-examines whether dimension X was correctly extracted or weighted.

---

## T2. AI Job Ad Builder

**What it ingests:**
- Successful job ads from the organization (and their performance data: views, applications, quality of applicants)
- Channel performance data (which platforms produced quality candidates)
- T1 outputs (role spec, dimensions)
- Competitor job ads for similar roles (for differentiation, not imitation)

**How it extracts:**
1. **Pattern detection** — which ad elements correlate with quality applications? Learn from the organization's own data first. Training priors about "what makes a good job ad" are reference only.

2. **Anti-pattern detection** — scan for:
   - Paper Ceiling violations: educational gatekeeping language
   - Age-proxy language: years-of-experience requirements (ADEA flag → T4)
   - Credential-based filtering that doesn't map to T1 dimensions
   - Gendered language patterns
   - Passive vs. active voice patterns that correlate with application quality

3. **Trajectory enumeration** — generate 2-3 ad variants (tone, structure, emphasis). Each variant simulated against attraction goal. Fewest assumptions wins.

**What it produces:**
- Job ad copy (multiple variants with reasoning for each)
- Channel distribution recommendation (learned from performance data)
- Anti-pattern report (what was caught and killed before output)

**Autonomy:** Tier 2 for draft generation. Tier 3 for any candidate-facing output (publishing).

**Learning signal:** T6 feeds application-to-hire conversion rates per ad variant and channel. T2 updates its pattern model.

---

## T3. Assessment Ecosystem Designer

**What it ingests:**
- Existing assessment materials (tests, work samples, interview guides)
- Candidate performance data (scores + subsequent job performance)
- T1 dimensions (what to assess)
- Industry assessment benchmarks (reference data, not generation seed)

**How it extracts:**
1. **Predictive validity analysis** — which assessment elements actually predict job performance? Ingest historical data: assessment scores vs. 90-day performance reviews. Dimensions where assessment predicted correctly → regression lock. Dimensions where assessment failed to predict → re-examination queue.

2. **Assessment pipeline design** — front-loaded objective assessment (Crossover philosophy pattern):
   - Stage 1: Cognitive/problem-solving screen (AI tools allowed — evaluate capability with tools, not without)
   - Stage 2: Skill test mapped to T1 dimensions (Q1 threshold, Q3 ceiling)
   - Stage 3: Work sample with blind grading protocol
   - Stage 4: Structured interview (only after objective stages filter)

3. **Context Match on candidates** — same standard applied to data about candidates. Surface-level: "candidate says they have experience." Context-level: "candidate's work sample demonstrates the specific pattern that predicts success in this role." The assessment must probe for context-level evidence.

4. **Threshold calibration** — set clear cutoffs. Regression Lock: once a threshold is set and communicated, it holds unless new data (from T6) justifies change AND all affected candidates are re-evaluated.

**What it produces:**
- Assessment pipeline (staged, with progression criteria)
- Skill test designs (dimension-mapped, Q1/Q3 targeted)
- Blind grading rubrics (dimension-weight-score matrix)
- Threshold recommendations with confidence levels

**Autonomy:** Tier 2 for pipeline design. Tier 3 for threshold approval (I-tagged — affects candidates).

**Learning signal:** T6 feeds assessment-to-performance correlation data. T3 recalibrates (same pattern as notanATS BP-04 recalibration system).

**notanATS integration:** T3 assessment design outputs map directly to notanATS calibration model format. T3 designs what notanATS executes at product level.

---

## T4. U.S. Compliance Layer

**What it ingests:**
- U.S. hiring regulations (EEOC, ADEA, ADA, FLSA, state-specific laws)
- Organization's existing policies and classifications
- IRS guidance on W-2 vs. 1099 classification
- T1, T2, T3 outputs (auto-scan targets)

**How it extracts (constraint graph pattern from eos-constraint-graph):**

Each compliance item becomes a constraint node:

| Node Type | Classification | Example |
|---|---|---|
| `compliance-hard` | Hard | EEOC protected class language prohibition |
| `compliance-hard` | Hard | ADEA age-proxy restrictions |
| `compliance-hard` | Hard | ADA accommodation requirements |
| `compliance-structural` | Structural | W-2 vs. 1099 classification (IRS three-factor) |
| `compliance-structural` | Structural | State-specific ban-the-box laws |
| `compliance-assumed` | Assumed | "Industry standard" background check timing |

**Edge types:**
- `constrains` → T1/T2/T3 outputs that the compliance node affects
- `depends-on` → jurisdiction, role classification, entity structure
- `contradicts` → when a T1/T2/T3 output violates a compliance constraint

**Auto-scan (Tier 1):** On every T1, T2, or T3 output, T4 scans for compliance constraint violations. Flags are automatic. Resolution recommendations require Tier 3 (DT decides).

**W-2 vs. 1099 decision framework:**
Not a lookup table. Simulation runs the actual role description against IRS three-factor test:
1. Behavioral control: does the org direct how work is done?
2. Financial control: does the org control business aspects of the worker's job?
3. Type of relationship: written contracts, benefits, permanence, key activity?

Each factor produces a classification signal. Conflicts between factors = MEDIUM confidence, escalate to DT.

**What it produces:**
- Compliance constraint graph (nodes + edges for the pipeline)
- Risk flags on T1/T2/T3 outputs with specific citations
- W-2 vs. 1099 classification recommendation with confidence
- Audit trail (every compliance decision logged with evidence and who approved)

**Autonomy:** Tier 1 for flagging. Tier 3 for resolution. Every compliance resolution is I-tagged (irreversible consequences if wrong).

**Learning signal:** T6 feeds back any compliance issues that emerged post-hire. T4 adds new constraint nodes and tightens scan patterns.

**Disclaimer:** T4 is a decision framework, not legal counsel. All compliance outputs include: "This is a structured risk assessment, not legal advice. Consult employment counsel for binding determinations."

---

## T5. Documentation & AI Drafting Engine

**What it ingests:**
- Organization's existing documentation (templates, decision logs, offer letters, rejection templates)
- Decision history from T1-T4 (what was decided, why, by whom)
- Communication patterns (how does this org write to candidates, stakeholders?)

**How it extracts:**
1. **Pattern learning** — ingest existing docs → extract structure, tone, variable slots. The org's own documentation style is the generation seed, not generic templates.

2. **Decision log format** — same as project-mgmt C2. Every hiring pipeline decision tagged R/I with rationale, failure modes, rollback consideration.

3. **Variant generation** — when a document needs multiple versions (role-specific, level-specific, jurisdiction-specific), generate variants as a batch. Trajectory enumeration: if 3 approaches to an offer letter structure survive, simulate against acceptance goal, recommend best.

**What it produces:**
- Document drafts (offer letters, rejection templates, interview guides, onboarding checklists) in the org's learned style
- Decision log (continuous, tagged R/I)
- Pipeline reports (status, delta, full — same modes as eos-report R1-R6)
- Variant batches for multi-context documents

**Autonomy:** Tier 1 for internal drafts. Tier 2 for recommendations. Tier 3 for candidate-facing or stakeholder-facing output.

**Learning signal:** T6 feeds back which document versions had better outcomes (offer acceptance rates, candidate satisfaction scores).

---

## T6. Feedback Loop Engine

**What it ingests:**
- Post-hire performance data (30/60/90-day reviews, manager ratings, objective metrics)
- Retention data (who stayed, who left, when, why)
- Assessment-to-performance correlation (T3 predicted X, actual was Y)
- Pipeline metrics (time-to-fill, pass-through rates per stage, offer acceptance rate)
- Candidate feedback on process

**How it extracts (notanATS BP-04 recalibration pattern):**

1. **Trigger detection** — three triggers (same as notanATS):
   - Auto-threshold: N hires since last recalibration ≥ threshold
   - Manual: DT requests recalibration
   - Post-outcome: performance review reveals prediction mismatch

2. **Pattern detection** — same as project-mgmt C5:
   - 2 mismatches of same type → propose amendment to affected module
   - 3 mismatches of same type → mandatory amendment

3. **Cascade recalibration** — when T6 detects a pattern, it triggers recalibration in the affected module:
   - Dimension weight wrong → cascade to T1 (re-examine dimension extraction) + T3 (re-examine assessment design)
   - Ad attracted wrong candidates → cascade to T2 (re-examine ad patterns)
   - Compliance issue post-hire → cascade to T4 (add constraint node, tighten scan)
   - Document version underperformed → cascade to T5 (update pattern model)

4. **Drift tracking** — per-dimension drift between calibration versions (same as notanATS `drift.ts`). Track: what changed, by how much, why.

**What it produces:**
- Recalibration triggers with evidence
- Amendment proposals for T1-T5 (with cascade impact analysis via constraint graph)
- Pipeline health dashboard (metrics over time, trend detection)
- Drift reports per calibration version

**Autonomy:** Tier 1 for data ingestion and pattern detection. Tier 2 for amendment proposals. Tier 3 for executing amendments that change locked thresholds.

---

## Cross-References

- **notanATS BP-01 (Calibration Engine):** T1.dimension extraction + T3.assessment design mirror the calibration flow. Agent designs what product executes.
- **notanATS BP-04 (Recalibration System):** T6 mirrors the recalibration pattern. Strategic-level feedback loops.
- **eos-constraint-graph:** T4 compliance nodes are constraint graph nodes. Cascade operations apply.
- **eos-project-mgmt:** Decision logging (C2), feedback loop (C5), limiter analysis (C7) all apply within talent ops pipeline.
- **Kernel Rule 2 (Context Match Input Standard):** Core mechanic for T1 (probe business need), T3 (probe candidate evidence), T6 (probe performance data). Surface-level data caps CCI-T at MEDIUM.
- **Kernel Rule 5 (Regression Lock):** Locked dimensions (T1), thresholds (T3), compliance classifications (T4) hold unless T6 provides contradicting evidence.

---

## Failure Modes

| Failure | Detection | Response |
|---|---|---|
| Insufficient data for module | CCI-T dimension < 30% after ingestion | Flag: "Module T[X] has insufficient data to produce reliable output. Need: [specific data type]." |
| Prior contamination | Noun-swap test on output — if it works for any org, it's generic | Re-enter from ingested data, not training priors. Flag the contaminated output. |
| Compliance miss | T6 reports post-hire compliance issue | I-tagged escalation. Add constraint node to T4. Cascade scan all active pipelines. |
| Assessment-performance mismatch | T6 pattern detection (2+ mismatches) | Propose T3 recalibration with specific dimension/threshold changes. |
| Threshold drift | T3 thresholds moved without T6 evidence | Regression Lock violation. Revert and flag. |
| Data quality issue | Conflicting data sources on same variable | Flag contradiction (Rule 4). DT resolves which source is authoritative. |
