# GV Contextualization Layer

## From Community Voice Data to Structured, Evidence-Backed, Contextualized Insights

This repository contains the implementation and research artifacts for an **ICTD (Information and Communication Technologies for Development)** project focused on building a contextualization layer over **Gram Vaani (GV)** community-generated voice data.

The project explores how large-scale, multilingual, community-generated audio and metadata can be transformed into **structured, location-aware, evidence-backed insights**, and how these insights can subsequently be enriched with information from external sources such as **CoRE Stack** and **GDELT**.

The central objective is not simply to summarize individual voice records. Instead, the project investigates a complete pipeline for moving from:

**raw community voice → observations → concepts → taxonomy → aggregated evidence → contextualized community insights**

---

## 1. Project Motivation

Gram Vaani enables communities to share information, experiences, concerns, and local issues through voice-based platforms.

This creates a valuable source of **community-generated, ground-level information**. However, large-scale voice datasets are difficult to analyze directly because they contain:

* unstructured audio,
* multilingual speech,
* diverse topics,
* repeated observations,
* location-specific issues,
* demographic context,
* varying audio quality,
* and information distributed across thousands of individual records.

A useful computational system therefore needs to answer more than:

> "What does this individual recording say?"

It should also help answer:

> "What recurring issues are visible across the community data?"

and:

> "Where are these issues occurring, what evidence supports them, and what additional context is available from external information sources?"

This project investigates such a **contextualization layer**.

---

# 2. Overall System

The overall research pipeline can be viewed as:

```text
                    GRAM VAANI DATA
                           │
                           ▼
              ┌────────────────────────┐
              │ Data Preparation       │
              │ Cleaning + Metadata    │
              │ Quality Filtering      │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │ Sampling & Pilot       │
              │ Development Dataset    │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │ Open Coding             │
              │ Discover Concepts       │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │ Concept Consolidation  │
              │ Merge Similar Concepts │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │ Taxonomy Development   │
              │ Domain → Theme → Issue │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │ 1K Validation          │
              │ Prompt + Taxonomy Test │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │ 37K Production         │
              │ Large-scale Processing │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │ Evidence Aggregation   │
              │ Location + Context     │
              └────────────┬───────────┘
                           │
                ┌──────────┴───────────┐
                ▼                      ▼
       ┌────────────────┐      ┌────────────────┐
       │  CoRE Stack    │      │     GDELT      │
       │ Structured     │      │ External News │
       │ Context        │      │ / Web Context  │
       └───────┬────────┘      └───────┬────────┘
               │                       │
               └───────────┬───────────┘
                           ▼
              ┌────────────────────────┐
              │ Contextualized         │
              │ Community Insights     │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │ Demonstrator / Reports │
              │ & Analysis             │
              └────────────────────────┘
```

---

# 3. Dataset

The project works with a labelled Gram Vaani dataset containing approximately **100 hours of community-generated audio** and around **37,000 utterances**.

The main production dataset contains approximately:

| Property                |                          Value |
| ----------------------- | -----------------------------: |
| Audio duration          |                     ~100 hours |
| Total utterances        |                        ~37,152 |
| Data type               |      Community-generated voice |
| Metadata                |                      Available |
| Location information    | Available for relevant records |
| Demographic information |       Available where provided |
| Sentiment information   | Available in labelled metadata |
| Audio quality labels    |                      Available |

The metadata contains fields associated with individual utterances, including identifiers, audio references, location/demographic information, sentiment-related information, and quality-related annotations.

The project does not assume that every utterance represents a community-wide issue. Instead, individual observations are treated as evidence that can potentially contribute to a larger pattern.

---

# 4. From Individual Voices to Community Insights

One of the main conceptual decisions in the project is to distinguish between an **observation** and an **insight**.

An individual record might contain:

```text
"People in this area are having difficulty accessing irrigation water."
```

That is an observation.

If many related records from the same or related locations describe the same issue, they can be aggregated:

```text
Multiple voice records
        │
        ├── Record 1
        ├── Record 2
        ├── Record 3
        ├── ...
        └── Record N
                │
                ▼
        Common issue/theme
                │
                ▼
        Evidence aggregation
                │
                ▼
        Community-level insight
```

