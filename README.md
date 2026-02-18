# 📊 Student Engagement & Academic Performance Analytics Dashboard

## 🔎 Project Overview

This Power BI project analyzes student academic performance and program
engagement using a tenure-adjusted scoring model. The dashboard supports
advising decisions, retention monitoring, and program-level performance
evaluation.

The goal of this project was to transform operational student data into
a structured semantic model that enables dynamic, context-aware
analytics while maintaining strong data governance standards.

------------------------------------------------------------------------
## ✅ Progress Update (Feb 2026)

**Engagement Score Improvements**
- Added **Expected Engagement Months** (excludes summer months) to adjust engagement expectations.
- Updated engagement components to use **pace-based scoring**:
  - Coaching Minutes per Expected Month
  - Group Activities Attended per Expected Month
  - Goals vs Expected Goals (1 goal per 6 expected months)
- Engagement score now reflects fair expectations across students with different program tenures.

------------------------------------------------------------------------
## 🎯 Business Problem

Academic advisors and program leadership require tools to:

-   Identify students at academic risk early
-   Evaluate engagement relative to time in program
-   Track GPA trajectory across semesters
-   Monitor progress toward degree completion
-   Assess overall program effectiveness

Raw data (GPA, coaching minutes, attendance, goals) does not inherently
account for tenure. This project introduces a normalized engagement
model that adjusts expectations based on time enrolled.

------------------------------------------------------------------------

## 🧱 Data Model Architecture

The model follows a **star schema design** to eliminate ambiguous filter
paths and ensure stable DAX evaluation.

### Dimension Table

-   **DimStudent** (Primary Key: Contact ID)

### Fact Tables

-   Semester Metrics (GPA, Earned Credits, Attempted Credits, Term Rank)
-   Cumulative Metrics
-   Group Activities (Attendance %)
-   Student Goals
-   Coaching Records

All relationships use **Contact ID** as the single filter path (1:\*
cardinality, single-direction).\
Full Name was intentionally not used as a relationship key to preserve
referential integrity.

------------------------------------------------------------------------

## 📐 Technical Design Decisions

-   Implemented a star schema to prevent ambiguous relationships.
-   Removed bi-directional filters to ensure predictable measure
    evaluation.
-   Used measures (not calculated columns) for dynamic scoring logic.
-   Applied tenure smoothing to prevent volatility for newly enrolled
    students.
-   Excluded personally identifiable and geographic information for
    public release.

------------------------------------------------------------------------

## 🧮 Key DAX Highlights

### Tenure (Months)

Calculated from Date Entered Program to Today:

``` dax
Tenure (Months) =
DATEDIFF ( [Date Entered Program], TODAY(), MONTH )
```

### GPA Change vs Prior Term

Utilizes term ranking logic to calculate academic trajectory between
semesters.

### Tenure-Adjusted Engagement Score

Engagement is calculated using normalized pace metrics:

-   Coaching Minutes per Month
-   Goals per Month
-   Group Activity Attendance %

Weighted model:

``` dax
Engagement Score =
0.40 * [Coaching Pace Score]
+ 0.35 * [Group Activity Score]
+ 0.25 * [Goals Pace Score]
```

This approach ensures longer-tenured students are evaluated relative to
time in program rather than raw totals.

------------------------------------------------------------------------

## 📊 Engagement Classification

  Score Range   Tier
  ------------- ----------
  80+           High
  55--79        Moderate
  \<55          Low

These tiers support advisor prioritization and intervention planning.

------------------------------------------------------------------------

## 🔐 Privacy & Data Governance

To maintain compliance with data security standards:

-   Personally identifiable information was removed.
-   Geographic data was excluded from the public version.
-   Contact IDs are anonymized.
-   Public dataset uses de-identified or synthetic records.

------------------------------------------------------------------------

## 📈 Key Insights Enabled

-   Engagement pace is a stronger predictor of GPA stability than raw
    participation totals.
-   GPA decline frequently correlates with reduced coaching pace.
-   Tenure-adjusted scoring highlights disengagement earlier than
    traditional attendance metrics.
-   Program-wide engagement averages provide leadership-level
    performance benchmarks.

------------------------------------------------------------------------

## 🚀 Future Enhancements

-   Cohort-based engagement benchmarking
-   Predictive retention modeling
-   Rolling GPA trend indicators
-   Advisor workload optimization metrics
-   Engagement trend visualization over time

------------------------------------------------------------------------

## 🛠 Tools & Technologies

-   Power BI
-   DAX
-   Power Query (M)
-   Star Schema Modeling
-   Data Governance Best Practices

------------------------------------------------------------------------

## 👤 Author

Andrew Eason\
Business Intelligence & Data Analytics Professional\
LinkedIn: https://www.linkedin.com/in/andrew-eason-242a7459
