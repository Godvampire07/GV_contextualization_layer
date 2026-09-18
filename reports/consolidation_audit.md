# Gram Vaani Concept Consolidation Audit

## Executive Summary
This audit inspects the **58 canonical concepts** generated during the synonym consolidation stage.

### Key Findings:
1. **Properly Merged Synonyms**: Dialectal and lexical variants of water shortage (`water shortage`, `water scarcity`, `lack of water`, `सूखा`) were successfully consolidated into `Irrigation Water Availability` and `Handpump Breakdown`.
2. **Preserved Distinctions**: Critical operational distinctions were correctly maintained without collapsing (e.g., `Crop Pricing & MSP Procurement` was NOT merged into `Crop Protection & Pest Damage`; `Distress Out-Migration` was NOT merged into `Deficit of Local Livelihood Opportunities`).
3. **Questionable Mergers**: `Civic Information & Community Announcements` absorbed a disproportionate number of generic labels (`General Community Update`, `Civic Information Dissemination`, `General Public Grievance`), creating an oversized bucket.
4. **Vague English Labels**: Labels like `General Public Grievance` or `Civic Information Dissemination` are too generic to link to specific CoRE or Census indicators.

---

## Canonical Concepts Detail Table

| ID | Canonical Name | Type | Parent | Source Utterances | Aliases | Assessment |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `irrigation_water_availability` | **Irrigation Water Availability** | issue | `irrigation_and_water_management` | 6 | Water Availability for Irrigation<br>irrigation water shortage<br>canal water sc | Strong |
| `irrigation_power_and_infrastructure` | **Irrigation Infrastructure & Power Supply** | issue | `irrigation_and_water_management` | 0 | agricultural motor power outage<br>burnt transformer for tubewells<br>canal brea | Low Evidence (<5) |
| `irrigation_and_water_management` | **Irrigation & Agricultural Water** | theme | `agriculture` | 6 | Irrigation & Agricultural Water | Strong |
| `fertilizer_and_seed_shortage` | **Fertilizer & Seed Supply Shortages** | issue | `agricultural_inputs_and_seeds` | 18 | Fertilizer & Seed Supply Shortage<br>urea scarcity<br>black marketing of fertili | Strong |
| `pest_infestation_and_crop_disease` | **Pest Infestation & Crop Diseases** | issue | `agricultural_inputs_and_seeds` | 6 | Pest Infestation & Crop Damage<br>crop blight<br>insect damage<br>plant disease  | Strong |
| `agricultural_inputs_and_seeds` | **Agricultural Inputs & Technology** | theme | `agriculture` | 24 | Agricultural Inputs & Technology | Strong |
| `crop_pricing_and_msp_access` | **Crop Pricing & MSP Procurement** | issue | `agricultural_markets_and_pricing` | 8 | Crop Pricing & Market Access<br>distress crop sale<br>delayed PACS procurement<b | Strong |
| `agricultural_markets_and_pricing` | **Agricultural Markets & Pricing** | theme | `agriculture` | 8 | Agricultural Markets & Pricing | Strong |
| `agriculture` | **Agriculture & Allied Activities** | domain | `None` | 36 | Agriculture & Allied Activities | Strong |
| `handpump_and_groundwater_breakdown` | **Handpump Breakdown & Groundwater Depletion** | issue | `drinking_water_access` | 9 | Handpump & Tap Water Breakdown<br>broken chapakal<br>dry handpumps<br>chapakal r | Strong |
| `piped_water_scheme_irregularity` | **Piped Water Scheme Delivery Irregularity** | issue | `drinking_water_access` | 2 | Piped Water Scheme Irregularity<br>Nal Jal Yojana failure<br>irregular tap water | Low Evidence (<5) |
| `drinking_water_access` | **Potable Drinking Water Supply** | theme | `water_and_sanitation` | 11 | Potable Drinking Water Supply | Strong |
| `drainage_overflow_and_waste_accumulation` | **Drainage Overflow & Waste Accumulation** | issue | `sanitation_and_drainage` | 24 | Lack of Drainage & Sanitation Facilities<br>waterlogging in village lanes<br>ope | Strong |
| `sanitation_and_drainage` | **Sanitation & Village Drainage** | theme | `water_and_sanitation` | 24 | Sanitation & Village Drainage | Strong |
| `water_and_sanitation` | **Water & Sanitation (WASH)** | domain | `None` | 31 | Water & Sanitation (WASH) | Strong |
| `doctor_absence_and_medicine_shortage` | **Doctor Absenteeism & Essential Drug Shortages** | issue | `healthcare_access_and_facilities` | 52 | Doctor Absence & Medicine Shortage<br>absent doctor at PHC<br>lack of medicines  | Strong |
| `emergency_transport_and_ambulance` | **Emergency Medical Transport & Ambulance Access** | issue | `healthcare_access_and_facilities` | 0 | lack of ambulance service<br>102 ambulance delay<br>maternity emergency transpor | Low Evidence (<5) |
| `healthcare_access_and_facilities` | **Primary Healthcare Access & Facilities** | theme | `health_and_nutrition` | 52 | Primary Healthcare Access & Facilities | Strong |
| `vaccination_and_immunization_coverage` | **Routine Immunization & Vaccination Delivery** | issue | `maternal_child_health_and_nutrition` | 5 | Vaccination & Immunization Coverage<br>immunization camp irregularity<br>missed  | Strong |
| `anganwadi_nutrition_distribution` | **Anganwadi Supplementary Nutrition Distribution** | issue | `maternal_child_health_and_nutrition` | 3 | Anganwadi Nutrition Distribution Issues<br>poor anganwadi meal quality<br>THR di | Low Evidence (<5) |
| `maternal_child_health_and_nutrition` | **Maternal, Child Health & Nutrition** | theme | `health_and_nutrition` | 8 | Maternal, Child Health & Nutrition | Strong |
| `health_and_nutrition` | **Health & Nutrition** | domain | `None` | 57 | Health & Nutrition | Strong |
| `teacher_shortage_and_absenteeism` | **Teacher Shortage & Teacher Absenteeism** | issue | `school_infrastructure_and_staffing` | 19 | Teacher Shortage & Absenteeism<br>single-teacher schools<br>irregular teacher at | Strong |
| `dilapidated_school_buildings` | **Dilapidated School Buildings & Basic Amenities** | issue | `school_infrastructure_and_staffing` | 0 | damaged school building<br>lack of school drinking water<br>broken school bounda | Low Evidence (<5) |
| `school_infrastructure_and_staffing` | **School Infrastructure & Staffing** | theme | `education` | 19 | School Infrastructure & Staffing | Strong |
| `midday_meal_quality_and_regularity` | **Mid-Day Meal Quality & Regularity** | issue | `school_entitlements_and_nutrition` | 4 | Mid-Day Meal Quality & Irregularity<br>substandard school food<br>irregular MDM  | Low Evidence (<5) |
| `scholarship_and_uniform_entitlements` | **Scholarship & Student Entitlement Disbursement** | issue | `school_entitlements_and_nutrition` | 7 | Scholarship & Uniform Entitlements<br>delayed student scholarship<br>uniform mon | Strong |
| `school_entitlements_and_nutrition` | **School Meals & Student Entitlements** | theme | `education` | 11 | School Meals & Student Entitlements | Strong |
| `education` | **Education & Learning** | domain | `None` | 27 | Education & Learning | Strong |
| `dilapidated_roads_and_bridges` | **Dilapidated Roads & Missing Culverts** | issue | `roads_and_connectivity` | 31 | Dilapidated Roads & Missing Bridges<br>pothole-ridden road<br>broken bridge<br>u | Strong |
| `roads_and_connectivity` | **Rural Roads & Physical Connectivity** | theme | `infrastructure_and_energy` | 31 | Rural Roads & Physical Connectivity | Strong |
| `power_outages_and_transformer_breakdown` | **Frequent Power Outages & Burnt Transformers** | issue | `electricity_supply_and_grid` | 48 | Frequent Power Outages & Burnt Transformers<br>low voltage issues<br>transformer | Strong |
| `electricity_supply_and_grid` | **Electricity Supply & Power Grid** | theme | `infrastructure_and_energy` | 48 | Electricity Supply & Power Grid | Strong |
| `infrastructure_and_energy` | **Infrastructure & Energy** | domain | `None` | 79 | Infrastructure & Energy | Strong |
| `pds_ration_shortage_and_irregularity` | **PDS Ration Under-weighing & Irregular Distribution** | issue | `public_distribution_system` | 10 | PDS Ration Under-weighing & Black Marketing<br>ration dealer cut<br>grain divers | Strong |
| `public_distribution_system` | **Public Distribution System (PDS) & Food Security** | theme | `governance_and_social_welfare` | 10 | Public Distribution System (PDS) & Food Security | Strong |
| `delayed_pension_disbursement` | **Delayed Social Pension Disbursement** | issue | `social_security_pensions` | 9 | Delayed Pension Disbursement<br>unpaid old age pension<br>widow pension pending< | Strong |
| `social_security_pensions` | **Social Security Pensions** | theme | `governance_and_social_welfare` | 9 | Social Security Pensions | Strong |
| `mgnrega_wage_delays_and_work_allotment` | **MGNREGA Wage Delays & Work Allocation** | issue | `rural_employment_guarantee_mgnrega` | 7 | MGNREGA Wage Payment Delays & Work Allotment<br>pending MGNREGA wages<br>job car | Strong |
| `rural_employment_guarantee_mgnrega` | **Rural Employment Guarantee (MGNREGA)** | theme | `governance_and_social_welfare` | 7 | Rural Employment Guarantee (MGNREGA) | Strong |
| `administrative_unresponsiveness` | **Administrative Unresponsiveness & Corruption Concerns** | issue | `local_governance_accountability` | 83 | Lack of Administrative Accountability<br>panchayat secretary absence<br>bribery  | Strong |
| `local_governance_accountability` | **Local Governance & Administrative Redressal** | theme | `governance_and_social_welfare` | 83 | Local Governance & Administrative Redressal | Strong |
| `governance_and_social_welfare` | **Governance & Social Entitlements** | domain | `None` | 102 | Governance & Social Entitlements | Strong |
| `lack_of_local_livelihood_opportunities` | **Deficit of Local Non-Farm Livelihood Opportunities** | issue | `local_livelihoods_and_wages` | 12 | Lack of Local Livelihood Opportunities<br>rural unemployment<br>lack of factory  | Strong |
| `local_livelihoods_and_wages` | **Local Employment & Wage Work** | theme | `employment_and_livelihoods` | 12 | Local Employment & Wage Work | Strong |
| `distress_out_migration` | **Distress Out-Migration for Work** | issue | `labor_migration` | 22 | Distress Out-Migration for Work<br>interstate labor migration<br>migrant worker  | Strong |
| `labor_migration` | **Labor Migration & Worker Welfare** | theme | `employment_and_livelihoods` | 22 | Labor Migration & Worker Welfare | Strong |
| `employment_and_livelihoods` | **Employment, Livelihoods & Migration** | domain | `None` | 34 | Employment, Livelihoods & Migration | Strong |
| `housing_scheme_installment_delays` | **Housing Scheme Installment Delays & Exclusion** | issue | `rural_housing_schemes` | 9 | Pradhan Mantri Awas Yojana Installment Delays<br>PMAY list exclusion<br>delayed  | Strong |
| `rural_housing_schemes` | **Rural Housing Assistance** | theme | `housing_and_disaster` | 9 | Rural Housing Assistance | Strong |
| `flood_damage_and_relief_delays` | **Flood Inundation & Delayed Relief Assistance** | issue | `disaster_and_flood_relief` | 1 | Flood Damage & Delayed Compensation<br>flood compensation delay<br>crop submerge | Low Evidence (<5) |
| `disaster_and_flood_relief` | **Disaster Vulnerability & Flood Relief** | theme | `housing_and_disaster` | 1 | Disaster Vulnerability & Flood Relief | Strong |
| `housing_and_disaster` | **Housing & Disaster Resilience** | domain | `None` | 10 | Housing & Disaster Resilience | Strong |
| `shg_credit_and_livelihood_support` | **SHG Micro-Credit & Livelihood Mobilization** | issue | `women_empowerment_and_shgs` | 14 | SHG Credit & Livelihood Support<br>Jeevika group loan delays<br>SHG meeting faci | Strong |
| `women_empowerment_and_shgs` | **Women Empowerment & Self-Help Groups** | theme | `community_and_culture` | 14 | Women Empowerment & Self-Help Groups | Strong |
| `community_updates_and_public_notices` | **Civic Information & Community Announcements** | issue | `civic_awareness_and_community_affairs` | 936 | General Community Update<br>Civic Information Dissemination<br>General Public Gr | Overly Dominant |
| `civic_awareness_and_community_affairs` | **Community Information & Civic Updates** | theme | `community_and_culture` | 936 | Community Information & Civic Updates | Strong |
| `community_and_culture` | **Community & Civic Life** | domain | `None` | 950 | Community & Civic Life | Strong |