Therefore, the intended system is not simply:

```text
Audio → Summary
```

but:

```text
Audio
  ↓
Observation
  ↓
Concept
  ↓
Taxonomy
  ↓
Evidence aggregation
  ↓
Contextualized insight
```

This distinction is important for avoiding unsupported generalizations from isolated voice records.

---

# 5. Data Preparation

Before large-scale analysis, the available GV data was inspected and processed to understand:

* available metadata,
* location information,
* demographic fields,
* sentiment information,
* audio quality,
* record identifiers,
* transcript-related fields,
* and the overall structure of the dataset.

The project maintains a master metadata representation under:

```text
data/master/
```

and production-related data artifacts under:

```text
production_37k/data/
```

Quality information is also retained so that unreliable records can be distinguished from usable observations.

---

# 6. Sampling and Pilot Development

The complete dataset was not immediately processed as a single experiment.

Instead, the project followed an iterative development strategy:

```text
37K+ records
      │
      ▼
Sampling
      │
      ▼
Pilot dataset
      │
      ▼
Prompt / taxonomy experiments
      │
      ▼
Validation
      │
      ▼
Production processing
```

This was important because the project required iterative development of:

* prompts,
* taxonomy structure,
* output schemas,
* aggregation strategies,
* external-source matching,
* and evaluation criteria.

The repository therefore contains separate artifacts for pilot experiments, validation, and production processing.

---

# 7. Open Coding

A major early step was **open coding**.

Instead of starting with a completely fixed taxonomy and forcing every observation into predefined categories, the project first attempted to discover concepts emerging from the data.

Conceptually:

```text
Community observations
        │
        ▼
     LLM analysis
        │
        ▼
Candidate concepts
        │
        ▼
Open codes
```

The objective was to capture the language and concepts actually present in the community data.

Open-coding outputs are stored under:

```text
llm_outputs/open_coding/
```

The project generated multiple batches of open-coding outputs rather than relying on a single monolithic LLM call.

This made it possible to inspect the consistency and diversity of discovered concepts.

---

# 8. Concept Consolidation

Open coding naturally produces similar or overlapping concepts.

For example:

```text
"lack of irrigation"
"no irrigation water"
"water unavailable for farming"
"irrigation shortage"
```

may represent a related underlying concept.

Therefore, the project introduced a **concept consolidation** stage:

```text
Open Codes
    │
    ├── Concept A
    ├── Concept B
    ├── Concept C
    └── Concept D
          │
          ▼
   Consolidation
          │
          ▼
Unified Concept
```

The consolidated outputs are stored under:

```text
llm_outputs/consolidation/
```

This step reduces unnecessary fragmentation before building the final taxonomy.

---

# 9. Taxonomy

The taxonomy is the main structural layer of the project.

The current conceptual hierarchy is:

```text
Domain
   │
   └── Theme
          │
          └── Issue
                 │
                 └── Observation
```

For example:

```text
Agriculture
   │
   └── Crop Production
          │
          └── Irrigation
                 │
                 └── Difficulty accessing irrigation water
```

The taxonomy provides a common vocabulary through which otherwise heterogeneous voice observations can be organized.

The taxonomy is intended to be:

* hierarchical,
* interpretable,
* extensible,
* location-aware,
* suitable for LLM-assisted annotation,
* useful for aggregation,
* and grounded in the original evidence.

Multiple iterations of the taxonomy are maintained in:

```text
taxonomy/
```

The evolution from earlier taxonomy versions to later versions is part of the research process rather than merely a software implementation detail.

---

# 10. Why the Taxonomy Matters

Without a taxonomy, related records may remain disconnected:

```text
Record A → "water problem"
Record B → "irrigation shortage"
Record C → "no water for crops"
Record D → "canal not working"
```

A structured taxonomy can connect them:

```text
Agriculture
    └── Crop Production
          └── Irrigation
                └── Water Access Problems
```

This makes aggregation possible.

The taxonomy therefore acts as a bridge between:

