# 📊 FP&A Financial Performance Dashboard | Power BI Project

> **An effective financial dashboard is not just about numbers; it transforms raw data into variance drivers and executive decisions.**

This three-page Power BI project delivers an FP&A business performance view that goes beyond descriptive reporting to provide diagnostic and prescriptive analytics. It covers KPI tracking, YoY variance analysis, profitability drivers, a Pro Forma margin discount scenario, and a full Price-Volume-Mix (PVM) profit bridge — isolating the exact profitability drivers of margin expansion and compression from prior year (PY) to current year (CY).

---

##  Strategic Objective

This project was architected to answer the critical strategic questions that guide leadership action by evaluating two fiscal years of financial data across five market segments and five countries to:
*   **Uncover** financial growth patterns, structural margin shifts, strends, and loss-generating drivers.
*   **Assess** YoY performance by tracking and quantifying variance across six core business KPIs.
*   **Pinpoint** top-performing, highest-revenue products and highest-ROI scaling opportunities.
*   **Decompose** gross profit movement through the PVM analysis, quantifying the five distinct profitability impacts.

---

##  Dataset

- **Source:** Microsoft public financial sample dataset used for professional practice.
- **Scope:** Units Sold, COGS, Net Sales, Gross Profit, and Discount across market segments, products, and countries.
- **Coverage:** Two complete fiscal years (2023–2024) — enabling the full-period comparative analysis.
- **Data Note:** The original dataset lacked PY data (Jan–Aug). I used Claude AI to create 376 realistic data rows and appended them to enable a complete YoY comparison and PVM bridge analysis. N/A and blank rows were also inserted to simulate real-world data quality conditions and demonstrate practical ETL handling.

> *Disclaimer: "Vanzard Global Co." is a fictional placeholder name used to simulate real-world reporting structure.*

---

##  The Process

### 1 — Data Preparation — Excel & Power Query

*   Pre-ingestion review in Excel: fixed a leading space in the `Sales` column header to ensure accurate column mapping in Power Query.

*   Completed the PY dataset by appending 376 generated data rows (see Dataset section).

*   ETL in Power Query: removed N/A values, blanks, and duplicates; standardized data types (numeric, text, date), and applied consistent column naming conventions.

### 2 — Data Modeling — Star Schema
*   Built a Star Schema in Power BI with a fully structured fact–dimension relationship model. 
*   **Time Intelligence:** Created a dynamic complete **Date Table** using DAX to power period-over-period filtering and YoY calculations.

### 3 — DAX Measures
Wrote **explicit DAX measures and functions** for all calculations —  key measures include:

| Measures | Purpose |
|---|---|
| `CY [KPI]`, `PY [KPI]` | Core financial KPIs |
| `Net Sales`, `Gross Profit`, `Gross Profit Margin %`, `Units Sold`, `COGS`, `Discount Offered` | Time intelligence — CY vs. PY logic applied across all core KPIs for period comparison |
| `Waterfall Bridge Value`,`Price Impact`, `Volume Impact`, `Mix Impact`, `Discount Impact`, `Cost Impact` | PVM bridge analysis — 5 profit variance drivers and bar values powering the waterfall  |
| `Pro Forma Gross Profit Margin % — PY Discount Rate` | Counterfactual margin scenario — isolates PY discount rate impact on Gross Profit Margin % |
| `Top 3 Products by Sales` | Dynamic ranking logic — auto-updates top performers under active filter context |
| `KPI_PY [KPI]`, `Highlight [KPI] YoY%` | PY KPI reference values, YoY% conditional formatting and directional logic |

**Key DAX functions applied:** `CALCULATE`, `SAMEPERIODLASTYEAR`, `TOTALYTD`, `IF`/`SWITCH`, `VAR`/`RETURN`, `KEEPFILTERS`, `ISFILTERED`/`ISBLANK`, `VARX.P`, `FORMAT`, `TOPN`/`RANKX` — Core calculation engine for context filtering, period logic, conditional branching, and statistical variance.

### 4 — Report Design & Interactivity
Three-page layout with consistent navigation, cross-page filtering, and conditional formatting:

- **Interactive page navigation buttons** (2 per page) and bookmark-driven filter controls.
- **Year, Month, and Country slicers** applied globally across all pages.
- **Conditional formatting** on KPI cards, tables, and visuals with dynamic color thresholds.
- **Visual interactions**, custom tooltips, page-level drill-through, and field parameters for dynamic analysis.

---

##  Report Pages

### Page 1 — Executive Insights & Recommendations
Strategic FP&A summary page combining the PVM bridge with insights and recommendations.
- **PVM Gross Profit Bridge** — waterfall chart decomposing PY→CY profit movement: Volume, Price, Discount, Cost, and Mix Impact
- **5 Key Insights panels** — each pairing a quantified finding with a strategic recommendation

### Page 2 — Market Performance
Operational overview of revenue trends, geographic distribution, and segment-level profitability.
- **6 KPI Cards** — Units Sold, COGS, Discount, Net Sales, Gross Profit, Gross Profit Margin % — CY value, PY value, and YoY variance %
- **Net Sales Trend** — monthly line chart showing seasonality and growth trajectory
- **Gross Profit by Country** — interactive Bing map with bubble sizing overlay
- **Gross Profit by Segment** — waterfall chart showing segment contribution to total
- **Gross Profit %GT by Country and Product** — drill-down profit matrix with product-level breakdown

