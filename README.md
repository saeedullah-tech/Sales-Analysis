# Sales Analysis Dashboard | Power BI

![Images](https://github.com/saeedullah-tech/Sales-Analysis/blob/f0307394811b4a602e8057599ee3930cb65e4d5a/Sales%20Dashboard.png))


## 📊 Project Overview

A regional sales performance dashboard built in Power BI to practice **time intelligence, geographic analysis, and comparative KPIs**. This project demonstrates skills in DAX measure creation, star schema modeling, and business-oriented dashboard design.

**Purpose:** Enable sales managers to compare regional performance, identify seasonal trends, and track year-over-year growth across states.

---

## 🎯 Business Questions Answered

This dashboard helps answer:

1. **Which regions are growing vs. declining year-over-year?**
2. **What are the sales trends by month for each region?**
3. **Which states contribute most to regional revenue?**
4. **How does current year performance compare to previous year?**

### Key Decisions Supported
- **Resource Reallocation:** Identify underperforming regions that need support or intervention
- **Trend Analysis:** Spot seasonal patterns to optimize inventory and marketing timing
- **Performance Benchmarking:** Compare state-level sales to understand geographic strengths

---

## 🧮 Key DAX Measures

### Year-over-Year Analysis
```DAX
CY Sales = SUM(Sales[Sales Amount])

PY Sales = 
CALCULATE(
    [CY Sales],
    SAMEPERIODLASTYEAR('Date'[Date])
)

YoY Growth % = 
DIVIDE(
    [CY Sales] - [PY Sales],
    [PY Sales],
    0
)
```

**Why this approach:**
- `SAMEPERIODLASTYEAR()` ensures accurate time comparisons even with incomplete years
- `DIVIDE()` handles division-by-zero errors gracefully (returns 0 instead of error)
- Calculated at measure level (not column) to maintain flexibility with filters

### Profit Metrics
```DAX
CY Profit = SUM(Sales[Profit])

PY Profit = 
CALCULATE(
    [CY Profit],
    SAMEPERIODLASTYEAR('Date'[Date])
)

Profit Margin % = DIVIDE([CY Profit], [CY Sales], 0)
```

---

## 📐 Data Model Structure

### Star Schema Design

**Fact Table:**
- `Sales` (Orders, Sales Amount, Profit, Quantity, Discount)

**Dimension Tables:**
- `Date` (Calendar table with Year, Quarter, Month hierarchy)
- `Geography` (State, Region, Country)
- `Product` (Category, Sub-Category, Product Name)
- `Customer` (Customer ID, Segment)

**Relationships:**
- One-to-Many from Dimension → Fact tables
- Date table marked as Date Table for time intelligence functions

```
          ┌──────────┐
          │   Date   │
          └────┬─────┘
               │
        ┌──────▼───────┐
        │              │
   ┌────▼────┐    ┌────▼────┐
   │Geography│    │ Product │
   └────┬────┘    └────┬────┘
        │              │
        └──────┬───────┘
               │
          ┌────▼─────┐
          │  Sales   │
          │ (Fact)   │
          └──────────┘
```

---

## 📈 Dashboard Features

### Regional Performance Cards
- **Central Region:** $470.65K (Primary revenue driver)
- **East Region:** $470.65K 
- **South Region:** $71.36K (Potential concern - lowest performer)
- **West Region:** $139.97K

### Visualizations

1. **Geographic Map:** State-level sales distribution for quick pattern recognition
2. **Horizontal Bar Chart:** Sales by state ranked for easy comparison
3. **Line Charts:** Monthly trends with PY comparison (sparklines show seasonality)
4. **Performance Table:** Detailed metrics with YoY variance and profit margins

### Interactivity
- **Region filter:** Drill down into specific regions
- **Cross-filtering:** Click states on map to filter all visuals
- **Synchronized slicers:** Consistent filtering across pages (if multi-page)

---

## 💡 Key Insights & Analysis

### What This Dashboard Reveals:

✅ **Central and East regions dominate revenue** (~66% of total sales)  
⚠️ **South region significantly underperforms** (only $71K vs $470K in top regions)  
📊 **Seasonal patterns visible** in monthly trend lines (Q4 spike likely holiday sales)  
📈 **YoY growth varies by region** (East +21%, South -31% - critical variance)

### Interview Talking Points:

If discussing this project in an interview:

> *"I built this dashboard to practice time intelligence in DAX. The most challenging part was ensuring the year-over-year calculations worked correctly with incomplete data periods. I used `SAMEPERIODLASTYEAR()` instead of manual date arithmetic to handle edge cases automatically."*

> *"From a business perspective, this dashboard would immediately flag the South region's -31% decline. A sales manager would need to investigate: Are there staffing issues? Market changes? Competitor activity? The dashboard doesn't answer why, but it clearly shows where to focus attention."*

---

## 🛠️ Technical Skills Demonstrated

| Skill | Application in Project |
|-------|----------------------|
| **DAX Measures** | Time intelligence functions, CALCULATE, DIVIDE |
| **Data Modeling** | Star schema, relationship management, calendar table |
| **Visualizations** | Maps, bar charts, KPI cards, comparison tables |
| **Design Principles** | Regional color coding, consistent formatting, clear hierarchy |
| **Business Context** | KPIs tied to managerial decisions, variance analysis |

---

## 🚀 How to Use This Project

### Prerequisites
- Power BI Desktop (latest version)
- No external data connections required (embedded dataset)

### Steps
1. Clone this repository
   ```bash
   git clone https://github.com/yourusername/powerbi-sales-analysis.git
   ```

2. Open `Sales_Analysis.pbix` in Power BI Desktop

3. Explore the dashboard:
   - Use the region cards to filter views
   - Click states on the map to drill down
   - Hover over trend lines to see monthly details

4. View the data model:
   - Go to **Model View** to see table relationships
   - Check **Data View** to inspect source tables
   - Review DAX measures in the **Fields** pane

---

## 📚 Dataset Information

**Source:** Practice dataset (Superstore/similar retail sales data)  
**Records:** ~10,000 orders  
**Time Period:** 2022-2024  
**Geography:** United States

**Note:** This is a learning project using sample data. The insights are for demonstration purposes and not based on real business operations.

---

## 🎓 What I Learned

### Challenges Overcome:
1. **Date Table Creation:** Built a proper calendar table with all necessary date hierarchies
2. **Filter Context:** Understanding how CALCULATE modifies filter context for time intelligence
3. **Performance:** Optimized measures to avoid row-by-row calculations (used aggregations)
4. **Visual Design:** Balanced information density with readability

### Areas for Improvement:
- Add target/benchmark lines to show expected vs actual performance
- Include profitability analysis (margin % by product category)
- Create drill-through pages for deep-dive state analysis
- Add dynamic titles that change based on filter selections
- Implement conditional formatting to highlight variance thresholds

---

## 📁 Repository Structure

```
powerbi-sales-analysis/
│
├── Sales_Analysis.pbix          # Power BI report file
├── dashboard-screenshot.png     # Dashboard preview image
├── README.md                    # This file
└── data/
    └── sample-sales-data.csv    # (Optional) Source data if not embedded
```

