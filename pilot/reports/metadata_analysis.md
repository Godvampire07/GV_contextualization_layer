# Gram Vaani Metadata Analysis: Enhancing Location-Based Summaries & Insights

## 1. Overview
This analysis evaluates all available metadata attributes from the master corpus (`gv_master_metadata.csv`) and external items tables (`DAUV_tag.xlsx`, `KBBL_tag.xlsx`). The objective is to identify how each metadata field can enrich location-based summaries and enable multi-dimensional community insights without forcing non-topical metadata into the frozen taxonomy.

---

## 2. Categorized Metadata Taxonomy

### A. Identity & Provenance Metadata
| Field Name | Source | Description | Grouping Utility | Summarization Utility | Future Analysis Enabled |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `utt_id` | Master CSV | Unique recording ID (e.g. `13-00073-02`). | Primary key for record tracing. | Injected into summary citations for 100% auditability. | Longitudinal caller tracking across campaigns. |
| `Unique Item ID` | Items Table | Broadcast item ID in Gram Vaani CMS. | Cross-referencing platform items. | Links summaries to CMS broadcast items. | Platform CMS lifecycle analytics. |
| `CallerId` | Items Table | Hashed telephone number of caller. | Household/caller deduplication. | Flags repeat callers reporting recurring village issues. | Caller frequency & citizen engagement intensity. |
| `audio_drive_id` | Master CSV | Google Drive audio file ID. | Audio file retrieval key. | Allows one-click listening verification. | Direct audio playback in future web interfaces. |

---

### B. Location Metadata
| Field Name | Source | Description | Grouping Utility | Summarization Utility | Future Analysis Enabled |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `State` | Master CSV / Items Table | State name (Bihar, Jharkhand, UP, MP). | Macro-level state geographic aggregation. | Contextualizes state-specific welfare schemes. | State-level policy performance benchmarking. |
| `District` | Master CSV / Items Table | District name (Madhubani, Dhanbad, etc.). | Primary geographical aggregation unit. | Generates District Community Briefs. | Census & District Aspirational indicators. |
| `Block` | Items Table | Administrative sub-district / Tehsil. | Hyper-local block-level clustering. | Pinpoints specific Block Development Office (BDO) issues. | Mission Antyodaya GP/Block clustering. |
| `Instance name` | Items Table | Voice channel instance (e.g. `Ghazipur_MV`). | Identifies platform community radio station. | Contextualizes regional dialect nuances. | Station coverage & reach evaluation. |
| `location_source` | Pipeline | Provenance tag (`metadata`, `transcript`, `unknown`). | Prevents unverified location claims. | Alerts reader to geographic certainty level. | Data quality and NER confidence scoring. |

---

### C. Temporal Metadata
| Field Name | Source | Description | Grouping Utility | Summarization Utility | Future Analysis Enabled |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `Item created date` | Items Table | Timestamp of initial audio recording. | Temporal binning (monthly, seasonal, annual). | Identifies acute seasonal crises (monsoon floods, summer water scarcity). | Time-series trend analysis & event detection. |
| `published date` | Items Table | Timestamp when item was broadcast over IVR. | Moderation latency tracking. | Distinguishes fresh reports from re-broadcasts. | Platform turnaround & broadcast velocity. |

---

### D. Demographic & Affected Population Metadata
| Field Name | Source | Description | Grouping Utility | Summarization Utility | Future Analysis Enabled |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `Gender` | Master CSV | `Female`, `Male`, `Unknown`. | Gender-disaggregated evidence grouping. | Highlights women-specific concerns (maternal health, SHG loans). | Gender parity in civic grievance reporting. |
| `Age` | Master CSV | `Adult`, `Senior`, `Young`. | Age-cohort stratification. | Separates youth unemployment from elder pension delays. | Vulnerable population impact assessment. |
| `Accent` | Master CSV | Dialect indicator (e.g. `Bihari`, `Maithili`). | Linguistic / cultural clustering. | Validates regional translation accuracy. | Low-resource ASR adaptation. |

---

### E. Content & Structural Metadata
| Field Name | Source | Description | Grouping Utility | Summarization Utility | Future Analysis Enabled |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `content_type` | Schema v0.3 | 7 communication modalities. | Isolates grievances from radio station promos. | Prevents broadcast speech from distorting summaries. | True grievance vs informational volume ratios. |
| `topic_status` | Taxonomy v0.3 | `substantive`, `not_applicable`, `unknown`. | High-level data filtering filter. | Clean separation of development topics. | Zero-noise insight generation. |
| `failure_mode` | Schema v0.3 | 8 delivery failure classes. | Failure-mode cross-tabulation. | Explains *why* a public service failed (absenteeism vs corruption). | Systemic governance bottleneck diagnosis. |
| `tags` | Items Table | Editorial tags added by GV moderators. | Cross-thematic filtering. | Provides human-validated secondary keywords. | Hybrid human-in-the-loop taxonomy tuning. |

---

### F. Quality & Engagement Metadata
| Field Name | Source | Description | Grouping Utility | Summarization Utility | Future Analysis Enabled |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `Sentiment` | Master CSV | Caller emotional tone (`Serious`, `Angry`). | Distress / severity prioritization. | Identifies urgent, high-emotion community emergencies. | Sentiment-weighted grievance escalation. |
| `Item duration` | Items Table | Length of audio recording in seconds. | Filters out truncated calls (<5s). | Reflects depth and detail of caller grievance. | Speech density & narrative length modeling. |
| `Total listening duration` | Items Table | Cumulative seconds listeners listened to recording. | Community resonance & virality metric. | Identifies issues that resonate most widely across listeners. | Community priority weighting algorithms. |
