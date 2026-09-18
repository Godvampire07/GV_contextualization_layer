# Gram Vaani Taxonomy v0.3: Conceptual Indicator Crosswalk & Alignment Examples

## 1. Executive Summary & Verification Guardrail
This document presents **10 real conceptual crosswalk examples** connecting validated Gram Vaani Taxonomy v0.3 issues to external socio-economic and ecological indicator frameworks.

> [!WARNING]
> This document represents a **conceptual interoperability design exercise**, NOT a declaration that formal external database integrations are complete.
> Formal mappings will be established only after full-corpus extraction and empirical correlation testing against Census, Mission Antyodaya, and CoRE Stack datasets.

---

## 2. Ten Representative Conceptual Crosswalk Demonstrations

### Example 1: `Frequent Power Outages, Low Voltage & Burnt Transformers`
- **GV Taxonomy Path**: `Energy & Rural Electrification` $\longrightarrow$ `Rural Electricity & Power Grid` $\longrightarrow$ `frequent_power_outages_and_transformers`.
- **GV Corpus Definition**: Recurrent power outages, low-voltage surges damaging appliances, and unaddressed burnt electrical transformers.
- **Socio-Economic Dimension**: Rural Infrastructure Reliability & Energy Access Quality.
- **Candidate External Frameworks**:
  1. **UN SDG**: `SDG 7.1.1` (Proportion of population with access to electricity) $\longrightarrow$ **Relationship: `narrower_concept`**.
  2. **Mission Antyodaya**: Parameter `MA_ELEC_02` (Daily hours of domestic electricity) $\longrightarrow$ **Relationship: `contextual_relationship`**.
  3. **Census 2011 DCHB**: `Power Supply (Domestic / Agriculture)` $\longrightarrow$ **Relationship: `contextual_relationship`**.
- **Required Verification Evidence**: Gram Panchayat spatial join between GV transformer complaint spikes and official DISCOM feeder outage logs.

---

### Example 2: `Doctor Absenteeism & Essential Drug Shortages`
- **GV Taxonomy Path**: `Healthcare & Nutrition` $\longrightarrow$ `Primary Healthcare Access & Facilities` $\longrightarrow$ `doctor_absence_and_medicine_shortage`.
- **GV Corpus Definition**: Absence of MBBS doctors and ANMs at Primary Health Centres (PHCs) and stockouts of free essential medicines.
- **Socio-Economic Dimension**: Universal Health Coverage, Rural Health Facility Functionality.
- **Candidate External Frameworks**:
  1. **UN SDG**: `SDG 3.8.1` (Coverage of essential health services) & `SDG 3.c.1` (Health worker density) $\longrightarrow$ **Relationship: `narrower_concept`**.
  2. **Mission Antyodaya**: Parameter `MA_HLTH_01` (PHC / Sub-Centre functional with staff) $\longrightarrow$ **Relationship: `direct_correspondence`**.
  3. **NITI Aayog Aspirational Districts**: Indicator `H4` (Percentage of functional Sub-centres/PHCs) $\longrightarrow$ **Relationship: `direct_correspondence`**.
- **Required Verification Evidence**: Correlation between caller PHC unresponsiveness complaints and district National Health Mission (NHM) staffing rosters.

---

### Example 3: `Dilapidated Roads, Potholes & Missing Culverts`
- **GV Taxonomy Path**: `Rural Roads & Physical Connectivity` $\longrightarrow$ `Village Road Infrastructure` $\longrightarrow$ `dilapidated_roads_potholes_and_culverts`.
- **GV Corpus Definition**: Physical deterioration of village paved roads, unpaved muddy road stretches, potholes, and broken culverts.
- **Socio-Economic Dimension**: Rural Transport Logistics, Physical Market Access, Emergency Evacuation.
- **Candidate External Frameworks**:
  1. **UN SDG**: `SDG 9.1.1` (Proportion of rural population who live within 2 km of an all-season road) $\longrightarrow$ **Relationship: `direct_correspondence`**.
  2. **Mission Antyodaya**: Parameter `MA_ROAD_01` (Is village connected by all-weather paved road) $\longrightarrow$ **Relationship: `contextual_relationship`**.
  3. **Census 2011 DCHB**: `Approach to Village (Pucca / Kuchha Road)` $\longrightarrow$ **Relationship: `contextual_relationship`**.
- **Required Verification Evidence**: Geospatial overlap of PMGSY asset maintenance records with citizen road condition grievance clusters.

---

