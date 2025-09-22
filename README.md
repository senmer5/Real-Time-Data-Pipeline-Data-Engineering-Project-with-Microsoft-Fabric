# 🚖 Real-World Data Engineering Project 🚦

**Project Name :**  Uber-like Streaming Data Pipeline (Medallion Architecture)  

**Goal:**  
Process trip data with Microsoft Fabric through **Bronze → Silver → Gold layers**, simulate streaming from CSV files, and build **real-time dashboards with automated actions**.  

Welcome to this project where we built an end-to-end real-time data pipeline using Microsoft Fabric. This project was carried out as part of a data engineering program, focusing on modern architectural principles such as the Medallion Architecture.

<img width="1164" height="497" alt="diyagram" src="https://github.com/user-attachments/assets/15c802ee-7c5e-49ee-823c-33446b2d1829" />

---

## ✨ 1. Fabric Workspace Setup  
- Log in to Microsoft Fabric portal.  
- Create a new Workspace (e.g., `UberPipelineWorkspace`).  
- Add required components:  
  - Lakehouse (Bronze, Silver, Gold)  
  - Eventstream (streaming ingestion)  
  - KQL Database (real-time queries)  
  - Data Warehouse (Gold layer)  
  - Activator (threshold-based actions)  

---

## ✨ 2. Data Source & Streaming Simulation  
- Data stored in **Google Drive**: `trip_data.csv`, `trip_fare.csv`.  
- Instead of Docker:  
  - Use **PySpark Notebooks** or **Fabric Dataflow** to read rows continuously.  
  - Publish rows to **Eventstream**, simulating streaming.  

<img width="1847" height="1063" alt="bronze1" src="https://github.com/user-attachments/assets/ea255eae-89a5-4aa7-9b6f-176dd23bb03b" />

---

## ✨ 3. Eventstream Configuration  
Eventstream routes data to two destinations:  
1. **Lakehouse / Bronze Layer**  
   - Save to `/Files/raw_taxi_data/` in **Delta Lake** format.  
   - Partition by `ingest_date`, retention: 30 days.  
2. **KQL Database / Eventhouse**  
   - For real-time queries and dashboards.

<img width="3620" height="1778" alt="bronze 3" src="https://github.com/user-attachments/assets/49a67a93-3435-4910-8015-615a9c045e0f" />

---

## ✨ 4. Bronze Layer – Raw Data  
- Purpose: Store raw data as-is.  
- Write Eventstream output into `/Files/bronze_taxi_data/` in Delta format.  
- Keep timestamp + message offset.

<img width="3043" height="1989" alt="bronze to silver cleaning" src="https://github.com/user-attachments/assets/458de3dc-cd0d-4563-bbd9-c67e7edb5a7f" />

---

## ✨ 5. Silver Layer – Cleaned Data (PySpark + Lakehouse)  
- Define schemas for `trip_data` & `trip_fare`.  
- Clean & transform:  
  - Convert datetime → TIMESTAMP.  
  - Remove negative/null values.  
  - Fill missing fare values with `0`.  
- Feature engineering:  
  - `trip_duration`, `average_speed`.  
  - Join `trip_data` + `trip_fare` on `trip_id`.  
- Deduplication & validation.  
- Save to **Delta table**: `taxi_silver_trips`, partitioned by `pickup_date`.  

<img width="2713" height="2186" alt="silver lakehouse" src="https://github.com/user-attachments/assets/b4c2146d-39ae-446f-ad15-18940dbefb41" />

---

## ✨ 6. Gold Layer – Analytics (Dataflow Gen2 + Data Warehouse)  
- Purpose: Store fully processed, business-ready data optimized for analytics and reporting.
- Tech: Dataflow Gen2 → Data Warehouse
- Use Cases:
	•	Business dashboards & aggregated reporting
	•	Cross-functional insights
	•	Power BI integration for rich visualizations(star schema).

<img width="3542" height="1998" alt="data flow gen 2 2" src="https://github.com/user-attachments/assets/d1ba9156-78c4-4f10-8662-391171ce507a" />

<img width="2915" height="1498" alt="semantic model 3" src="https://github.com/user-attachments/assets/f4d86422-aab6-4f48-b91a-d190da89777d" />

---

## ✨ 7. Real-Time Monitoring & Dashboard  
- Eventstream → KQL Database.  
- Build live dashboard with:  
  - 🚦 Active trips  
  - 📍 Live locations  
  - 🌐 Hotspot areas  
- Powered by **KQL queries**.
  
<img width="3047" height="1750" alt="eventhouse1" src="https://github.com/user-attachments/assets/41d02a64-32f6-454d-bdf7-7967f23dd9ad" />

<img width="3112" height="1815" alt="realtime dashboard2" src="https://github.com/user-attachments/assets/d3b8248d-954f-4b11-9193-6e2a6799b6b4" />

---

## ✨ 8. Action Triggers (Activator)  
- Watch tables or metrics.  
- Trigger when thresholds are reached:  
  - 📩 Send notification  
  - 🔁 Trigger another Dataflow  
  - 🛠️ Call Azure Function
    
<img width="1089" height="608" alt="activator1 " src="https://github.com/user-attachments/assets/3a19f52e-ed26-42bf-9b25-54166bab9051" />

<img width="1047" height="535" alt="activator 2" src="https://github.com/user-attachments/assets/97075e3e-929f-49ab-9e01-b6b36301a549" />

---

## ✨ 9. Testing & Validation  
- Validate full pipeline: Bronze → Silver → Gold.  
- Ensure dashboards and triggers respond correctly.

<img width="1079" height="584" alt="a3" src="https://github.com/user-attachments/assets/6c3ea36b-1154-42a1-a7fc-abb9793a28aa" />

---

## ⚙️ 10. Technologies Used
- Microsoft Fabric
- Eventstream – for real-time data ingestion
- Lakehouse (Bronze & Silver layers) – for storage and raw data processing
- PySpark Notebooks – for transformations
- Dataflow Gen2 – for modeling a star schema
- Data Warehouse (Gold layer) – for optimized reporting
- KQL Database – for real-time queries
- Real-Time Dashboard – for visualization
- Medallion Architecture – as the guiding architectural principle
  
---  


## 👥 Team & Mentorship

- Team Members :  Senem Mergenci - Zehra Okay - Mehmet Gezer - Sefa Öztürk - Sueda Ekiz

- Mentors : A. Özcan Kurşun -  Abdullah Mart

- Supervisor : Fatih Demir (Instructor)
