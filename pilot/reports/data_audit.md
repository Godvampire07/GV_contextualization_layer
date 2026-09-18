# Gram Vaani Pilot Pipeline: Data & Field Audit Report

## 1. Executive Summary & File Inventory
This audit documents the authoritative file sources, schemas, column mappings, and metadata availability for the Gram Vaani community voice analytics pipeline.

### Authoritative Files Inspected:
| File Path | Total Records | Format | Role in Pipeline |
| :--- | :--- | :--- | :--- |
| `data/master/gv_master_metadata.csv` | 37,152 rows | CSV (13 cols) | Primary Master Audio & Transcript Metadata Pool |
| `samples/taxonomy_discovery_1500.csv` | 1,500 rows | CSV (13 cols) | Discovery Sample (seed=42) |
| `validation/taxonomy_validation_200.csv` | 200 rows | CSV (13 cols) | Original Held-Out Validation Sample (seed=123) |
| `validation/taxonomy_validation_blind_200.csv` | 200 rows | CSV (13 cols) | Blind Held-Out Validation Sample (seed=999) |
| `taxonomy/gramvaani_taxonomy_v0.3.json` | 11 Domains, 22 Themes, 29 Issues | JSON | Frozen Semantic Taxonomy v0.3 |
| `taxonomy/gramvaani_content_type_schema.json` | 7 Modality Classes | JSON | Orthogonal Communication Modality Schema |
| `DAUV_tag.xlsx` & `KBBL_tag.xlsx` | 3,460 & 6,400+ rows | Excel | External Items Tables with Block, Timestamp & Channel Tags |

---

## 2. Field & Column Mapping Reference

| Pipeline Dimension | Source Field Name | Source File | Description & Format | Missingness Rate |
| :--- | :--- | :--- | :--- | :--- |
| **Audio Unique ID** | `utt_id` | Master CSV | Unique recording identifier (e.g. `13-00073-02`, `01-02614-01`). | **0.0% (0 / 37,152)** |
| **ASR Transcript (Hindi)** | `reference` | Master CSV | Devanagari Hindi speech-to-text transcript. | **0.0% (37,152 populated)** |
| **Translated Text (English)** | `translated_text` | Pilot Dataset | Faithful English translation of community speech. | **0.0% in Pilot** |
| **State Location** | `State` | Master CSV | State name (`Bihar`, `Jharkhand`, `Madhya_pradesh`, etc.). | **67.53% (25,087 / 37,152)** |
| **District Location** | `District` | Master CSV | District name (`Dhanbad`, `Munger`, `Samastipur`, etc.). | **99.79% (37,074 / 37,152)** |
| **Spoken Location Mention** | Spoken in `reference` | Master CSV | Caller explicitly stating district in audio transcript. | **~19.5% detectable** |
| **Gender Demographic** | `Gender` | Master CSV | `Male` (83.8%), `Female` (6.2%), `NaN` (10.0%). | **10.0% (3,715 / 37,152)** |
| **Age Demographic** | `Age` | Master CSV | `Adult` (88.7%), `Senior` (0.6%), `NaN` (10.7%). | **10.7% (3,980 / 37,152)** |
| **Acoustic Background** | `Background` | Master CSV | Background noise tag (e.g. `Clean`, `Noise`, `Music`). | **99.7% missing in master** |
| **Sentiment / Tone** | `Sentiment` | Master CSV | `Serious`, `Angry`, `Neutral`, `Happy`. | **95.2% missing in master** |
| **Audio File Link** | `audio_path` / `audio_drive_id` | Master CSV | Google Drive audio file ID & MP3 path. | **0.0% missing** |
| **Creation / Broadcast Date** | `Item created date` / `published date` | Items Tables (`DAUV`/`KBBL`) | ISO timestamp of call creation / broadcast. | **0.0% in Items Table** |
| **Taxonomy Labels** | `domain`, `theme`, `issue` | Taxonomy v0.3 | 3-level frozen hierarchical classification. | **Deterministic** |
| **Communication Modality** | `content_type` | Schema v0.3 | 7 orthogonal communication classes. | **Deterministic** |
| **Failure Modes** | `failure_mode` | Schema v0.3 | 8 orthogonal public service failure tags. | **Deterministic** |

---

## 3. Provenance & Location Quality Guardrail

> [!CAUTION]
> Because district metadata is missing in 99.79% of master CSV rows, the pipeline enforces a **3-tier location provenance attribute**:
> 1. `location_source = metadata`: Explicitly recorded in master CSV.
> 2. `location_source = transcript`: Explicitly spoken by caller in audio transcript (e.g. *"मैं समस्तीपुर जिला से बोल रहा हूँ"*).
> 3. `location_source = unknown`: Explicitly labeled as `Unspecified_District, Unspecified_State` to prevent geographical hallucinations.
