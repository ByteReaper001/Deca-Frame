# DECA-FRAME

### A Ten-Stage Framework for Degradation-Aware Remaining Useful Life Prediction of Jet Engines

**DECA-FRAME** is a modular research framework for **Remaining Useful Life (RUL) prediction of jet engines**, with a primary focus on **aircraft turbofan engine prognostics**.

The framework is designed to transform raw **PHM (Prognostics and Health Management)** sensor data into a degradation-aware prognostic system that can estimate **how much useful life remains in a jet engine**, quantify uncertainty, retrieve similar historical degradation trajectories, construct supporting evidence, and generate interpretable prognostic reasoning.

The framework is designed to work with datasets such as **NASA C-MAPSS, N-CMAPSS**, and potentially other PHM datasets.

> **From raw jet-engine sensor data → degradation understanding → trajectory memory → adaptive RUL prediction → evidence-backed prognostic reasoning → decision and feedback.**

---

# Research Motivation

**Remaining Useful Life (RUL)** prediction is a fundamental problem in **Prognostics and Health Management (PHM)** and predictive maintenance.

For a jet engine, RUL represents the estimated amount of operational life remaining before the engine reaches a defined failure or end-of-life condition.

Traditional RUL prediction approaches often focus on learning a direct relationship between historical sensor measurements and remaining cycles:

```text
Sensor Data
     ↓
Machine Learning Model
     ↓
RUL Prediction
```

However, jet-engine degradation is influenced by multiple interacting factors:

* Operating conditions
* Sensor behavior
* Degradation progression
* Different degradation trajectories
* Failure modes
* Temporal dependencies
* Noise and measurement variability
* Model uncertainty
* Limited interpretability
* Differences between historical and current trajectories

DECA-FRAME approaches RUL prediction as a **multi-stage prognostic reasoning problem** rather than treating it as a standalone regression task.

---

# Framework Overview

DECA-FRAME consists of **10 interconnected stages**:

```text
[START] + [PHM DATA AS INPUT]
        │
        ▼
[STAGE-1: DATASET & FAILURE-MODE PROFILING]
        │
        ▼
[STAGE-2: DEGRADATION STATE ESTIMATION]
        │
        ▼
[STAGE-3: DEGRADATION SIGNATURE]
        │
        ▼
[STAGE-4: TRAJECTORY MEMORY & ANALOG RETRIEVAL]
        │
        ▼
[STAGE-5: ADAPTIVE PROGNOSTIC ENSEMBLE]
        │
        ▼
[STAGE-6: RUL + UNCERTAINTY + ABSTENTION]
        │
        ▼
[STAGE-7: PROGNOSTIC EVIDENCE GRAPH]
        │
        ▼
[STAGE-8: EVIDENCE-CALIBRATED RAG]
        │
        ▼
[STAGE-9: GENAI PROGNOSTIC REASONING]
        │
        ▼
[STAGE-10: DECISION + FEEDBACK + AUDIT]
```

The central objective is to move from:

> **"What is the predicted RUL?"**

toward:

> **"Why is this jet engine degrading, how much useful life remains, how certain is that estimate, what historical evidence supports it, and can the system justify its prognostic decision?"**

---

# The 10 Stages

## 01 — Dataset & Failure-Mode Profiling

The first stage establishes an understanding of the PHM dataset and the failure behavior represented within it.

For jet-engine datasets, this stage examines:

* Engine population
* Sensor measurements
* Operating conditions
* Operational cycles
* Sensor distributions
* Failure characteristics
* Degradation behavior
* Data quality
* Failure modes
* Differences between operating regimes

The objective is to understand **what the data represents and what types of degradation are present** before applying predictive models.

```text
PHM Data
   ↓
Dataset Characteristics
   ↓
Operating Conditions
   ↓
Sensor Behavior
   ↓
Failure Modes
   ↓
Degradation Context
```

---

# 02 — Degradation State Estimation

Stage 2 estimates the current **degradation state of the jet engine**.

Instead of immediately predicting RUL, the framework first attempts to determine where the engine currently lies within its degradation progression.

A conceptual representation is:

```text
Healthy
   │
   ▼
Early Degradation
   │
   ▼
Progressive Degradation
   │
   ▼
Critical Degradation
   │
   ▼
Failure
```

The degradation state can incorporate:

* Current sensor behavior
* Historical behavior
* Operating conditions
* Temporal trends
* Change points
* Degradation progression
* Failure-mode information

The result provides contextual information for the subsequent prognostic stages.

---

# 03 — Degradation Signature

Stage 3 creates a structured **degradation signature** describing the current health and degradation behavior of the engine.