### Page 3 — Portfolio & Profitability Drivers
Deep-dive into margin quality, discount exposure, and product revenue ranking.
- **6 KPI Cards** — set consistently with page 2 for cross-page reference
- **Gross Profit Margin % — Actual vs. Pro Forma** — dual-series chart comparing actual margin against Pro Forma margin "what-if" scenario at PY discount rates, by country
- **Discount Band Breakdown** — donut chart segmented by Band (High | Medium | Low)
- **Top 3 Products by Sales** — dynamic top 3 ranking and highlighting bar chart
- **Gross Profit Margin % by Segment and Product** — matrix table showing product-level margins within each segment with conditional formatting

---

##  What the Data Reveals — 5 FP&A Questions Addressed

### 1) How effectively is our pricing strategy flowing through to the bottom line?

 Price Impact added +$55M — but Cost Impact consumed -$47M (85% absorption rate), limiting gross profit improvement to $8M ($5M → $13M CY).
> ***Recommendation:** Run a product-level cost-to-serve analysis targeting the lowest-margin products to protect pricing gains from cost absorption.*

### 2) Which segments are diluting our overall portfolio margin?

 Enterprise is the only loss-making segment at -2.70% gross margin — a 75.92pp gap below Channel Partners (73.22%). The business is currently subsidizing this segment.
> ***Recommendation:** Suspend Enterprise discount approvals and conduct a pricing floor analysis. Escalate to leadership if break-even is not confirmed within two quarters.*

### 3) Is our top-line revenue growth structurally sound and balanced?

 Net Sales grew from $37.2M to $92.3M, but Units Sold moved only +1.11% and Volume Impact was $0M on the bridge. Growth was driven entirely by pricing — a commercially unsustainable position.
> ***Recommendation:** Prioritize volume growth in Germany, which trails market leader France by 28.79% in units (147.2K vs. 189.6K) — the most actionable gap in the portfolio.*

### 4) What is the primary headwind compressing our Gross Profit Margin?

 COGS grew +148.99% vs. Net Sales +148.16%, compressing Gross Profit Margin 28 basis points (14.38% → 14.10%). Cost Impact at -$47M is the dominant profit headwind.
> ***Recommendation:** Prioritize COGS decomposition and procurement review over discount remediation to isolate cost drivers — cost containment is the higher-impact action.*

### 5) Where should we allocate capital and sales resources to maximize ROI?

 Channel Partners delivered 73.22% consistent Gross Profit Margin across all six products (72.51%–73.80%), versus the 14.10% company average — a structural advantage underweighted in the commercial mix.
> ***Recommendation:** Reorient commercial growth toward Channel Partners; analyze PWN-Q7 ($27.10M, top product) for penetration rate as the highest-ROI margin improvement lever.*

---

##  Tools & Technologies

| Tool | Role |
|---|---|
| **Excel** | Initial data inspection, column correction, pre-ingestion formatting, dataset completion |
| **Power Query (M)** | ETL — transformation, data quality handling, and calculated columns |
| **Power BI** | Data modeling, DAX measures, dashboard design, data visualization |
| **DAX** | Explicit measures, time intelligence, PVM profit bridge, Pro Forma simulation |

---

##  Power BI & FP&A Skills Demonstrated

- **Advanced DAX Measures** — variance logic, dynamic calculations and functions with logic-based formatting and grouping. 
- **Power Query (ETL)** — multi-step data transformation: null/blank handling, duplicates removal, type standardization, and calculated column creation.
- **Star Schema Modeling** — fact-dimension model with active Date Table.
- **PVM Profit Bridge Analysis** — custom-built 5-category Price–Volume–Mix profit decomposition with DAX variance calculations and dynamic waterfall visual.
- **Pro Forma Impact Analysis** —  counterfactual profit margin analysis for actual vs. PY discount rates scenario across all countries.
- **KPI Engineering** — 6 CY vs. PY KPI cards with YoY variance %, directional indicators, and conditional formatting.
- **Geospatial Analysis** — geographic profit distribution mapping by country-level bubble visualization.
- **Advanced Report Interactivity** — drill-throughs, cross-page navigation, bookmarks, slicers, and custom contextual tooltips enabling segment-to-product deep dives and analysis flow.
- **Executive Dashboard Design** — dark-themed three-page layout with deliberate visual hierarchy, narrative sequencing,and insight-to-recommendation structure.

---

##  Repository Structure

```
 Vanzard_Financial_Analysis_PowerBI
 ┣ Vanzard_Financial_Analysis_Dashboard.pbix
 ┣ Screenshots
 ┃  ┣ Project_Dashboards.pdf
 ┃  ┣ Page1_Executive_Insights.jpg
 ┃  ┣ Page2_Market_Performance.jpg
 ┃  ┣ Page3_Portfolio_Drivers.jpg
 ┃  ┗ Data_Model.jpg
 ┣ README.md
 ┗ Data
    ┗ Financials.xlsx
```

---

##  How to Use

1. Download the `.pbix` file and open with [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free).
2. Use **Year**, **Month**, and **Country** slicers to filter across all pages dynamically.
3. Navigate between pages using the navigation buttons on each page.
4. Hover over PVM Bridge bars for margin and sales context and the Geo Map for filtered values via custom tooltips.
5. Use right-click **drill-through** on visuals to explore cross-report detail focus.

---
##  Why This Project Matters

Beyond standard dashboard design, this project showcases the ability to:

- Transform raw financial data into executive narratives — from variance drivers to actionable insights and recommendations.
- Isolate true profit drivers instead of reporting headline growth only.
- Connect commercial performance to margin quality.
- Frame analysis methodologically to support management action.

This is the difference between a generic dashboard and an **FP&A decision-support reporting tool**.

---

*Created by **Skander Haffar** | FP&A · Power BI · DAX · Power Query*

