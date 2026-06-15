# Data Collection & Methodology

## Project Overview

This document outlines the data collection process, analytical decisions, quality controls, and limitations for the **India Data Roles — Job Market Intelligence Dashboard 2026** project.

All data was manually collected and validated by the author. No automated scraping tools, bots, or third-party data providers were used.

---

## Data Collection

### Platforms Covered
| Platform | Type | Focus |
|---|---|---|
| LinkedIn | Professional network | Full-time roles, skill-heavy JDs |
| Naukri.com | Indian job portal | High volume, fresher-friendly filters |
| Foundit (formerly Monster India) | Indian job portal | Mid-size company postings |
| Internshala | Internship platform | Internship postings with stipend data |
| Unstop | Student community platform | Internship and entry-level postings |

### Collection Period
May 2026 – June 2026

### Roles Targeted
- Data Analyst
- Business Analyst
- Data Engineer
- BI Developer
- MIS Analyst

### Cities Covered
- Bengaluru
- Delhi NCR *(consolidates Delhi, Noida, Gurgaon, Gurugram — see Regional Consolidation below)*
- Hyderabad
- Pune
- Mumbai
- Chennai

### Dataset Composition
| Category | Count |
|---|---|
| Full-time postings | 205 |
| Internship postings | 25 |
| **Total** | **230** |

---

## Inclusion Criteria

A posting was included in the dataset only if it met **all** of the following conditions:

- Posted within the **last 30 days** of the collection date
- Targeted candidates with **0–3 years of experience**
- Job title and description were **clearly data-related**
- Job description contained **at least some extractable skill information**

---

## Exclusion Criteria

A posting was excluded if **any** of the following applied:

- Clear mismatch between job title and job description content
- Duplicate posting across platforms *(same company + role + city combination)*
- Job description contained no skill or tool requirements whatsoever
- Role was clearly senior-level despite being filtered under fresher criteria
- Posting was older than 30 days at time of collection

---

## Data Quality Decisions

### Salary Handling
- Salary fields were left **blank** where not disclosed — values were never estimated or imputed
- Internship stipends (monthly, in ₹) were kept in a **separate column** from full-time salaries (annual LPA) to prevent unit mixing
- Salary analysis is based on **15 full-time postings with disclosed compensation** — representing 7.3% of the full-time dataset
- All salary figures should be treated as **directional and not statistically conclusive** at this sample size

### Outlier Handling
- One full-time posting disclosed a maximum salary of **29 LPA** — significantly above all other disclosed figures
- This posting was **retained in the raw dataset** but **excluded from mean calculations**
- **Median salary** was used as the primary central tendency measure due to this outlier
- The outlier is documented transparently in the Salary Insights sheet with a note

### Skill Extraction
- Skills were extracted from raw job description text using **keyword search (COUNTIF with wildcards)** in Excel
- Skill detection was **case-insensitive** — "SQL", "sql", and "Sql" are all counted identically
- The search term "visuali" was used for Data Visualization to capture both "visualization" (American) and "visualisation" (British) spellings
- Skills in the **Required Skills** column and **Preferred/Good-to-Have Skills** column were tracked separately

### Work Mode Standardization
Raw text from postings was standardized to three categories:

| Original Text | Standardized To |
|---|---|
| Work from home, WFH | Remote |
| In-office, Onsite, On site | On-site |
| Hybrid/Remote, Flexible | Hybrid |
| Not mentioned | Not Disclosed |

### Regional Consolidation
Delhi NCR postings were collected under multiple city labels:

- Delhi
- New Delhi
- Noida
- Gurgaon / Gurugram

These were **consolidated into "Delhi NCR"** in all analysis sheets — treated as one hiring region reflecting the ground reality of the NCR job market where candidates routinely apply across these sub-locations.

**Raw city names were preserved in RAW_DATA** — consolidation was applied only at the analysis layer using multi-condition COUNTIFS formulas.

### Employment Type Separation
- A dedicated **Employment_Type column** (Full-time / Internship) was added to RAW_DATA
- All primary analysis (skill matrix, salary, city trends) filters for **Full-time only** unless explicitly stated
- Internship data is summarized separately in a dedicated snapshot table

---

## Analytical Techniques Used

| Technique | Application |
|---|---|
| COUNTIF with wildcards | Skill frequency detection from raw text |
| COUNTIFS | Multi-condition filtering by city, role, platform |
| AVERAGEIFS | Conditional salary averages excluding blanks |
| SUMPRODUCT | Skill co-occurrence pair analysis |
| Array formulas (Ctrl+Shift+Enter) | Median salary with conditional filtering |
| Conditional formatting color scales | City × Role heatmap visualization |
| Outlier exclusion via threshold filter | AVERAGEIF with upper bound condition |

---

## Limitations

| Limitation | Impact | Mitigation |
|---|---|---|
| 7.3% salary disclosure rate | Compensation analysis is directional only | Clearly documented; median used over mean |
| Manual collection introduces selection bias | Postings seen first may be over-represented | Collected across multiple sessions and platforms |
| 230 rows is sufficient for directional insights but not statistically conclusive for all sub-segments | Role × city cross-tabs have small n | Sample sizes noted in analysis; no over-claiming |
| Point-in-time snapshot (May–Jun 2026) | Market conditions shift over time | Collection period clearly stated throughout |
| Keyword-based skill detection | May miss synonyms or abbreviations | Conservative keywords chosen; "visuali" captures both spellings |
| Internshala showed 100% salary disclosure | Based on only 3 postings — not representative | Flagged in Salary Insights sheet with sample size note |

---

## Ethical Notes

- No personal data, candidate information, or recruiter contact details were collected
- No proprietary or confidential company information was recorded
- All data was collected from **publicly visible job postings**
- This project is prepared for **academic and career development purposes only**
- Company names recorded solely for categorization (startup / mid-size / large) — no company is individually profiled or evaluated

---

## Reproducibility

Anyone wishing to replicate this analysis can:

1. Search the same 5 platforms using identical role and city filters
2. Apply the same inclusion/exclusion criteria documented above
3. Use the COUNTIF formula patterns documented in the SKILL_MATRIX sheet
4. Results will differ due to the time-sensitive nature of job postings — this dataset represents a specific market snapshot from May–June 2026

---

*Prepared by: Gurpreet | B.Tech CSE 2025 | June 2026*