Rather than representing an engine only through its raw sensor values, the signature attempts to capture **how the engine is degrading**.

It may incorporate:

* Sensor trends
* Rate of degradation
* Dominant sensors
* Sensor interactions
* Operating regime
* Degradation state
* Temporal characteristics
* Failure-mode indicators
* Degradation severity
* Change-point information

Conceptually:

```text
Sensor Measurements
        +
Operating Conditions
        +
Degradation State
        +
Temporal Behavior
        │
        ▼
DEGRADATION SIGNATURE
```

This signature becomes an important representation for comparing the current engine trajectory with historical engine behavior.

---

# 04 — Trajectory Memory & Analog Retrieval

Stage 4 introduces **trajectory memory** into the prognostic process.

The framework maintains representations of previously observed degradation trajectories and uses them to identify **historically similar engine trajectories**.

```text
Current Engine Trajectory
          │
          ▼
Trajectory Representation
          │
          ▼
Similarity Retrieval
          │
     ┌────┴────┐
     ▼         ▼
 Analog 1    Analog 2
     │         │
     └────┬────┘
          ▼
Historical Prognostic Evidence
```

Similarity can consider:

* Degradation signature
* Sensor trajectories
* Operating conditions
* Degradation state
* Failure mode
* Temporal behavior

The underlying idea is that **historical degradation trajectories can provide useful contextual information about the future behavior of a currently degrading engine**.

---

# 05 — Adaptive Prognostic Ensemble

Stage 5 generates RUL estimates using an **adaptive prognostic ensemble**.

Instead of assuming that one predictive model is optimal for every engine and every degradation trajectory, multiple prognostic models can be considered.

Potential models include:

* LSTM
* GRU
* Temporal CNN
* Transformers
* XGBoost
* Statistical models
* Hybrid models
* Custom degradation-aware architectures

Conceptually:

```text
                ┌── LSTM ────────────┐
                │                    │
                ├── Transformer ─────┤
                │                    │
Engine Context ─┼── XGBoost ─────────┼──► Adaptive RUL
                │                    │
                ├── Statistical ────┤
                │                    │
                └── Hybrid Model ────┘
```

The ensemble can take into account:

* Degradation state
* Degradation signature
* Historical analogs
* Operating conditions
* Model behavior
* Prediction confidence

The objective is to make prognostic modeling **adaptive to the current degradation context**.

---

# 06 — RUL + Uncertainty + Abstention

Stage 6 produces the primary prognostic output:

### Remaining Useful Life

For a jet engine, RUL represents the estimated number of operational cycles remaining before the defined failure or end-of-life condition.

Instead of producing only:

```text
Predicted RUL = 47 cycles
```

DECA-FRAME aims to provide:

```text
Predicted RUL = 47 cycles
Uncertainty   = ± X cycles
Confidence    = X%
```

The stage also introduces **abstention**.

If the available evidence is insufficient or the predictive uncertainty is too high, the system can choose not to provide a definitive RUL estimate.

```text
RUL Prediction
      +
Uncertainty
      +
Evidence Quality
      │
      ▼
 ┌───────────────┐
 │ Predict /     │
 │ Abstain       │
 └───────────────┘
```

Potential reasons for abstention include:

* High uncertainty
* Strong disagreement between models
* Weak historical analog similarity
* Conflicting degradation indicators
* Out-of-distribution behavior
* Insufficient evidence

This allows the system to distinguish between:

> **"The model predicts this RUL."**

and:

> **"The available evidence is insufficient for a reliable RUL prediction."**

---

# 07 — Prognostic Evidence Graph

Stage 7 creates a structured **Prognostic Evidence Graph** connecting the different elements involved in the prediction.

The graph can represent relationships between:

* Sensor observations
* Degradation indicators
* Degradation state
* Failure modes
* Historical trajectories
* Predictive models
* RUL predictions
* Uncertainty
* Supporting evidence

Conceptually:

```text
Sensor Observation
        │
        ▼
Degradation Indicator
        │
        ▼
Degradation State
        │
        ├──────────────► Failure Mode
        │
        ▼
RUL Prediction
        │
        ├──────────────► Uncertainty
        │
        └──────────────► Analog Trajectories
                              │
                              ▼
                     Supporting Evidence
```

The purpose of this stage is to establish a **traceable relationship between observed engine behavior and the resulting prognostic output**.

---

# 08 — Evidence-Calibrated RAG

Stage 8 introduces **Retrieval-Augmented Generation (RAG)** using the evidence generated by the prognostic pipeline.

