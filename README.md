# True Cross Health System: Inpatient Performance and Population Health Dashboard

**Tools:** Power BI
**Data:** Inpatient admission records for five hospitals in Ohio, January 2023 to December 2025: 104,270 admissions for 100,000 patients on record (53,776 of whom were admitted), covering admissions, discharge details, diagnoses, outcomes, treatment costs and linked patient and survey information where available. It contains no real patient information.

## Business overview
True Cross Health System is a network of hospitals serving communities in Ohio, United States, providing emergency, inpatient, surgical, diagnostic and specialist care. Each hospital serves a different patient population and faces different levels of demand, clinical complexity and operational pressure. Management wants a consistent view of performance across the network.

## The business problem
True Cross needs to understand why inpatient performance differs across its five hospitals. Management wants to investigate four problems:
- **Uneven patient demand:** which hospitals and departments handle the most admissions, and how demand changes over time
- **Long hospital stays:** which hospitals and patient groups have longer stays, allowing for diagnosis and clinical severity
- **Discharge delays:** where delays are greatest and which patients are most affected


## Project aim
Build a two-page Power BI report that gives management a single, consistent view of inpatient demand, treatment cost, length of stay, outcomes and patient health profiles across the hospital network.

## Business questions this dashboard answers
- How many inpatient admissions occurred, and how does demand vary across the year?
- Which hospitals, admission types and departments account for the largest admission volumes?
- How much treatment cost is documented, and how is it split across payer types and departments?
- What are the average length of stay, complication rate and in-hospital mortality rate?
- Which departments have higher volumes, longer stays and higher satisfaction?
- How many patients are on record, how many were admitted, and how many have cancer, hypertension, obesity or cardiovascular disease?
- What proportion of patients have two or more recorded chronic conditions?
- How does the admitted population differ by smoking status?
- How satisfied are patients who returned scored inpatient surveys?

## My role and approach
1. **Prepared the data** 
2. **Built the data model:** a star schema with a fact table (`FactHospitalAdmissions`) linked to dimension tables.
3. **Created measures in DAX:** the key counts distinguish people from admissions, which matters because a patient can be admitted more than once.
   - Total Patient (everyone on record):
     `Total Patient = DISTINCTCOUNT(DimPatient[Patient_ID])`
   - Total Admission (each hospital stay):
     `Total Admission = DISTINCTCOUNT(FactHospitalAdmissions[Admission_ID])`
   - Total Admitted Patient (individual patients who were admitted at least once):
     `Total Admitted Patient = DISTINCTCOUNT(FactHospitalAdmissions[Patient_ID])`

   Together they show that 104,270 admissions came from 53,776 individual patients, out of 100,000 on record. [Total Documented Cost, Average Completed LOS, Complication Rate, Hospital Mortality Rate and the condition counts.]
4. **Designed two interactive pages:** a **Financial and OP Performance** page with year slicers (2023, 2024, 2025) and a **Population Health** page with hospital slicers, linked by navigation buttons.
5. **Added a Decomposition Tree** to let leaders drill from hospital to admission type, department and diagnosis category.


## Key findings

