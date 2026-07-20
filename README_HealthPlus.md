# HealthPlus Healthcare Network — Patient Visit Analytics

## Why I built this

This one started as a question I kept coming back to while studying healthcare operations: does making patients wait longer actually make them less satisfied? I wanted a project substantial enough to test that kind of question properly — not just a single flat table, but something that mirrored how a real hospital network's data is actually structured.

So this project works with a proper star schema: one fact table of 10,308 patient visits, connected to five dimension tables — Patients, Doctors, Services, Clinics, and a full Calendar dimension for time intelligence. It's built to reflect how a multi-clinic healthcare network would actually track visits, revenue, wait times, and satisfaction across departments and locations.

## Data source

The dataset was provided as part of the **Aspire Code AI Internship** — a synthetic healthcare network dataset built to mirror real-world hospital operations, not real patient records. I used it as the foundation to build out my own data model, EDA, and dashboard from scratch.

## Tools used

- **Python (Pandas, Matplotlib, Seaborn)** — exploratory data analysis in Jupyter/Colab
- **Power BI** — star schema data model, DAX measures, and a 4-page interactive dashboard

## The data model

- **Fact_Visits** — 10,308 records: visit date, patient, service, doctor, clinic, fee charged, discount, revenue, insurance claimed, out-of-pocket cost, wait time, satisfaction score, follow-up flag, visit type
- **Dim_Patients** — demographics, city, insurance provider, chronic condition, lifetime visit count
- **Dim_Doctors** — specialization, qualification, experience, shift, clinic city
- **Dim_Services** — service name, department, category, fee, primary doctor, duration
- **Dim_Clinics** — clinic name, city, state, region, type, pharmacy availability
- **Dim_Calendar** — a full date dimension (year, quarter, month, week, day name, weekend flag, season) built specifically to support proper time-intelligence DAX rather than relying on the raw date column directly

## The Python / EDA side

Before touching Power BI, I explored the dataset in Python to get a feel for what was actually going on in the numbers. A few things that came out of that:

- **Monthly visit trends** — patient visits fluctuate through the year, with August recording the highest volume and July the lowest, suggesting seasonal demand that a hospital would need to staff around.
- **Revenue with rolling averages** — I compared 3-month and 6-month rolling averages against raw monthly revenue, which made it much easier to separate genuine trend from short-term noise.
- **Top revenue services and departments** — a small number of services and departments account for a disproportionate share of total revenue, which is a useful thing for a hospital to know when deciding where to invest.
- **Diagnostics and OPD** consistently had the highest visit volume of any department, meaning they're the ones most likely to need extra staffing attention.
- **Satisfaction scores** clustered mostly between 3.5 and 5, suggesting the overall patient experience skews positive — but this is exactly what led me to the bigger question the Power BI side digs into.

## The Power BI dashboard

Four pages, each built around a different angle on the same data:

1. **Operation Overview** — high-level KPIs and trends across the whole network
2. **Patient Analysis** — demographics, chronic conditions, visit patterns by patient segment
3. **Doctor and Clinic Performance** — how individual doctors and clinics compare on volume, revenue, and satisfaction
4. **Department Detail** — a drillthrough page for digging into any single department's numbers directly from the other pages

All four pages share cross-page slicers, so filtering by date, clinic, or department on one page carries through to the others — meant to feel like one connected tool rather than four separate reports.

## The key finding

The most interesting result in this whole project was a negative one: **wait time and satisfaction score showed close to zero correlation.** I went in expecting the obvious story — longer wait, lower satisfaction — and the data just didn't back that up.

That's not a failed analysis, though. If anything, it's a more useful finding for a hospital to have, because it means throwing money at reducing wait times alone probably wouldn't move patient satisfaction much on its own. Whatever's actually driving how patients feel about their visit, it isn't sitting in the wait-time column  which points toward things like doctor communication, service quality, or the actual outcome of the visit as more likely drivers, and that's a genuinely different (and more useful) recommendation than "reduce wait times."

## A note on how I approached this

It would have been easy to assume the wait-time/satisfaction link and build a dashboard around confirming it. Testing that assumption directly instead  and being willing to report that it didn't hold felt like the more honest and more useful version of this project. A dashboard that only tells you what you expected to hear isn't actually doing much analytical work.
