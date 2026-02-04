# AZ Real-Time E-Commerce Insights

A small end-to-end, real-time analytics project that simulates e-commerce events and turns them into streaming insights using Azure + Databricks + Power BI.

**Goal:** Generate live e-commerce activity (orders/clicks/payments), process it as a stream, build curated analytics tables, and visualize KPIs in Power BI.

---

## What this repo contains

- **`simulator/`**  
  Event generator that produces synthetic e-commerce events (ex: orders, customers, products, payments).  
  Use it to create a continuous stream of data for your pipeline.

- **`databricks-notebooks/`**  
  Databricks notebooks for streaming ingestion + transformations (Bronze → Silver → Gold style).  
  Typically includes:
  - Stream ingestion (Event Hubs / Kafka / files)
  - Parsing + schema enforcement
  - Deduplication / watermarking
  - Aggregations for KPI tables (revenue, orders, AOV, top products, etc.)

- **`powerbi/`**  
  Power BI assets (PBIX / dataset notes / screenshots) for dashboards built on the curated output tables.

---

## Architecture (high-level)

1. **Simulator** emits e-commerce events continuously  
2. Events land in **Azure streaming layer** (commonly Event Hubs / Kafka)  
3. **Databricks Structured Streaming** ingests the events into a Bronze table (raw)
4. Databricks transforms to Silver (cleaned/validated) + Gold (analytics-ready aggregates)
5. **Power BI** connects to curated tables for real-time-ish dashboards



---

## KPIs you can track

Typical “real-time commerce” KPIs this pipeline supports:

- Revenue (total / by time window)
- Order count
- Average Order Value (AOV)
- Unique customers
- Top products / categories
- Conversion funnel (if click/view events exist)
- Payment success vs failure rate (if payment events exist)
- Late/delayed events (streaming quality indicator)

---

## Quickstart

### Prereqs
- Azure subscription (if running the full cloud version)
- Databricks workspace
- Power BI Desktop
- Python (for simulator) or whatever runtime your simulator uses

### 1) Run the simulator
From `simulator/`, start the event generator.

Example (adjust to your actual script/entrypoint):
```bash
cd simulator
# python main.py --rate 50 --mode stream
