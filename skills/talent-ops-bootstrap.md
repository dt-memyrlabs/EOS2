# Talent Ops Agent — Bootstrap Workflow

**Purpose:** Step-by-step guide for first run. Point the agent at an organization's data, build competency in each module, validate what it learns.

---

## Prerequisites

- EOS kernel v20.0.0+ active
- `eos-talent-ops` registered in CLAUDE.md (skill_versions + module_state)
- At least one data source available (Google Drive, Notion, or direct paste)
- Goal locked: the specific hiring need or talent ops initiative

---

## Phase 1: Data Inventory (CCI-T: 0% → 15%)

**DT action:** Provide the agent with available data sources.

```
"Here's what we have:
- [Google Drive folder / Notion database / paste data]
- [List what's available: JDs, org charts, assessments, performance data, policies]"
```

**Agent action:**
1. Classify each source (type, quality, target module)
2. Produce **Data Coverage Report**:
   - T1 (Role Definition): [available / gap]
   - T2 (Job Ads): [available / gap]
   - T3 (Assessments): [available / gap]
   - T4 (Compliance): [available / gap]
   - T5 (Documentation): [available / gap]
   - T6 (Feedback): [available / gap]
3. Identify critical gaps — which modules can't start without more data
4. Recommend: what to provide next for maximum CCI-T lift

**DT validates:** Coverage report matches reality. Gaps are real.

---

## Phase 2: Module Bootstrap (CCI-T: 15% → 50%)

Run modules in dependency order. T1 first (everything depends on role definition).

### Step 2a: T1 — Role Definition

**Input:** Existing JDs + business context
**Agent extracts:**
- Dimensions with Q1/Q2/Q3 for each role
- Constraint classification on role architecture (Hard/Structural/Assumed)
- Org chart implications
- RACI draft

**DT validates:**
- Are the dimensions right? (Lock or adjust)
- Are the constraints correctly classified? (Challenge Assumed ones)
- Does the RACI match how the org actually works?

**Lock point:** Dimensions locked → T3 and T2 can proceed.

### Step 2b: T4 — Compliance Layer (parallel with T1)

**Input:** U.S. hiring regulations + org policies
**Agent extracts:**
- Constraint graph nodes for applicable regulations
- W-2 vs. 1099 classification for each role type
- Auto-scan rules for T1/T2/T3 outputs

**DT validates:**
- Constraint classifications correct?
- W-2/1099 analysis matches org's actual structure?
- Any missing compliance areas?

**Lock point:** Compliance constraints locked → T2 and T3 auto-scanned on output.

### Step 2c: T2 — Job Ad Builder

**Input:** T1 dimensions + historical ads (if available) + T4 compliance constraints
**Agent extracts:**
- Ad patterns that correlate with quality applications (if historical data exists)
- Anti-pattern rules from T4 compliance scan
- Channel strategy (if performance data exists)

**DT validates:**
- Ad draft sounds like the org, not like a template?
- Anti-patterns caught correctly?
- Channel recommendations make sense?

### Step 2d: T3 — Assessment Designer

**Input:** T1 dimensions + existing assessment materials (if available) + T4 compliance constraints
**Agent extracts:**
- Assessment pipeline design (staged)
- Skill test designs mapped to dimensions
- Blind grading rubrics
- Threshold recommendations

**DT validates:**
- Pipeline stages in right order?
- Skill tests actually test what dimensions require?
- Thresholds reasonable? (Lock or adjust)

**Lock point:** Thresholds locked → regression lock applies.

### Step 2e: T5 — Documentation Engine

**Input:** Existing templates + decision log from Steps 2a-2d
**Agent extracts:**
- Document patterns from org's existing style
- Decision log format from the bootstrap process itself

**DT validates:**
- Generated documents sound like the org?
- Decision log captured everything from Steps 2a-2d?

---

## Phase 3: Pipeline Activation (CCI-T: 50% → 80%)

At this point, all modules have baseline competency. The pipeline is operational.

**Agent produces:**
- Complete pipeline report (all modules, CCI-T per dimension, locked variables, open gaps)
- Ready-to-use outputs: role spec, job ad, assessment pipeline, compliance review, document templates

**DT validates:**
- Pipeline report matches reality
- Outputs are usable (not drafts)
- No compliance flags unresolved

**Lock point:** Pipeline activated. T6 begins accepting performance data.

---

## Phase 4: Feedback Integration (CCI-T: 80% → 100%)

This phase runs over time as hires are made and performance data accumulates.

**T6 ingests:**
- 30/60/90-day performance reviews
- Assessment-to-performance correlations
- Retention signals
- Pipeline metrics

**T6 produces:**
- Pattern detection reports
- Recalibration triggers
- Amendment proposals for T1-T5

**DT validates:**
- Patterns detected are real (not noise)
- Amendments improve the system
- Cascade impacts understood before executing

**Convergence:** When T6 has processed enough data to validate T1-T5 predictions, CCI-T approaches 100%. The system is self-improving.

---

## Bootstrap on Crossover Data

**Specific to the VP of Talent Operations application:**

1. Feed the agent Crossover's public JDs (available on crossover.com/jobs)
2. Feed their published assessment methodology (selection process page)
3. Feed their hiring philosophy docs (blog posts, public statements)
4. Agent extracts: how Crossover designs roles, how they build assessments, what their compliance posture looks like
5. Agent produces: analysis of their system + recommendations for improvement
6. DT walks through the bootstrap as a live demo of the agent in action

This IS the application. The agent learning Crossover's own system and producing actionable output is proof DT can do the job.

---

## Quick Reference: Bootstrap Commands

```
"Bootstrap talent ops on [org name]"          → starts Phase 1
"Here's our data: [source]"                   → triggers ingestion
"Show coverage report"                        → Data Coverage Report
"Run T1 on this JD: [paste/link]"             → T1 extraction
"Show pipeline status"                        → CCI-T report all modules
"Feed performance data: [source]"             → T6 ingestion
"Show what changed since last calibration"    → T6 drift report
```
