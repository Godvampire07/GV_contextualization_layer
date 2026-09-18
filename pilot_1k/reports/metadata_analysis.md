# Gram Vaani Metadata Utility Analysis (1,000 Utterances)

## 1. Categorized Metadata Utility Ledger

### A. Location & Administrative Metadata
- **`District` & `State`**: Primary spatial aggregation units. Enables district-level grievance summaries and mapping to Census / Aspirational District indicators.
- **`Block` (Tehsil)**: Available in external items table (`DAUV`/`KBBL`). Enables hyper-local grievance clustering around specific Block Development Offices (BDOs).
- **`Instance name`**: Voice station channel (e.g. `Ghazipur_MV`, `Varanasi_MV`). Essential for regional dialect normalization.

---

### B. Temporal Metadata
- **`Item created date` & `published date`**: ISO timestamps of recording and moderation. Enables time-series event detection, seasonal crisis tracking (monsoon floods vs summer droughts), and broadcast velocity analysis.

---

### C. Speaker & Demographic Metadata
- **`Gender` & `Age`**: Disaggregates community reports across gender lines (e.g. women callers reporting maternal health and SHG loan issues) and age cohorts (youth unemployment vs senior citizen pension delays).
- **`CallerId`**: Hashed telephone identifier. Enables caller deduplication and repeat-caller engagement intensity tracking.

---

### D. Audio Quality & Engagement Metadata
- **`Sentiment`**: Caller emotional tone (`Serious`, `Angry`, `Neutral`). Prioritizes high-urgency community distress calls.
- **`Total listening duration` & `Item duration`**: Captures community virality and listener interest across broadcasts.