### Example 4: `PDS Ration Distribution & Under-Weighing`
- **GV Taxonomy Path**: `Governance & Social Entitlements` $\longrightarrow$ `Food Security & PDS Access` $\longrightarrow$ `pds_ration_cuts_and_irregularity`.
- **GV Corpus Definition**: Ration dealers cutting grain allocations (1–2 kg per card), overcharging, irregular shop opening, and card cancellation.
- **Socio-Economic Dimension**: Food Security, Social Protection Integrity, Public Distribution Accountability.
- **Candidate External Frameworks**:
  1. **UN SDG**: `SDG 2.1.2` (Prevalence of moderate or severe food insecurity) $\longrightarrow$ **Relationship: `related_concept`**.
  2. **Mission Antyodaya**: Parameter `MA_PDS_01` (Functional Fair Price Shop in Gram Panchayat) $\longrightarrow$ **Relationship: `direct_correspondence`**.
  3. **NFHS-5 (National Family Health Survey)**: `Household Food Access & Targeted PDS Coverage` $\longrightarrow$ **Relationship: `related_concept`**.
- **Required Verification Evidence**: Comparison of Annavitran e-PoS transaction records with localized ration dealer under-weighing reports.

---

### Example 5: `Wage Payment Delays & Compensation (MGNREGA)`
- **GV Taxonomy Path**: `Employment, Livelihoods & Migration` $\longrightarrow$ `Rural Wage Employment Schemes` $\longrightarrow$ `mgnrega_wage_delays_and_work`.
- **GV Corpus Definition**: Unreasonable delays (3–6 months) in crediting MGNREGA wages to worker bank accounts and denial of work muster rolls.
- **Socio-Economic Dimension**: Social Safety Nets, Rural Liquidity, Distress Labor Protection.
- **Candidate External Frameworks**:
  1. **UN SDG**: `SDG 8.5.1` (Equal pay for work of equal value) & `SDG 1.3.1` (Social protection coverage) $\longrightarrow$ **Relationship: `narrower_concept`**.
  2. **MoRD MGNREGA MIS**: `NREGA Soft FTO (Fund Transfer Order) Stage-2 Delay Indicator` $\longrightarrow$ **Relationship: `direct_correspondence`**.
  3. **Mission Antyodaya**: Parameter `MA_NREGA_01` (Number of households provided 100 days of work) $\longrightarrow$ **Relationship: `related_concept`**.
- **Required Verification Evidence**: Timestamp correlation between MGNREGA MIS fund release delays and voice grievance spikes.

---

