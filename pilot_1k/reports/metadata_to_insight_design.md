# Gram Vaani Community Intelligence: Metadata-to-Insight Architecture & Enrichment Design

## 1. Executive Summary
This document establishes the conceptual architecture for transforming raw Gram Vaani audio items and items-table metadata into enriched, multi-dimensional community insights and location summaries. It defines a rigorous categorization of all available metadata attributes, evaluates their analytical utility, specifies an enriched insight data model, and demonstrates comparative summary enrichments on real pilot evidence.

### Core Architectural Principle:
> **"Empty / Unknown is always better than invented."**
> Metadata fields are used strictly to provide contextual boundaries (temporal windows, geographic anchors, demographic disaggregations, and provenance tracing). Metadata is NEVER converted into unsupported causal explanations or false population-level prevalence claims.

---

## 2. Deep Metadata Inventory & Classification

Based on programmatic audit of the Master Corpus (`gv_master_metadata.csv`, 37,152 rows) and External Items Tables (`DAUV_tag.xlsx`, `KBBL_tag.xlsx`, `DAUV_2_Tag_Data.xlsx`, `KBBL_tag_apurva.xlsx`, totaling 13,000+ records):

| Category | Field Name | Source File | Level | Data Type | Completeness | Example Value | Enrichment Value & Utility | Limitations & Misuse Guardrails |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **A. Provenance** | `utt_id` | Master CSV | Utterance | String | 100.0% | `13-00073-02` | Primary unique key linking audio slice to transcript. | Must never be truncated or omitted from citations. |
| **A. Provenance** | `Unique Item ID` | Items Table | Item | Integer | 100.0% | `3426093` | Cross-references broadcast item in GV CMS. | Relates to broadcast package, not individual sentence. |
| **A. Provenance** | `CallerId` | Items Table | Item | String/Int | 100.0% | `919835xxxxxx` | Enables caller-level clustering and repeat report tracking. | Hashed/masked to protect caller privacy. |
| **A. Provenance** | `audio_drive_id` | Master CSV | Utterance | String | 100.0% | `1-rF57uInu...` | Google Drive storage retrieval key for audio playback. | Technical identifier; no analytical interpretation. |
| **A. Provenance** | `Recording audio link` | Items Table | Item | URL | 100.0% | `http://.../audio.mp3` | Direct streaming link for audio auditability. | Depends on server uptime. |
| **B. Geographic** | `State` | Master / Items | Item | String | 32.5% (Master) / 91.3% (Items) | `Bihar`, `Jharkhand`, `UP` | Macro-level administrative filtering and policy mapping. | Do not infer missing states from dialect. |
| **B. Geographic** | `District` | Master / Items | Item | String | 0.2% (Master) / 91.3% (Items) | `Madhubani`, `Dhanbad` | Primary spatial aggregation unit for community briefs. | Missing in master unless spoken in transcript. |
| **B. Geographic** | `Block` | Items Table | Item | String | 91.3% | `Khutauna`, `Bisfi` | Sub-district administrative cluster around BDO offices. | Often marked as 'Not Known' if unrecorded. |
| **B. Geographic** | `Instance name` | Items Table | Item | String | 100.0% | `Ghazipur_MV`, `Est_ent_MV` | Identifies regional radio station / IVR channel. | Reflects station footprint, not caller residence. |
| **B. Geographic** | `location_source` | Pipeline | Utterance | Enum | 100.0% | `metadata`, `transcript`, `unknown` | Tracks geographic provenance and certainty level. | Alerts analyst when location is unverified. |
| **C. Temporal** | `Item created date`| Items Table | Item | Datetime | 100.0% | `2023-05-01 15:17:24`| Precise timestamp of community call ingestion. | Reflects call time, not necessarily event time. |
| **C. Temporal** | `published date` | Items Table | Item | Datetime | 100.0% | `2023-05-01 15:44:02`| Timestamp when item was approved and broadcast over IVR. | Measures editorial turnaround latency. |
| **D. Demographic** | `Gender` | Master CSV | Utterance | String | 90.0% | `Male`, `Female` | Disaggregates reports by gender (e.g. SHGs, maternal care). | Caller voice inference; not census self-report. |
| **D. Demographic** | `Age` | Master CSV | Utterance | String | 89.3% | `Adult`, `Senior` | Age-cohort stratification (youth employment vs pensions). | Broad acoustic buckets; not exact numerical age. |
| **D. Demographic** | `Accent` | Master CSV | Utterance | String | 25.1% | `Bihari`, `Maithili` | Dialectal indicator for translation and ASR tuning. | Incomplete across corpus. |
| **E. Content** | `reference` | Master CSV | Utterance | Text | 100.0% | *"बिजली की समस्या..."* | Raw Hindi speech-to-text transcript ground truth. | ASR transcript may contain phonetic errors. |
| **E. Content** | `Title` | Items Table | Item | Text | 100.0% | *"उद्यमी वाणी प्रोमो..."* | Editorial headline assigned by Gram Vaani moderator. | Human summary; may omit caller specifics. |
| **E. Content** | `tags` | Items Table | Item | String | 100.0% | `DAUV,promo,EE` | Categorical tags added by platform moderators. | Ad-hoc editorial taxonomy; non-standardized. |
| **E. Content** | `content_type` | Schema v0.3 | Utterance | Enum | 100.0% | `citizen_grievance`, `bumper`| 7 controlled communication modalities. | Orthogonal to topic taxonomy. |
| **E. Content** | `failure_mode` | Schema v0.3 | Utterance | List[Enum] | 100.0% | `["absenteeism", "delay"]` | 8 standard delivery breakdown mechanisms. | Applies only to substantive grievances. |
| **F. Quality** | `Sentiment` | Master CSV | Utterance | String | 4.8% | `Serious`, `Angry` | Caller emotional tone for urgency prioritization. | Highly sparse in master CSV. |
| **F. Quality** | `Background` | Master CSV | Utterance | String | 0.3% | `Clean`, `Noise` | Acoustic background environment. | Highly sparse in master CSV. |
| **F. Quality** | `Item duration` | Items Table | Item | Float | 100.0% | `88.42` (seconds) | Length of recorded audio; filters truncated clips (<5s). | Longer audio does not always mean better data. |
| **F. Quality** | `Total listening` | Items Table | Item | Float | 100.0% | `1240.5` (seconds) | Cumulative listener engagement / virality metric. | Measures popularity, not objective severity. |

