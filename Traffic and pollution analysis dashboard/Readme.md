
# 🚦 Traffic and Pollution Analysis Dashboard
 
A Power BI dashboard providing comprehensive insights into traffic incidents, congestion patterns, vehicle distribution, and environmental conditions across key locations in Nagpur, India.
 
---
 
## 📸 Dashboard Preview
 
### Main Dashboard

 
---
 
## 📊 Overview
 
This dashboard enables traffic analysts, urban planners, and city administrators to monitor and analyze traffic incidents, congestion levels, vehicle movement, and pollution-related metrics in real time. It covers multiple high-traffic locations across Nagpur and supports month-wise, location-wise, and vehicle-wise drill-downs.
 
---
 
## 🔢 Key Metrics (KPIs)
 
| Metric | Value |
|---|---|
| Average Congestion Score | 3.44 |
| Total Incidents | 566 |
| High Severity Incidents | 175K |
| Average Speed | 43.10 km/h |
| Average Temperature | 29.31 °C |
| Hourly Incident Rate | 2,830 |
| Total Vehicles | 167M |
 
---
 
## 📈 Visualizations
 
### 1. Count of Incidents by Incident Type (Pie Chart)
Breaks down all incidents by type:
- **VIP Movement** – 109 (19.26%)
- **Road Work** – 100 (17.67%)
- **Accident** – 94 (16.61%)
- **Breakdown** – 93 (16.43%)
- **Signal Fault** – 93 (16.43%)
- Other – 77 (13.6%)
### 2. Total Incidents by Vehicle Name (Bar Chart)
Compares incident counts across vehicle categories: Auto-Rickshaw, Bike, Bus, Car, and Truck — all showing near-equal distribution at ~100% relative share.
 
### 3. Total Incidents by Location (Bar Chart)
Top incident-prone locations:
- MG Road Junction (highest)
- Wardha Road Flyover
- Sitabuldi Crossing
- Dharampeth Square
### 4. Count of Incident ID by Severity (Donut Chart)
- **High** – 185 (32.69%)
- **Low** – 175 (30.92%)
- **Medium** – 182 (32.16%)
- **Unknown** – small share
### 5. Incidents by Month and Location (Matrix Table)
Detailed monthly breakdown (February, January, March) showing:
- Total Vehicles
- Total Incidents
- Average Congestion per location
### 6. Slicers / Filters
- **Location Name** – Filter by specific intersections/roads
- **Vehicle Type** – Filter by Auto-Rickshaw, Bike, Bus, Car, Truck
---
 
## 🗺️ Monitored Locations
 
| Location |
|---|
| Amravati Road Toll |
| Dharampeth Square |
| MG Road Junction |
| Sitabuldi Crossing |
| Wardha Road Flyover |
 
---
 
## 🗃️ Data Model
 
The dashboard is built on a **star schema** with the following tables:
 
### Fact Tables
| Table | Key Fields |
|---|---|
| `fact_traffic` | avg_speed_kmh, congestion_score, date_id, direction, hour, hour_bucket, is_weekend, location_id, vehicle details |
| `fact_incidents` | date_id, duration_mins, hour, hour_bucket, incident_id, incident_type, location_id, severity |
| `fact_weather` | condition, date_id, hour, hour_bucket, humidity_pct, temp_celsius, wind_kmh, location_id |
 
### Dimension Tables
| Table | Key Fields |
|---|---|
| `dim_date` | date_id, is_weekend, month, month_name, quarter, week |
| `dim_location` | city, latitude, longitude, location_id, location_name, zone |
| `dim_vehicle_type` | vehicle_name, vehicle_type |
 
### Aggregated Summary Tables
| Table | Key Fields |
|---|---|
| `agg_daily_summary` | avg_congestion, avg_speed_kmh, avg_temp, date_id, dominant_weather, high_sev_incidents, location_id, max_temp, min_temp |
| `agg_hourly_summary` | avg_congestion, avg_humidity, avg_speed_kmh, avg_temp, date_id, hour, hour_bucket, incident_count, location_id |
 
### Relationships
- `dim_date` → `fact_traffic`, `fact_incidents`, `fact_weather`, `agg_daily_summary`, `agg_hourly_summary` (via `date_id`, one-to-many)
- `dim_location` → `fact_traffic`, `fact_incidents`, `fact_weather`, `agg_daily_summary`, `agg_hourly_summary` (via `location_id`, one-to-many)
- `dim_vehicle_type` → `fact_traffic` (via vehicle key, one-to-many)
---
 
## 📁 File Structure
 
```
Pollution_analysis_dashboard.pbix   # Main Power BI file
README.md                           # Project documentation
Screenshot_2026-05-19_005332.png    # Dashboard screenshot
Screenshot_2026-05-19_005724.png    # Data model screenshot
```
 
---
 
## 🛠️ Requirements
 
- **Power BI Desktop** (latest version recommended)
- Data source access (if live connection is used)
- No additional custom visuals required — all visuals use built-in Power BI components
---
 
## 🚀 Getting Started
 
1. Clone or download this repository.
2. Open `Pollution_analysis_dashboard.pbix` in **Power BI Desktop**.
3. If prompted, update the data source credentials or file path.
4. Refresh the data to load the latest records.
5. Use the **location_name** and **vehicle_type** slicers to filter the dashboard interactively.
---
 
## 📌 Notes
 
- Data covers **January, February, and March** (Q1).
- All five monitored locations are within **Nagpur, Maharashtra, India**.
- The congestion score is on a normalized scale; higher values indicate greater congestion.
- High Severity Incidents (175K) represent aggregated weighted counts, not raw incident rows.