```text
unstructured community observations
```

and:

```text
structured community-level analysis
```

---

# 11. LLM-Based Processing

LLMs are used as analysis components throughout the pipeline.

The project explores their use for:

* open coding,
* concept discovery,
* concept consolidation,
* taxonomy assignment,
* structured extraction,
* summarization,
* evidence organization,
* and contextualization.

The LLM is not treated as an independent source of truth.

A generated statement should ideally remain traceable to the underlying records:

```text
Generated insight
      │
      ├── Supporting records
      ├── Evidence count
      ├── Location
      ├── Taxonomy
      └── External context
```

This is intended to reduce hallucination and improve interpretability.

---

# 12. Pilot and Validation

The project contains separate pilot and validation stages.

Relevant directories include:

```text
pilot/
pilot_1k/
validation/
```

The pilot stage was used to experiment with:

* prompts,
* taxonomy assignment,
* output structures,
* aggregation,
* and external alignment.

A larger **1K-scale validation stage** was then used to test the pipeline before production-scale processing.

The overall development strategy was:

```text
Small-scale experimentation
          ↓
1K validation
          ↓
37K production
```

This reduces the risk of applying an unstable prompt or taxonomy to the complete dataset.

---

# 13. Production-Scale Processing

After iterative development, the pipeline was extended to the approximately **37K-record dataset**.

Production artifacts are organized under:

```text
production_37k/
```

The production directory contains components for:

```text
production_37k/
├── checkpoints/
├── core_bridge/
├── data/
├── demonstrator/
├── external_alignment/
├── gdelt/
├── reports/
└── summaries/
```

The processing was divided into batches and checkpoints so that large-scale processing could be resumed and inspected without treating the entire dataset as a single opaque execution.

---

# 14. Evidence Aggregation

A key step is aggregating multiple related observations into a structured representation.

A conceptual insight object contains information such as:

### Location

* State
* District
* Other available geographic information

### Taxonomy

* Domain
* Theme
* Issue

### Evidence

* Number of supporting records
* Supporting observations
* Qualitative evidence
* Evidence summary

### Context

* Demographic information where available
* Temporal information where available
* Geographic context

### External information

* CoRE Stack mappings
* GDELT queries
* Relevant external links

The intended structure can be summarized as:

```text
                INSIGHT
                   │
       ┌───────────┼────────────┐
       ▼           ▼            ▼
   Location     Taxonomy      Evidence
       │           │            │
       │           │            ├── Count
       │           │            ├── Records
       │           │            └── Summary
       │           │
       │           ├── Domain
       │           ├── Theme
       │           └── Issue
       │
       └── State / District

                   │
                   ▼
              Context
                   │
          ┌────────┴────────┐
          ▼                 ▼
     CoRE Stack           GDELT
```

---

# 15. Location-Aware Contextualization

Location is a central part of the system.

An issue should not automatically be treated as a general phenomenon simply because it appears somewhere in the dataset.

The intended flow is:

```text
Voice Record
     ↓
Metadata
     ↓
Location
     ↓
Taxonomy
     ↓
Aggregation
     ↓
Location-specific insight
```

This enables analysis such as:

* What issues are appearing in a particular district?
* Which themes recur within a state?
* Which issues are shared across multiple locations?
* What external contextual information exists for a particular location?

Location also provides an important bridge to external sources such as GDELT and CoRE Stack.

---

# 16. CoRE Stack Integration

The project includes a bridge between identified GV issues and **CoRE Stack** information.

The basic idea is:

```text
GV Observation
      ↓
Issue / Theme
      ↓
Location
      ↓
CoRE Stack matching
      ↓
Relevant contextual information
```

The current project artifacts contain approximately:

```text
44 CoRE Stack mappings
```

These mappings are stored in:

```text
production_37k/core_bridge/
```

and related production artifacts.

The purpose of this integration is to add structured contextual information around community observations.

CoRE Stack information is therefore treated as an additional contextual layer rather than as a replacement for GV evidence.

---

# 17. GDELT Integration

The project also explores **GDELT** as an external information source.