Rather than allowing a language model to independently retrieve arbitrary information, the retrieval process is intended to be informed by the current prognostic context.

```text
Prognostic Evidence
        │
        ▼
Evidence Context
        │
        ▼
Knowledge Retrieval
        │
        ▼
Evidence-Calibrated Context
```

Potential knowledge sources include:

* Jet-engine maintenance documentation
* Technical manuals
* Failure-mode information
* Engineering references
* Component information
* Historical maintenance knowledge
* Operational guidelines

Retrieval can be influenced by:

* Failure mode
* Degradation state
* Sensor evidence
* Operating condition
* RUL estimate
* Historical analogs

The objective is to provide **relevant domain knowledge that supports the prognostic evidence**.

---

# 09 — GenAI Prognostic Reasoning

Stage 9 uses **Generative AI** to reason over the structured information generated by the previous stages.

The GenAI layer can receive:

```text
Degradation State
        +
Degradation Signature
        +
Analog Trajectories
        +
RUL Prediction
        +
Uncertainty
        +
Abstention Status
        +
Prognostic Evidence
        +
Retrieved Knowledge
```

The output can provide:

* Degradation summaries
* Prognostic explanations
* Failure-context interpretation
* Evidence-grounded reasoning
* Uncertainty interpretation
* Maintenance-oriented insights

The GenAI component is positioned **after the analytical and prognostic pipeline**.

It is therefore not intended to replace the underlying RUL prediction model.

Instead:

> **Machine learning estimates the prognosis; GenAI explains and contextualizes the prognosis using available evidence.**

---

# 10 — Decision + Feedback + Audit

The final stage closes the prognostic loop.

The system combines:

```text
RUL
+
Uncertainty
+
Degradation State
+
Evidence
+
Historical Analogs
+
GenAI Reasoning
```

to support a maintenance-oriented decision.

Possible outputs may include:

* Continue monitoring
* Increased monitoring
* Engineering investigation
* Maintenance review
* Insufficient evidence / abstention

The framework also incorporates **feedback**.

Once the actual future behavior of the engine becomes known, the observed outcome can be compared against the previous prediction.

```text
Prediction
     │
     ▼
Actual Engine Outcome
     │
     ▼
Comparison
     │
     ├── Prediction Error
     ├── Uncertainty Calibration
     ├── Retrieval Quality
     ├── Model Performance
     └── Decision Quality
```

The **audit** component preserves the reasoning chain behind the prediction and decision.

This enables the system to answer:

> **What did the system observe, what did it predict, what evidence did it use, why did it reach that conclusion, and what actually happened afterward?**

---

# Core Research Concept

One of the important concepts explored within DECA-FRAME is **degradation-aware residual analysis**.

Raw sensor measurements can be influenced by both:

```text
Operating Conditions
+
Actual Degradation
```

Therefore, a sensor value changing does not necessarily mean that the engine is degrading.

DECA-FRAME explores estimating the expected sensor behavior under a given operating condition and examining the difference between expected and observed behavior.

```text
Observed Sensor Behavior
          │
          │
          ▼
Operating-Condition Model
          │
          ▼
Expected Sensor Behavior
          │
          │
          ▼
Observed − Expected
          │
          ▼
       Residual
          │
          ▼
Potential Degradation Signal
```

The resulting residual can provide an additional representation of degradation that is less dependent on normal operating-condition variation.

This concept forms part of the broader degradation-aware philosophy of DECA-FRAME.

---

# Jet Engine RUL Prediction

The primary application of DECA-FRAME is **Remaining Useful Life prediction for aircraft turbofan engines**.

For a jet engine operating over multiple cycles:

```text
Engine Age / Operating Cycles
            │
            ▼
Sensor Measurements
            │
            ▼
Degradation Evolution
            │
            ▼
Current Health State
            │
            ▼
Estimated Remaining Useful Life
```

For example:

```text
Current Engine State
        │
        ▼
Predicted RUL
        │
        ▼
Remaining Operational Cycles
        │
        ▼
Maintenance Planning
```

The framework therefore attempts to move beyond simply predicting a numerical RUL value and toward understanding **why the engine is approaching failure and how reliable that prediction is**.

---

# Supported PHM Datasets

DECA-FRAME is designed to operate on PHM datasets containing temporal sensor measurements and degradation information.

## NASA C-MAPSS

The initial experimental focus includes the NASA **C-MAPSS turbofan engine degradation dataset**.

Target subsets include:

* FD001
* FD002
* FD003
* FD004

These subsets provide different combinations of operating conditions and fault/degradation characteristics for evaluating RUL prediction.

## N-CMAPSS