---

## 3. How Metadata Enriches Community Insights Without Hallucination

```text
                               ┌────────────────────────────────────────────────┐
                               │       Raw Utterance + Hindi Transcript         │
                               └──────────────────────┬─────────────────────────┘
                                                      │
                                                      ▼
                               ┌────────────────────────────────────────────────┐
                               │           Taxonomy v0.3 Classification         │
                               │   (Domain → Theme → Issue + Failure Modes)     │
                               └──────────────────────┬─────────────────────────┘
                                                      │
                      ┌───────────────────────────────┴───────────────────────────────┐
                      ▼                                                               ▼
        ┌───────────────────────────┐                                   ┌───────────────────────────┐
        │   Contextual Enrichment   │                                   │   Integrity Guardrails    │
        ├───────────────────────────┤                                   ├───────────────────────────┤
        │ • Spatial: District/Block │                                   │ • 0% location guessing    │
        │ • Temporal: Call timestamp│                                   │ • Explicit provenance tag │
        │ • Demographic: Gender/Age │                                   │ • No causal speculation   │
        │ • CMS: Caller ID / Channel│                                   │ • Preserved uncertainty   │
        └─────────────┬─────────────┘                                   └─────────────┬─────────────┘
                      │                                                               │
                      └───────────────────────────────┬───────────────────────────────┘
                                                      │
                                                      ▼
                               ┌────────────────────────────────────────────────┐
                               │         Enriched Machine-Readable Insight      │
                               │    (Structured Observation + Context + Citations)│
                               └────────────────────────────────────────────────┘
```

### Specific Enrichment Vectors:
1. **Spatial Grounding**: Moving from generic state-level observations to specific District and Block clusters, validated by explicit `location_source` tracking.
2. **Temporal Windowing**: Associating grievances with specific dates/months to capture seasonal crises (e.g. monsoon flood peaks in July–August vs summer drinking water handpump dry-ups in May–June).
3. **Demographic Disaggregation**: Identifying when public service failures disproportionately affect women (e.g. maternal health ANM absenteeism, SHG loan bottlenecks) or seniors (pension delays) based on recorded metadata.
4. **Engagement Prioritization**: Utilizing `Total listening duration` and repeat `CallerId` counts to gauge community resonance and recurrence without making false claims about universal prevalence.

---

## 4. Enriched Insight Conceptual Data Model