## Detailed Category-by-Category Analysis

### 1. Concepts Correctly Consolidated
- `irrigation_water_availability`: Successfully merged canal water deficit, tube well water shortage, and drought stress without blurring into general drinking water.
- `fertilizer_and_seed_shortage`: Consolidated urea shortage, DAP non-availability, and seed quality issues under agricultural inputs.
- `doctor_absence_and_medicine_shortage`: Merged absent medical officers at PHCs and lack of free generic medicines into primary healthcare service delivery.
- `pds_ration_shortage_and_irregularity`: Unified ration dealer cuts, grain diversion, and monthly distribution delays into PDS delivery irregularity.

### 2. Concepts That Should Be Split or Refined in Future Versions
- `community_updates_and_public_notices`: Currently aliases `General Community Update`, `Civic Information Dissemination`, and `General Public Grievance`. This lumps radio bumpers, cultural chatter, and genuine unclassified public grievances together.
- `drainage_overflow_and_waste_accumulation`: Bundles village drain blockage with lack of dustbins; drain waterlogging in alleys is an urgent sanitation crisis, whereas solid waste is a municipal amenity issue.

### 3. Vague Aliases Requiring Disambiguation
- `General Public Grievance`: Should be mapped to a dedicated `Unspecified Citizen Grievance` holding category rather than absorbed into Community Information.
- `General Community Update`: Should be formally partitioned into `Platform Audio Bumpers/Greetings` vs `Local Development News`.