DECA-FRAME is also designed to extend to **N-CMAPSS**, enabling evaluation on a more complex turbofan-engine prognostics dataset.

The broader objective is to develop a framework that is not restricted to a single benchmark dataset.

---

# Evaluation

DECA-FRAME evaluates the framework from multiple perspectives.

### RUL Prediction

Potential metrics include:

* RMSE
* MAE
* NASA C-MAPSS scoring function
* Prediction error distribution

### Degradation Modeling

Potential evaluation includes:

* Degradation-state consistency
* Trendability
* Monotonicity
* Prognosability
* Change-point consistency

### Uncertainty

Potential evaluation includes:

* Prediction interval coverage
* Calibration
* Sharpness
* Uncertainty-error relationship

### Trajectory Retrieval

Potential evaluation includes:

* Analog similarity
* Retrieval relevance
* Failure-mode consistency
* Historical trajectory usefulness

### Explainability

Potential evaluation includes:

* Sensor contribution
* Feature attribution
* Temporal contribution
* Evidence consistency

### Abstention

Potential evaluation includes:

* Prediction coverage
* Selective risk
* Uncertainty-based rejection
* Out-of-distribution behavior

---

# Experimental Philosophy

DECA-FRAME is designed around **ablation and comparative experimentation**.

The contribution of individual stages can be studied independently instead of assuming that every component automatically improves the final system.

For example:

```text
Baseline RUL Model
        │
        ├── + Degradation State
        │
        ├── + Degradation Signature
        │
        ├── + Trajectory Memory
        │
        ├── + Adaptive Ensemble
        │
        ├── + Uncertainty
        │
        ├── + Abstention
        │
        ├── + Evidence Graph
        │
        ├── + Evidence-Calibrated RAG
        │
        ├── + GenAI Reasoning
        │
        └── + Feedback & Audit
```

This allows the research to determine which components contribute to:

* RUL prediction performance
* Reliability
* Uncertainty calibration
* Retrieval quality
* Explainability
* Decision support

---

# Research Questions

DECA-FRAME is being developed around questions such as:

1. Can explicit degradation-state estimation improve jet-engine RUL prediction?

2. Can degradation signatures provide more informative representations than raw sensor sequences?

3. Can historical trajectory memory improve prognostic estimation for currently degrading engines?

4. Can an adaptive prognostic ensemble respond more effectively to different degradation trajectories?

5. Can uncertainty estimation identify situations where RUL predictions should not be trusted?

6. Can abstention reduce the risk of unsupported prognostic predictions?

7. Can a Prognostic Evidence Graph provide a traceable relationship between sensor observations and RUL predictions?

8. Can evidence-calibrated RAG provide more relevant maintenance knowledge?

9. Can GenAI generate useful prognostic reasoning when constrained by structured evidence?

10. Can feedback and audit mechanisms create a more complete end-to-end prognostic lifecycle?

---

# Research Direction

The long-term objective of DECA-FRAME is to develop and experimentally evaluate a **degradation-aware, uncertainty-aware, evidence-grounded, and auditable framework for jet-engine prognostics**.

The framework combines:

```text
PHM
+
Degradation Analysis
+
Trajectory Memory
+
Machine Learning
+
Uncertainty Quantification
+
Abstention
+
Evidence Graphs
+
RAG
+
Generative AI
+
Feedback
```

into a single prognostic architecture.

The central idea is to move from:

> **Prediction-only prognostics**

toward:

> **Evidence-driven prognostic intelligence.**

---

# Authors

## DECA-FRAME Research Team

1. **Chaitanya Kherdikar**
2. **Arya Singh**
3. **Sabiha Mulla**
4. **Darpan Shah**

### Research Areas

* Prognostics & Health Management
* Jet Engine RUL Prediction
* Remaining Useful Life Prediction
* Degradation Modeling
* Trajectory-Based Prognostics
* Uncertainty Quantification
* Selective Prediction & Abstention
* Evidence-Based AI
* Retrieval-Augmented Generation
* Generative AI
* Explainable AI
* Predictive Maintenance

---

# Citation

A formal citation will be added following completion of the research manuscript.

```text
DECA-FRAME:
A Ten-Stage Framework for Degradation-Aware
Remaining Useful Life Prediction of Jet Engines
```

---

# Disclaimer

DECA-FRAME is a research framework intended for academic experimentation and research.

Predictions generated by the framework should not be treated as operational aircraft maintenance instructions without appropriate engineering validation, domain expertise, safety procedures, and applicable certification requirements.

---

> **DECA-FRAME — Understand the degradation. Remember the trajectory. Predict with evidence.**