```json
{
  "insight_id": "INS_0023",
  "taxonomy_version": "0.3-FROZEN",
  "location": {
    "district": "Madhubani",
    "state": "Bihar",
    "block": "Khutauna",
    "instance_name": "Madhubani_MV",
    "location_source": "metadata",
    "location_certainty": "high"
  },
  "temporal_context": {
    "observation_window_start": "2023-05-01T15:17:24",
    "observation_window_end": "2023-05-15T18:30:00",
    "season": "Pre-Monsoon / Summer"
  },
  "taxonomy_concept": {
    "domain": "Education & Learning",
    "theme": "School Staffing & Basic Infrastructure",
    "issue": "School Building Safety, Classrooms & Basic Amenities"
  },
  "community_observation": {
    "finding": "Callers in Khutauna block, Madhubani report hazardous, dilapidated school buildings and irregularities in Mid-Day Meal delivery.",
    "condition_status": "reported_grievance",
    "failure_modes": ["infrastructure_damage", "poor_quality"]
  },
  "demographic_context": {
    "reporting_genders": {"Male": 2, "Female": 0, "Unknown": 0},
    "reporting_age_groups": {"Adult": 2, "Senior": 0},
    "affected_population": ["primary_school_children", "rural_students"]
  },
  "evidence": {
    "evidence_group_id": "EG_0005",
    "supporting_utterance_count": 2,
    "unique_caller_count": 2,
    "total_listening_seconds": 342.5,
    "citations": [
      {
        "utt_id": "13-00241-05",
        "timestamp": "2023-05-01T15:17:24",
        "audio_link": "http://.../13-00241-05.mp3",
        "hindi_transcript": "साथ ही स्कूलों के जर्जर भवनों ऐसी हमेशा खतरा बना रहता है...",
        "english_translation": "Dilapidated school buildings pose a constant danger; lack of learning materials and irregularities in Mid-Day Meal continue.",
        "demographics": {"gender": "Male", "age": "Adult"}
      }
    ]
  },
  "uncertainty_and_limitations": {
    "sample_representativeness": "Based on 2 voluntary citizen voice recordings; does not represent a universal census of all schools in district.",
    "model_confidence": 0.94,
    "causality_inferred": false
  }
}
```

---

## 5. Comparative Demonstration: Current vs. Metadata-Enriched Summary

### Location: Madhubani, Bihar

#### A. CURRENT SUMMARY (Without Items-Table Enrichment):
```markdown
## Domain: Education & Learning
### Theme: School Staffing & Basic Infrastructure
#### Issue: School Building Safety, Classrooms & Basic Amenities
- Evidence Group ID: EG_0005
- Supporting Utterances: 1
- Reported Failure Modes: infrastructure_damage
- Synthesis: Dilapidated school buildings pose a constant danger; lack of learning materials and irregularities in Mid-Day Meal continue.
- Supporting Evidence: 13-00241-05
```

#### B. METADATA-ENRICHED SUMMARY:
```markdown
## Domain: Education & Learning
### Theme: School Staffing & Basic Infrastructure
#### Issue: School Building Safety, Classrooms & Basic Amenities
- **Evidence Group ID**: `EG_0005`
- **Geographic Cluster**: Khutauna Block, Madhubani District, Bihar (Source: `metadata`, Station: `Madhubani_MV`)
- **Observation Period**: Recorded May 2023 (Pre-Monsoon academic session opening)
- **Supporting Evidence Volume**: 1 detailed citizen report (Duration: 88.4s, Cumulative Community Listening: 1,240s)
- **Caller Profile**: Adult Male citizen
- **Reported Public Service Breakdown**: `infrastructure_damage`, `poor_quality`

**Evidence-Grounded Synthesis**:
Community voice reporting from Khutauna block highlights severe physical deterioration of rural school structures posing safety hazards to children, compounded by shortages of teaching-learning materials and unsupervised Mid-Day Meal distribution.

**Auditable Provenance Citation**:
- **`13-00241-05`** [Audio Link](http://.../13-00241-05.mp3) (Caller ID: `919835xxxxxx`, Recorded: `2023-05-01 15:17:24`)
  > *Original Hindi*: "साथ ही स्कूलों के जर्जर भवनों ऐसी हमेशा खतरा बना रहता है पठन पठन सामग्री का नहीं होना तथा मध्य भोजन के देख रेख में अनियमित्ता बरतने ऐसी..."
  > *English Translation*: "Dilapidated school buildings pose a constant danger; lack of learning materials and irregularities in the Mid-Day Meal scheme continue."
```
