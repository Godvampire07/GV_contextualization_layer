# Conceptual Framework: Connecting Gram Vaani Taxonomy to External Development Indicators

## 1. Core Architecture & Principle

```text
Gram Vaani Community Voice Evidence
                 ↓
Gram Vaani Corpus-Grounded Semantic Taxonomy v0.3 (Source Layer)
                 ↓
    ┌────────────┼────────────┬────────────┬────────────┐
    ↓            ↓            ↓            ↓            ↓
  SDGs     Mission Antyodaya Census      CoRE Stack   GDELT
```

### The Fundamental Rule:
> **The Gram Vaani Taxonomy is the primary, immutable source semantic layer.**
> External frameworks (SDGs, Mission Antyodaya, Census, CoRE Stack, GDELT) are **downstream projection / contextualization layers**.
> Community evidence is NEVER forced directly into an SDG or external indicator.

---

## 2. External Framework Alignment Architecture

### A. Sustainable Development Goals (SDGs)
| GV Taxonomy Domain (v0.3) | Primary Mapped SDG | Key Target Indicators |
| :--- | :--- | :--- |
| **Agriculture & Allied Livelihoods** | **SDG 2: Zero Hunger** | 2.3 (Agricultural productivity), 2.4 (Sustainable food production systems). |
| **Water & Sanitation (WASH)** | **SDG 6: Clean Water & Sanitation** | 6.1 (Universal safe drinking water), 6.2 (Adequate sanitation and hygiene). |
| **Healthcare & Nutrition** | **SDG 3: Good Health & Well-Being** | 3.1 (Maternal mortality), 3.8 (Universal health coverage & essential medicines). |
| **Education & Skill Development** | **SDG 4: Quality Education** | 4.1 (Free primary & secondary education), 4.a (Inclusive school facilities). |
| **Energy & Rural Electrification** | **SDG 7: Affordable & Clean Energy** | 7.1 (Universal access to reliable electricity services). |
| **Rural Roads & Physical Connectivity** | **SDG 9: Industry, Innovation & Infrastructure** | 9.1 (Resilient rural transport infrastructure and all-weather roads). |
| **Governance & Social Entitlements** | **SDG 16: Peace, Justice & Strong Institutions** | 16.6 (Effective, accountable institutions), 16.10 (Public access to information). |
| **Women Empowerment & Gender Dynamics** | **SDG 5: Gender Equality** | 5.a (Equal rights to economic resources, financial services & SHG credit). |
| **Employment, Livelihoods & Migration** | **SDG 8: Decent Work & Economic Growth** | 8.5 (Decent work for all), 8.8 (Protect labor rights for migrant workers). |
| **Disaster & Climatic Vulnerability** | **SDG 13: Climate Action** | 13.1 (Strengthen resilience to climate-related hazards and natural disasters). |

---

### B. Mission Antyodaya (Panchayat Development Indicators)
Mission Antyodaya evaluates Gram Panchayat development across 29 sectors. The GV Taxonomy directly links citizen complaints to official GP infrastructure parameters:
- `Panchayat Grievances` → GP Bhawan availability, Regularity of Gram Sabha meetings.
- `Handpump Breakdown` / `Piped Water` → Functional piped water supply & functional public handpumps per 1,000 population.
- `Frequent Power Outages & Burnt Transformers` → Hours of domestic electricity supply per day, hours of agricultural power supply.
- `Anganwadi Nutrition Distribution` → Operational Anganwadi Centre within 1 km, ICDS supplementary nutrition delivery.
- `PDS Ration Distribution & Under-Weighing` → Fair Price Shop (FPS) operational status and e-PoS biometric transaction success.

---

### C. Census & Socio-Economic Indicators (Village Amenities)
Census of India District Census Handbooks (DCHB) provide village-level infrastructure baselines:
- **Village Amenity Directory**: All-weather pucca road connectivity, primary school within village, primary health sub-centre distance.
- **Household Amenities Census**: Source of drinking water (Handpump vs Treated Tap Water), Primary source of lighting (Electricity vs Kerosene).
- **GV Integration Value**: GV community voices provide **real-time functional status** (e.g. "Transformer burnt for 2 months") over static Census decennial infrastructure tags.

---

### D. CoRE Stack (Common Open Research Engine for Socio-Ecological Indicators)
CoRE Stack provides geospatial environmental and livelihood layers (groundwater levels, vegetation index NDVI, waterbody polygons):
- `Irrigation Water Availability` → Groundwater depth maps (CGWB) & surface waterbody presence.
- `Flood Inundation & Crop Loss` → Sentinel-1 Synthetic Aperture Radar (SAR) flood inundation polygons.
- `MGNREGA Work Demand & Delays` → GP-level MGNREGA muster roll expenditure data.

---

### E. GDELT (Global Data on Events, Location, and Tone)
GDELT captures media news events at sub-national levels:
- **Event Tag Mapping**: GDELT Protest events (CAMEO code 14) and Government Inaction events cross-referenced with localized Gram Vaani citizen grievance spikes.
- **Signal Triangulation**: Comparing news media coverage intensity with grassroots voice reporting intensity to detect under-reported rural crises.
