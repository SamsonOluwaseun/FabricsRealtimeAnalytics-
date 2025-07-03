# 🚴 Real-time Bike Data Analytics in Microsoft Fabric

This repository showcases an end-to-end **real-time analytics solution** built on **Microsoft Fabric**, demonstrating the ingestion, transformation, storage, and visualization of **streaming bicycle rental data**, along with **proactive alerting** capabilities.

The project follows a **medallion architecture** (Bronze, Silver, Gold) for structured data processing.

---

## 🚀 Project Overview

The goal of this project is to establish a robust pipeline for **real-time analysis** of bicycle rental data — enabling **immediate insights** and **automated actions** based on predefined conditions.

Built entirely with **Microsoft Fabric Real-Time Analytics**, the pipeline spans from data ingestion to dashboard alerts.

---

## 🏗️ Architecture Flow

1. **📥 Get Data**  
   Ingest streaming bicycle rental data (simulated sample source).

2. **💾 Store Data**  
   Persist raw and transformed data in **Eventhouse** and **KQL databases**.

3. **📈 Visualize Data**  
   Create dashboards showing live metrics and location-based analytics.

4. **🔔 Track Data**  
   Trigger **alerts** and **automated responses** using thresholds and rules.

---

## 🛠️ Key Tools & Components Used

### 🧠 Real-Time Hub
- Entry point for **data streams and events** within Fabric.

### 🌊 Eventstream
- **Ingests data** from sample or external source.
- **Transforms in-stream**:
  - Adds system timestamps: `SYSTEM.Timestamp()`
  - Parses fields like `BikepointID`
  - Filters events (e.g., `Neighbourhood contains 'Chelsea'`)
- **Routes output** to Eventhouse or downstream consumers.

### 🏠 Eventhouse
- High-performance **real-time analytics database**.
- Tables:
  - `BikesRawData` (Bronze)
  - `BikesTransformedData` (Silver)

### 🔍 KQL Database & Queryset
- Queries using **Kusto Query Language (KQL)**:
  - `extend`, `summarize`, `arg_max`, etc.
- Used for:
  - Transformation functions (`TransformBikeData()`)
  - Update policies
  - Schema and folder organization via `.alter table`

### 🥉🥈🥇 Medallion Architecture
- **Bronze Layer**: Raw schema (`BikesRawData`)
- **Silver Layer**: Transformed output with logic applied
- **Gold Layer**: Aggregated `MaterializedView` (`AggregateData`) with:
  ```kql
  arg_max(Timestamp, No_Bikes) by BikepointID
  
## 📊 Real-Time Dashboard

- Visuals: column/bar charts, maps, metrics  
- Auto-refresh enabled  
- Alerts configured for conditions like `No_Bikes < 5`

---

## 🚨 Activator

Alert-action rules based on data thresholds.

Triggers:

- ✅ Email notifications  
- ✅ Microsoft Teams alerts  
- ✅ Other Fabric items or workflows

---

## 🧠 Key Learnings and Takeaways

- ✅ **End-to-End Real-time Pipeline**: Built ingestion-to-alert architecture in a unified platform  
- 🏅 **Medallion Design**: Structured processing through Bronze/Silver/Gold layers  
- 💻 **KQL Proficiency**: Built reusable queries and transformations via KQL functions  
- 💧 **Eventstream Power**: Performed inline filtering, routing, and transformation at ingestion level  
- ✨ **Materialized Views**: Used pre-aggregated live data to power high-performance dashboards  
- 📣 **Proactive Monitoring**: Alerting system based on tile thresholds or KQL logic  
- 🔁 **Full Fabric Integration**: Seamless flow between ingestion, storage, querying, alerts, and reporting

---

## 📦 Project Structure

| Folder        | Description                                      |
|---------------|--------------------------------------------------|
| `/dashboards` | Fabric dashboard          |
| `/queries`    | KQL transformation and aggregation scripts       |
| `/eventstream`| Eventstream setup and filter logic               |
| `/activator`  | Alert/trigger rules                              |
| `/docs`       | Architecture diagram, setup steps, notes         |

---

## 💡 Conclusion

This project offers a practical example of building **scalable**, **responsive**, and **actionable** data pipelines using the **Microsoft Fabric Real-Time stack**. From ingestion to proactive insights, it covers the essential components of a modern real-time analytics system.