The motivation is to investigate whether community-level issues can be connected to broader news/web information.

The basic pipeline is:

```text
GV Issue
    ↓
Taxonomy / Concept
    ↓
Location
    ↓
Query Generation
    ↓
GDELT
    ↓
External Articles / Links
    ↓
Contextual Evidence
```

The current exploratory artifacts contain approximately:

```text
129 GDELT queries
162 retrieved links
```

These artifacts are available under:

```text
production_37k/gdelt/
production_37k/external_alignment/
```

The external retrieval layer is intended to provide context around an issue.

It does **not** automatically establish that an external article proves the underlying GV observation.

---

# 18. External Alignment

The project therefore treats external-source integration as an **alignment problem**.

The system attempts to align:

```text
GV
│
├── Location
├── Domain
├── Theme
└── Issue
        │
        ├──────────────► CoRE Stack
        │
        └──────────────► GDELT
```

This creates a multi-source contextual representation:

```text
Community Evidence
        +
Structured Context
        +
External Information
        ↓
Contextualized Insight
```

The important distinction is that these sources have different roles.

### Gram Vaani

Provides community-generated evidence.

### CoRE Stack

Provides structured contextual information.

### GDELT

Provides external news/web context.

They should therefore not be treated as interchangeable evidence sources.

---

# 19. Demonstrator

The project also contains demonstrator artifacts under:

```text
production_37k/demonstrator/
```

The intended user experience is to allow exploration through dimensions such as:

```text
Location
   ↓
Domain
   ↓
Theme
   ↓
Issue
   ↓
Evidence
   ↓
External Context
```

A user should eventually be able to move from a high-level issue to the evidence supporting it and then inspect the contextual information associated with that issue.

---

# 20. Repository Structure

```text
GV_contextualization_layer/
│
├── README.md
├── .env.example
├── app.py
│
├── data/
│   └── master/
│       └── gv_master_metadata.csv
│
├── taxonomy/
│   └── Taxonomy versions and taxonomy artifacts
│
├── prompts/
│   └── LLM prompts and structured extraction instructions
│
├── scripts/
│   └── Data processing, analysis and utility scripts
│
├── llm_outputs/
│   ├── open_coding/
│   └── consolidation/
│
├── pilot/
│   ├── outputs/
│   ├── reports/
│   └── summaries/
│
├── pilot_1k/
│   ├── data/
│   ├── outputs/
│   └── reports/
│
├── validation/
│   └── Validation artifacts
│
├── production_37k/
│   ├── checkpoints/
│   ├── core_bridge/
│   ├── data/
│   ├── demonstrator/
│   ├── external_alignment/
│   ├── gdelt/
│   ├── reports/
│   └── summaries/
│
├── reports/
│   └── Project reports and analysis
│
├── samples/
│   └── Sampling-related artifacts
│
└── scratch/
    └── Experimental scripts and intermediate artifacts
```

---

# 21. Technology Stack

The project primarily uses:

### Programming

* Python
* PowerShell / shell scripting

### Data Processing

* Pandas
* NumPy
* CSV
* JSON
* JSONL

### NLP / LLM

* Large Language Models
* Prompt-based information extraction
* Open coding
* Structured JSON generation
* Text summarization
* Concept consolidation

### External Sources

* CoRE Stack
* GDELT

### Development

* Git
* GitHub
* VS Code
* Python virtual environments / Conda where appropriate

---

# 22. Configuration

API credentials and environment-specific configuration should never be committed to the repository.

A template is provided as:

```text
.env.example
```

Create a local environment file:

```bash
cp .env.example .env
```

On Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Then populate the required credentials locally.

For example:

```env
OPENAI_API_KEY=
GEMINI_API_KEY=
OTHER_API_KEY=
```

**Never commit real API keys.**

---

# 23. Running the Project

Clone the repository:

```bash
git clone https://github.com/Godvampire07/GV_contextualization_layer.git
cd GV_contextualization_layer
```

Create an environment:

```bash
python -m venv .venv
```

Activate on Windows:

```powershell
.venv\Scripts\Activate.ps1
```

Activate on Linux/macOS:

```bash
source .venv/bin/activate
```

Install dependencies if the repository contains a requirements file:

```bash
pip install -r requirements.txt
```

Create local configuration:

```powershell
Copy-Item .env.example .env
```

The exact execution command depends on the specific experiment or pipeline stage. The repository is organized so that individual scripts and production artifacts can be inspected and executed independently.

---

# 24. Reproducibility

For a reproducible experiment, the following should be recorded:

```text
Dataset version
Taxonomy version
Prompt version
LLM/model version
Model parameters
Sampling criteria
Processing date
External-source query version
Evaluation methodology
```

This is particularly important because LLM-generated outputs can change with:

* model versions,
* prompts,
* temperature,
* context,
* sampling,
* and structured-output constraints.

---

# 25. Evaluation Framework

A major future research question is:

> What qualifies as a useful contextualized insight?

The project therefore considers multiple evaluation dimensions.

### Groundedness

Does the generated insight accurately reflect the underlying community evidence?

### Faithfulness

Does the generated text avoid introducing information that is not supported by the source records?

### Evidence Coverage

Does the insight adequately represent the records used to generate it?

### Taxonomy Consistency

Are similar observations categorized consistently?

### Location Accuracy

Is geographic information preserved correctly?

### Relevance

Is the extracted issue actually relevant to the supporting observations?

### External Context Relevance

Are the retrieved CoRE Stack / GDELT results genuinely relevant to the identified issue and location?

### Usefulness

Does the contextualized representation provide information that is more useful for analysis than the original unstructured collection?

These dimensions provide a foundation for future human evaluation and automated evaluation protocols.

---

# 26. Research Challenges

The project involves several important research challenges.

## Multilinguality

Community voice data can contain multiple Indian languages and local linguistic variations.

A translation or transcription system may preserve literal meaning while losing local context.

---

## Noisy Audio

Community-generated audio may contain:

* background noise,
* inaudible segments,
* speaker changes,
* audio jumps,
* incomplete speech,
* and other quality issues.

Quality information therefore needs to remain part of the processing pipeline.

---

## LLM Hallucination

LLMs can generate plausible but unsupported statements.

The system therefore emphasizes:

```text
Evidence
   ↓
Extraction
   ↓
Aggregation
   ↓
Insight
```

rather than unconstrained generation.

---

## Taxonomy Drift

A taxonomy created at the beginning of the project may not adequately represent all concepts discovered later.

The taxonomy therefore needs iterative refinement.

---

## Aggregation

A critical methodological question is deciding when multiple observations should be considered evidence of a broader issue.

Simply counting similar text is insufficient.

Aggregation needs to consider factors such as:

* semantic similarity,
* location,
* time,
* demographic context,
* evidence count,
* and issue specificity.

---

## External Context

A retrieved article may mention similar words while discussing a completely different event or location.

Therefore:

```text
Keyword Match ≠ Contextual Relevance
```

External-source alignment requires semantic and geographic relevance.

---

# 27. Important Design Principles

### Evidence First

The community data remains the primary evidence source for community observations.

### Traceability

Generated insights should ideally be traceable back to the records that support them.

### Preserve Uncertainty

The system should avoid presenting weak evidence as a strong conclusion.

### Location Awareness

Geographic context should be preserved throughout the pipeline.

### Human-in-the-Loop

Taxonomy development and insight evaluation benefit from human review.

### External Sources as Context

CoRE Stack and GDELT provide additional context and should not automatically override community-generated evidence.

### Iterative Development

The system is developed through:

```text
Pilot
  ↓
Validation
  ↓
Production
  ↓
Evaluation
  ↓
Refinement
```

---

# 28. Current Project Artifacts

The repository currently contains artifacts corresponding to:

* data preparation,
* sampling,
* taxonomy development,
* multiple taxonomy versions,
* open coding,
* concept consolidation,
* pilot experiments,
* 1K validation,
* 37K-scale production processing,
* production checkpoints,
* evidence aggregation,
* location-aware analysis,
* CoRE Stack integration,
* GDELT query generation,
* external alignment,
* reports,
* summaries,
* and a contextualization demonstrator.

