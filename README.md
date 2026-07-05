# 📊 Education Management System (EMS) Analytics — Power BI Project

An end-to-end analytics project built on a state-scale school education dataset (**9,032 schools, 19,903 teachers, 1,52,371+ students** across multiple districts and blocks). The raw data was cleaned in **Excel**, explored and aggregated using **SQL**, and visualized through **three interconnected Power BI dashboards** covering infrastructure/HR analytics, learning assessment performance, and daily attendance monitoring.

---

## 🧭 Project Workflow

```
Raw Data (District → Block → School → Student level)
        │
        ▼
 Excel  →  Data cleaning: null handling, duplicate removal,
           column standardization, category mapping
        │
        ▼
 SQL    →  EDA: aggregations by District/Block/School,
           PTR calculation, performance %, ranking (RANK/ROW_NUMBER),
           retirement-age cohort extraction, infrastructure scoring
        │
        ▼
 Power BI → Data modeling (star schema), DAX measures,
            drill-down tables, slicers, 3 dashboards
```

The dataset is hierarchical (**District → Block → School → Student**) and lakh-scale, so the SQL layer was used to pre-aggregate before loading into Power BI, keeping the report responsive despite the volume.

---

## 📁 Dashboards

### 1️⃣ Education Management Analytics Dashboard
*Infrastructure, HR and district-level school distribution overview*

<img width="881" height="498" alt="image" src="https://github.com/user-attachments/assets/5e5dde72-86c5-408a-acaf-97c4ec0ee780" />


**Filters:** District, Block, School, School Management, School Category, Session Type

| Metric | Value |
|---|---|
| Total Schools | 9,032 |
| Total Teachers | 19,903 |
| Total Students | 1,52,371 |
| Avg. Teacher Experience | 16.51 years |
| Pupil–Teacher Ratio (PTR) | 8 : 1 |
| School-to-Student Ratio | 17 : 1 |

**Visuals & findings:**
- **District-wise School Count** (dual-line, split by `PTR > 30` vs `PTR ≤ 30`) — exposes a sharp imbalance: some districts (e.g. District-3, District-6) run lean with single-digit PTR-heavy counts, while others (District-2, District-5) cross 2,000+ schools, meaning staffing/infrastructure investment can't be uniform across districts and needs to follow this curve, not a flat state-wide average.
- **Top 10 Schools by Infrastructure Score** — a ranked table (School-2859 leads at 100, followed by School-2451 at 87 and School-2342 at 84) used as a benchmark cohort for replicable best practices.
- **Teacher Retirement Forecast (next 5 years)** — **16,767 teachers** and **3,162 principals** are due to retire, i.e. **~84% of current teaching staff and a large share of leadership will exit within 5 years**. This is the single most important workforce-planning number in the whole report — it signals an urgent recruitment/succession pipeline requirement, not a future one.

---

### 2️⃣ School Assessment Performance Dashboard
*Learning-outcome (LO) level analysis of student assessments*

<img width="885" height="491" alt="image" src="https://github.com/user-attachments/assets/95233f09-0c95-4b12-842a-0f81c51c94b0" />

**Filters:** District, Block, School, School Management, Grade, Subject

| Metric | Value |
|---|---|
| Average Score (overall) | 0.26 (≈26%) |
| Schools Participated | 9,016 |
| Students Participated | 1,52,328 |

**Visuals & findings:**
- **District/Block/School drill-down table** — Student Participation, Questions Attempted, Correct Score, Performance %. District-level performance is flat and low across the board: **District-1: 26.49%, District-2: 25.36%, District-3: 25.53%**, with block and school-level figures hovering in the same 25–27% band (e.g. Block-48: 25.76%, School-1356: 31.39% as a rare outlier). The narrow spread (mostly 25–28%) suggests a **systemic learning gap rather than isolated pockets of underperformance** — this points to curriculum/pedagogy issues over infrastructure ones.
- **Level-wise Student Distribution** — Advanced: 68K, Intermediate: 62K, Basic: 21K, Beginner: 1K. Despite the low average score %, most students are bucketed "Advanced/Intermediate" — implying the **scoring rubric/banding thresholds and the raw performance % tell two different stories**, worth reconciling before reporting outcomes externally.
- **Top 10 vs Bottom 10 Learning Objectives (LO)** — a bidirectional bar chart isolating which specific learning objectives (e.g. color recognition, comprehension-based LOs) score highest/lowest, letting curriculum teams target interventions at the LO level instead of the subject level.

