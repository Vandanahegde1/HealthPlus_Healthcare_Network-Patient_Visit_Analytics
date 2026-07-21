# HealthPlus Healthcare Network — Patient Visit Analytics

## Business Problem
Hospital networks often assume that longer wait times are the main driver of poor patient satisfaction, and default to investing in wait-time reduction as the fix. This analysis tests that assumption directly across a multi-clinic healthcare network, using patient visit, revenue, and satisfaction data to determine what's actually associated with satisfaction — and where operational investment would be better spent. Stakeholders are hospital administrators and clinic operations teams deciding where to focus improvement efforts across doctors, clinics, and departments.

## Dataset
- **Source:** Synthetic healthcare network dataset, provided as part of the Aspire Code AI Internship (mirrors real-world hospital operations, not real patient records)
- **Size:** 10,308 patient visits (fact table), connected to 5 dimension tables
- **Structure:** Star schema — Fact_Visits + Dim_Patients, Dim_Doctors, Dim_Services, Dim_Clinics, Dim_Calendar (full date dimension for time intelligence)
- **Key variables:** visit date, patient, service, doctor, clinic, fee charged, discount, revenue, insurance claimed, out-of-pocket cost, wait time, satisfaction score, follow-up flag, visit type

## Tools & Technologies
- **Python** (Pandas, Matplotlib, Seaborn) — exploratory data analysis in Jupyter/Colab
- **Power BI** — star schema data model, 15 DAX measures, 4-page interactive dashboard

## Data Model
- **Fact_Visits** — 10,308 records across visit date, patient, service, doctor, clinic, fee, discount, revenue, insurance claimed, out-of-pocket cost, wait time, satisfaction score, follow-up flag, visit type
- **Dim_Patients** — demographics, city, insurance provider, chronic condition, lifetime visit count
- **Dim_Doctors** — specialization, qualification, experience, shift, clinic city
- **Dim_Services** — service name, department, category, fee, primary doctor, duration
- **Dim_Clinics** — clinic name, city, state, region, type, pharmacy availability
- **Dim_Calendar** — full date dimension (year, quarter, month, week, day name, weekend flag, season), built specifically to support time-intelligence DAX rather than relying on the raw date column

## Key Questions Answered
1. Does longer patient wait time actually reduce satisfaction scores?
2. What seasonal patterns exist in visit volume across the year?
3. Which services and departments generate the most revenue?
4. Which departments carry the highest visit volume, and do they need more staffing attention?
5. How do individual doctors and clinics compare on volume, revenue, and satisfaction?

## Key Findings
- **Wait time and satisfaction score showed close to zero correlation.** The expected story — longer wait, lower satisfaction — didn't hold up in the data.
- **Visit volume is seasonal**, peaking in August and dropping to its lowest in July, indicating a staffing need that fluctuates through the year rather than staying flat.
- **A small number of services and departments account for a disproportionate share of total revenue** — useful for prioritizing where to invest operationally.
- **Diagnostics and OPD consistently have the highest visit volume** of any department, making them the most likely candidates for additional staffing.
- **Satisfaction scores cluster mostly between 3.5 and 5**, suggesting overall patient experience skews positive — which made the wait-time non-correlation even more notable, since satisfaction isn't uniformly low to begin with.

## Business Recommendations
1. **Don't prioritize wait-time reduction as a satisfaction lever on its own.** Since wait time shows close to zero correlation with satisfaction, budget aimed purely at speeding up visits is unlikely to move patient experience scores. Investigate doctor communication, service quality, and visit outcomes instead as more likely drivers.
2. **Plan staffing around the August peak and July trough** in visit volume rather than a flat year-round schedule.
3. **Direct operational investment toward the small set of high-revenue services and departments** identified in the analysis, rather than spreading resources evenly across all departments.
4. **Prioritize Diagnostics and OPD for additional staffing support**, given their consistently highest visit volumes.

## Dashboard / Visualisations
Four pages, each built around a different angle on the same data:

1. **Operation Overview** — high-level KPIs and trends across the whole network
2. **Patient Analysis** — demographics, chronic conditions, visit patterns by patient segment
3. **Doctor and Clinic Performance** — how individual doctors and clinics compare on volume, revenue, and satisfaction
4. **Department Detail** — a drillthrough page for digging into any single department's numbers directly from the other pages

All four pages share cross-page slicers, so filtering by date, clinic, or department on one page carries through to the others.

[Screenshot or link to live Power BI dashboard]

## A Note on Methodology
It would have been easy to assume the wait-time/satisfaction link and build a dashboard around confirming it. Testing that assumption directly — and being willing to report that it didn't hold — felt like the more honest and more useful version of this project. A dashboard that only tells you what you expected to hear isn't actually doing much analytical work.