Current exploratory external-source artifacts include:

| Source                | Current artifact count |
| --------------------- | ---------------------: |
| CoRE Stack            |           ~44 mappings |
| GDELT                 |            129 queries |
| GDELT retrieved links |                    162 |

These values describe the current state of the project artifacts and may change as the pipeline is refined.

---

# 29. Future Work

The current implementation establishes the initial contextualization pipeline. The next research stages include:

### 1. Refine the Taxonomy

Continue iterating on the Domain → Theme → Issue hierarchy using both data-driven discovery and human review.

### 2. Improve Insight Aggregation

Develop a principled method for deciding when multiple observations constitute a meaningful community-level pattern.

### 3. Formalize Evaluation

Create human evaluation protocols and quantitative metrics for:

* groundedness,
* faithfulness,
* evidence coverage,
* taxonomy consistency,
* relevance,
* and usefulness.

### 4. Improve Multilingual Processing

Investigate better approaches for Indian-language ASR, translation, multilingual embeddings, and LLM-based analysis.

### 5. Improve External Retrieval

Improve matching between GV issues and:

* CoRE Stack,
* GDELT,
* government datasets,
* institutional sources,
* and other public contextual datasets.

### 6. Human-in-the-Loop Validation

Allow researchers or domain experts to validate:

```text
Observation
    ↓
Taxonomy
    ↓
Aggregation
    ↓
Insight
    ↓
External Context
```

### 7. Interactive Contextualization Interface

Develop a richer interface for exploring:

```text
Location
    ↓
Domain
    ↓
Theme
    ↓
Issue
    ↓
Evidence
    ↓
External Context
```

### 8. Provenance-Aware Insights

Maintain explicit links between generated insights and the records, taxonomy decisions, prompts, models, and external sources used to construct them.

---

# 30. Long-Term Vision

The long-term goal is to develop a system that can transform large-scale community-generated voice data into **structured, traceable, location-aware, and context-rich representations of community concerns**.

The intended conceptual pipeline is:

```text
             COMMUNITY VOICE
                    │
                    ▼
              TRANSCRIPTION
                    │
                    ▼
              STRUCTURING
                    │
                    ▼
               TAXONOMY
                    │
                    ▼
              AGGREGATION
                    │
                    ▼
                EVIDENCE
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
     CORE STACK             GDELT
          │                   │
          └─────────┬─────────┘
                    ▼
             CONTEXTUALIZATION
                    │
                    ▼
              EVALUATION
                    │
                    ▼
             HUMAN / SYSTEM
                INTERFACE
```

The central research question is:

> **How can community-generated voice data be transformed into reliable, evidence-backed and context-rich insights while preserving local context, uncertainty, provenance, and the voices of the communities that generated the data?**

---

# 31. Data Responsibility

This project works with community-generated information and therefore requires careful handling of data.

Any deployment, publication, or redistribution should consider:

* privacy,
* personally identifiable information,
* sensitive demographic information,
* geographic privacy,
* consent,
* data ownership,
* community governance,
* responsible AI practices,
* model hallucination,
* and appropriate use of generated insights.

Private or restricted Gram Vaani data should **not** be redistributed through this repository unless explicit permission has been obtained.

Generated insights should also not be interpreted as statistically representative of an entire population unless the underlying sampling and evaluation methodology supports that conclusion.

---

# 32. Acknowledgements

This project is being developed as part of an ICTD research project involving:

**Gram Vaani**

**Indian Institute of Technology Delhi**

**Sardar Vallabhbhai National Institute of Technology, Surat**

The project builds on community-generated voice data and investigates computational methods for organizing, aggregating, and contextualizing such data using NLP, LLMs, structured taxonomies, and external information sources.

---

# 33. Project Repository

**GitHub:**
https://github.com/Godvampire07/GV_contextualization_layer

---

## Project Summary

In one line:

> **A research and engineering pipeline that transforms large-scale Gram Vaani community voice data into structured, location-aware, evidence-backed insights and enriches them with contextual information from sources such as CoRE Stack and GDELT.**