---

### 3️⃣ School Attendance Monitoring Dashboard
*Daily attendance capture health + infrastructure pillar breakdown*

<img width="861" height="482" alt="image" src="https://github.com/user-attachments/assets/ece7e623-9070-4a98-8c77-3fe7a967d602" />

**Filters:** District, Block, School, School Management, School Category, Session Type

| Metric | Value |
|---|---|
| % Schools that Marked Teacher Attendance | 99.69% |
| % Schools that Marked Student Attendance | 100.00% |
| Avg. Teacher Present Attendance | 49.59% |
| Avg. Student Present Attendance | 51.17% |

**Visuals & findings:**
- **Attendance-marking compliance is near-universal** (99.69–100%), but **actual physical presence sits close to a coin flip** (~50% for both teachers and students) — the gap between "marked" and "present" is the headline risk here: attendance is being *recorded* almost everywhere, but only about half of that recorded population is actually *present*, which undermines any downstream metric (like the assessment scores in Dashboard 2) that assumes full classroom exposure.
- **Infrastructure Assessment by Pillar** (donut): Building 33.29%, Sanitation 31.96%, Academic 25.06%, ICT 9.4%, **Labs 0.3%**. ICT and Labs are the weakest pillars by a wide margin — a direct, quantifiable input into any infrastructure-funding prioritization discussion.
- **District/Block/School Infrastructure & Performance Overview** — a combined table (Avg Infrastructure Score, Attendance %, Average Score) makes it possible to directly correlate infrastructure quality with learning outcomes at the school level, e.g. School-4240 (infra 45.00) vs School-4286 (infra 53.00) — infrastructure score alone doesn't cleanly predict the average score column, suggesting other factors (teacher presence, pedagogy) dominate over physical infrastructure.

---

## 🔗 Cross-Dashboard Insight

Reading all three dashboards together surfaces a insight that no single dashboard shows alone:
> Schools are recording near-perfect attendance compliance (Dashboard 3) and a workforce that looks experienced on paper (16.51 yrs avg, Dashboard 1) — yet actual student learning performance sits around 25–26% (Dashboard 2), and real physical presence is only ~50%. **The bottleneck isn't data capture or teacher tenure — it's actual classroom presence and instructional effectiveness**, and a large share of that experienced workforce is about to retire in the next 5 years with no visible succession data. This reframes the problem from "we need better dashboards" to "we need a presence + succession + pedagogy intervention," which is exactly what this report is built to surface for decision-makers.

---

## 🛠️ Tech Stack

| Layer | Tool | Purpose |
|---|---|---|
| Data Cleaning | Microsoft Excel | Null/duplicate handling, standardizing District/Block/School hierarchy, category mapping |
| EDA & Aggregation | SQL | Grouping by District/Block/School, PTR & Performance % calculation, ranking (Top/Bottom 10), retirement-cohort filtering |
| Visualization | Power BI | Data modeling, DAX measures, slicers, drill-down matrices, KPI cards, donut/bar/line visuals |

## 📐 Key DAX / SQL Concepts Used
- Pupil-Teacher Ratio & School-to-Student Ratio measures
- Performance % = Correct Score / Questions Attempted
- Rank-based Top 10 / Bottom 10 (Infrastructure Score, LO Performance %)
- Age-based cohort filter for 5-year retirement projection
- Weighted infrastructure pillar scoring (Academic / ICT / Labs / Building / Sanitation)
- Hierarchical drill-through: District → Block → School


## 🚀 How to Use
1. Open the `.pbix` file in Power BI Desktop (requires Power BI Desktop, latest version).
2. Use the slicers (District, Block, School, School Management, Category, Session Type/Grade/Subject) to drill into any specific region.
3. Click any District/Block row in the matrix tables to auto-filter all visuals on that page.

## 📌 Notes on Scale
Source data runs into the lakhs (150K+ student records, 9K+ schools). Pre-aggregation was done at the SQL layer (rather than relying on Power BI's in-memory engine alone) to keep report load times and slicer interactions fast.

---
*Built as a personal data analytics portfolio project — Excel (cleaning) → SQL (EDA) → Power BI (visualization).*
