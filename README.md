# 🌍 Analyzing Industry Carbon Emissions with SQL

In this project, we analyze a dataset of **product carbon emissions** to identify the **highest-emitting industries** based on the **most recent available year**. These industries contribute to over **75% of global emissions**, making this a critical step toward understanding and addressing climate change.

This is an **introductory single-task SQL project**, with a focus on:
- Grouping and summarizing data
- Filtering aggregated results
- Basic SQL reporting skills

---

## 🎯 Project Objective

- 🔍 Identify the **top carbon-emitting industries** in the most recent year
- 📊 Summarize total emissions across all industries
- ⚖️ Highlight key contributors to climate impact

---

## 🗃️ Dataset Overview

The dataset includes the following columns:

### `emissions_data`
| Column           | Description                                      |
|------------------|--------------------------------------------------|
| `industry`       | Name of the industry                             |
| `product`        | Specific product or category                     |
| `emission_year`  | Year of emission measurement                     |
| `co2e_tonnes`    | Carbon emissions in tonnes of CO₂ equivalent     |

---

## 🧾 SQL Highlights

### 🔥 Querying the Top Emitting Industries (Most Recent Year)

```sql
WITH recent_year AS (
  SELECT MAX(emission_year) AS latest_year
  FROM emissions_data
)

SELECT industry,
       SUM(co2e_tonnes) AS total_emissions
FROM emissions_data
JOIN recent_year
  ON emissions_data.emission_year = recent_year.latest_year
GROUP BY industry
ORDER BY total_emissions DESC;