### Example 6: `Irrigation Water Availability`
- **GV Taxonomy Path**: `Agriculture & Allied Livelihoods` $\longrightarrow` `Irrigation & Agricultural Water` $\longrightarrow$ `irrigation_water_availability`.
- **GV Corpus Definition**: Adequacy, timing, and infrastructure accessibility of irrigation water from canals, government borewells, and private tubewells.
- **Socio-Economic & Ecological Dimension**: Agricultural Productivity, Groundwater Depletion, Smallholder Climate Resilience.
- **Candidate External Frameworks**:
  1. **UN SDG**: `SDG 6.4.2` (Level of water stress: freshwater withdrawal) $\longrightarrow$ **Relationship: `related_concept`**.
  2. **Census 2011 DCHB**: `Irrigated Area by Source (Canals, Tubewells, Tanks, Wells)` $\longrightarrow$ **Relationship: `contextual_relationship`**.
  3. **CoRE Stack**: `CGWB Groundwater Level Anomaly Layer` & `Sentinel-2 NDVI Vegetation Vigor` $\longrightarrow$ **Relationship: `contextual_relationship`**.
- **Required Verification Evidence**: Overlay of canal tail-end drying grievances on Sentinel-2 NDVI vegetative stress indices.

---

### Example 7: `Teacher Shortage & Teacher Absenteeism`
- **GV Taxonomy Path**: `Education & Learning` $\longrightarrow$ `School Staffing & Basic Infrastructure` $\longrightarrow$ `teacher_shortage_and_absenteeism`.
- **GV Corpus Definition**: Inadequate teacher strength, single-teacher schools, non-attendance of primary school teachers, and untrained para-teachers.
- **Socio-Economic Dimension**: Primary Education Quality, Pupil-Teacher Ratio (PTR), Foundational Literacy.
- **Candidate External Frameworks**:
  1. **UN SDG**: `SDG 4.1.1` (Minimum proficiency in reading/math) & `SDG 4.c.1` (Proportion of qualified teachers) $\longrightarrow$ **Relationship: `narrower_concept`**.
  2. **UDISE+ (Unified District Information System for Education)**: `Pupil-Teacher Ratio (PTR)` & `Single-Teacher Primary Schools` $\longrightarrow$ **Relationship: `direct_correspondence`**.
  3. **ASER (Annual Status of Education Report)**: `Rural Teacher Attendance Rate` $\longrightarrow$ **Relationship: `direct_correspondence`**.
- **Required Verification Evidence**: Comparison of school-level UDISE+ vacancy data with caller teacher absenteeism petitions.

---

### Example 8: `Aadhaar, Voter ID & Bank DBT Seeding Hurdles`
- **GV Taxonomy Path**: `Governance & Social Entitlements` $\longrightarrow$ `Citizen Identity & Documentation Access` $\longrightarrow$ `aadhaar_voter_id_and_dbt_hurdles`.
- **GV Corpus Definition**: Biometric mismatches, bank account-Aadhaar de-linking, NPCI mapper failures, and voter ID documentation lockouts.
- **Socio-Economic Dimension**: Digital Inclusion, Last-Mile Direct Benefit Transfer (DBT) Friction, Legal Identity.
- **Candidate External Frameworks**:
  1. **UN SDG**: `SDG 16.9.1` (Proportion of population with legal identity) $\longrightarrow$ **Relationship: `related_concept`**.
  2. **DBT Bharat Portal**: `DBT Transaction Failure Rate due to Aadhaar-Bank Account Mismatch` $\longrightarrow$ **Relationship: `direct_correspondence`**.
  3. **Mission Antyodaya**: Parameter `MA_BANK_01` (Availability of Banking Correspondent / CSP in GP) $\longrightarrow$ **Relationship: `related_concept`**.
- **Required Verification Evidence**: Analysis of NPCI Aadhaar Payment Bridge System (APBS) rejection logs against citizen bank lockout calls.

---

### Example 9: `SHG Micro-Credit & Livelihood Mobilization (Jeevika/SRLM)`
- **GV Taxonomy Path**: `Civic Action & Community Mobilization` $\longrightarrow$ `Women Empowerment & Self-Help Groups` $\longrightarrow$ `shg_microcredit_and_livelihood_mobilization`.
- **GV Corpus Definition**: Community mobilization, micro-credit pooling, bank linkage loans, and livelihoods enterprise development by women's SHGs.
- **Socio-Economic Dimension**: Women's Financial Inclusion, Grassroots Institution Building, Collective Efficacy.
- **Candidate External Frameworks**:
  1. **UN SDG**: `SDG 5.a.1` (Women's ownership and equal rights to financial services) $\longrightarrow$ **Relationship: `direct_correspondence`**.
  2. **DAY-NRLM / Jeevika MIS**: `SHG Bank Credit Linkage Disbursement & NPA Rate` $\longrightarrow$ **Relationship: `direct_correspondence`**.
  3. **Mission Antyodaya**: Parameter `MA_SHG_01` (Number of active Women SHGs in Gram Panchayat) $\longrightarrow$ **Relationship: `direct_correspondence`**.
- **Required Verification Evidence**: Spatial correlation between Jeevika meeting announcements on GV and district SRLM credit absorption metrics.

---

### Example 10: `Monsoon Floods, River Erosion & Crop Inundation`
- **GV Taxonomy Path**: `Disaster & Climatic Vulnerability` $\longrightarrow$ `Monsoon Floods & River Inundation` $\longrightarrow$ `flood_inundation_and_relief_delays`.
- **GV Corpus Definition**: Embankment breaches, village river inundation, standing crop destruction, livestock fodder loss, and delayed disaster relief.
- **Socio-Economic & Ecological Dimension**: Climate Hazard Exposure, Disaster Vulnerability, Post-Disaster Social Safety.
- **Candidate External Frameworks**:
  1. **UN SDG**: `SDG 13.1.1` (Number of persons affected by disaster per 100,000 population) $\longrightarrow$ **Relationship: `direct_correspondence`**.
  2. **CoRE Stack / Sentinel-1 SAR**: `Surface Water Flood Inundation Extent Polygon Layers` $\longrightarrow$ **Relationship: `direct_correspondence`**.
  3. **GDELT Project**: `CAMEO Event Code 10 (Disaster / Humanitarian Aid Request)` $\longrightarrow$ **Relationship: `contextual_relationship`**.
- **Required Verification Evidence**: Spatio-temporal coincidence between caller flood SOS recordings and Sentinel-1 SAR radar water extent masks.