### Demand, cost and performance
- **Scale:** 104,270 admissions and $957.22M in documented treatment cost, about $9,200 per admission if every admission has a financial record (the true average will be higher if some do not).
- **Demand across the year:** admissions are fairly steady at around 8.4K to 8.7K a month, with a clear peak in December (9.38K, about 8% above the monthly average of 8.7K) and a high January (9.04K). The lowest months are April (8.38K) and November (8.40K). Complicated admissions follow the same pattern and are also highest in December.
- **Hospitals:** Lakehaven (29,320, about 28%) and Meadowbrook (25,750, about 25%) account for roughly 53% of admissions. Riverton has 18,305 and Westhaven 16,410, leaving about 14.5K for the fifth hospital. In Lakehaven, emergency admissions make up about 72% of its volume (21,096), ahead of elective (4,709), urgent (2,342) and transfer (1,173).
- **Cost by department:** the ICU accounts for $309M, about 32% of all documented cost, followed by Orthopaedics ($163M, 17%), Respiratory ($102M), General Medicine ($100M) and Cardiology ($88M). These five departments make up about 80% of cost.
- **Cost per patient treated:** the ICU treated the most patients (15,581) and generated $309M in documented cost, roughly $19.8K per patient treated. Orthopaedics generated about $11.5K per patient ($163M across 14,160 patients), compared with about $6.7K for Respiratory and $7.0K for General Medicine, which treat a similar number of patients as the ICU. Patients can appear in more than one department, so these are approximate figures.
- **Payers:** the two largest payer groups account for about 79% of documented cost ($434M and $324M), the third for $155M (16%), and the smallest for $43M (4.5%).
- **Quality indicators:** average completed length of stay of 5.75 days, 10,399 complicated admissions (a complication rate of 9.97%) and a hospital mortality rate of 1.00%.
- **Length of stay:** the ICU has the longest stays (7.67 days, about a third above average), followed by Oncology (6.91 days). Paediatrics has the shortest (4.64 days). Most other departments sit between 5.1 and 5.6 days.
- **Patient satisfaction:** the average score is 4.45 out of 5, very consistent across departments (4.43 to 4.49 in the main departments).

### Patient population
- **Patients:** 100,000 patients on record, of whom 53,776 (about 54%) were admitted. That is roughly 1.9 admissions per admitted patient.
- **Chronic conditions (across all 100,000 patients):** hypertension affects 30K (30%), obesity 16K (16%), cardiovascular disease 14K (14%) and cancer 6K (6%). About 28,400 patients (28%) have two or more chronic conditions.
- **Smoking status (admitted patients):** 26,633 never smoked, 10,645 are former smokers and 8,384 are current smokers, with 923 unknown. Among patients with a recorded status, about 41% are current or former smokers.

## Recommendations
1. **Review ICU capacity and flow.** The ICU has the longest stays and the highest cost share, so look at admission criteria, step-down capacity and earlier discharge planning to free beds and control cost.
2. **Look at Oncology and ICU length of stay together.** Check whether longer stays reflect clinical complexity or avoidable delays, and compare against similar hospitals.
3. **Plan for winter demand.** December and January bring the highest admissions and complications, so plan staffing, beds and supplies ahead of them, and confirm the pattern holds in each year.
4. **Focus on Lakehaven and Meadowbrook.** They carry more than half of admissions, and Lakehaven is heavily emergency-driven, so improve emergency-to-inpatient flow and bed management there first.
5. **Strengthen chronic disease management.** Three in ten patients have hypertension, and more than a quarter have several chronic conditions. Admitted patients average about 1.9 admissions each, so invest in hypertension, obesity and cardiovascular care pathways and in follow-up after discharge to reduce repeat admissions.
6. **Offer smoking cessation support** to the roughly 19,000 current and former smokers among admitted patients, starting during the hospital stay.
7. **Review payer mix and contracts.** Two payer groups drive about 79% of cost, so check reimbursement terms and utilisation with them first.


## Limitations
- The figures are counts and totals, so larger hospitals and departments naturally look bigger. Rates per admission would allow fairer comparisons.
- The monthly chart combines three years, so it shows seasonality, not a year-by-year trend.
- Diagnosis, department and chronic-condition effects overlap, so differences shouldn't be read as causes.
- Cost is documented cost only, so admissions without a financial record are not captured.
- Some departments treat few patients (for example, Obstetrics has about 100), so their averages are less reliable. A patient can appear in more than one department, so department patient counts add up to more than the 53,776 distinct admitted patients.

## What I learned
This project taught me to build a multi-page healthcare report that links operational, financial and clinical measures, and to be careful when interpreting counts, averages and combined years in a hospital setting.

## Repository contents
- README.md: this write-up
- data/: sample or synthetic data, or a link to its source
- dashboard/: screenshots of both report pages
- powerbi/: the Power BI (.pbix) file
