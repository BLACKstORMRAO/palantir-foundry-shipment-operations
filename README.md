Palantir Foundry — Shipment & Orders Operations Platform

Built as part of the Analyticore Palantir Foundry Foundations Program (March 2026)
An end-to-end data operations platform built on Palantir Foundry covering data ingestion, pipeline transformation, ontology modeling, Workshop app development, and AIP Logic automation.


📌 Project Overview
This project demonstrates a full Palantir Foundry implementation across 5 modules:
ModuleTool UsedOutputData IngestionFile ImportsRaw datasets (claims, orders, shipments)Data TransformationPipeline BuilderCleaned & joined datasetsData ModelingOntology Manager7 Object TypesData ExplorationContourEDA dashboards & KPI boardsApp DevelopmentWorkshopShipment Operations Centre + Orders InboxAI AutomationAIP Logic (Gemini 2.5 Pro)Order Priority Classification

🗂️ Module 1 — Data Ingestion & Raw Datasets

Uploaded raw datasets: claims_raw, orders_office_goods, orders_bureau_transactions, customers_raw, products_raw, transaction_raw
Dataset: claims_raw — 300 rows · 8 columns (claim_id, policy_id, date, claim_value, is_accepted, state, zip_code)
All datasets validated via Data Health checks


🔁 Module 2 — Pipeline Builder (ETL Transformation)
My First Pipeline

Inputs: transaction_raw, products_raw, customers_raw
Transformations: Clean → Join → Aggregate
Output: customer_lifetime_value (4 columns)

Orders Pipeline

Inputs: orders_office_goods, orders_bureau_transactions, consolidated_customers
Transformations: Clean → Join → Union → Extend
Output: All_oders (11 columns)
Extended columns added:

priority_level — Critical / Medium / High / Low (based on days_until_due)
is_overdue — Yes / NO (based on days_until_due < 0)
total_order_value — Multiply(quantity, unit_price)


Successfully deployed ✅ (6 checks passed)


🧬 Module 3 — Ontology (Data Lineage)

Built Data Lineage graph with 53 nodes selected
Created 7 Object Types:

Object TypeDescription[Kashish] RouteFlight route data[Kashish] AirportAirport information[Kashish] AircraftAircraft registry[Kashish] RunwayRunway details[Kashish] FlightFlight records[Kashish] AirlineAirline data[Kashish] Flight AlertAlert monitoring

Configured Object Storage, Live Pipeline, and Datasources for kashish All Oders
Schema: Up to date ✅


📊 Module 4 — Contour (Exploratory Data Analysis)
Explored kashish All Oders object type (1,492 results):

Quantity distribution — histogram analysis
Order Due Date — time series (June–July 2023)
Days Until Due — range distribution
Item Name breakdown — 30" Monitor (167), Office Desk (157), Paper Clips (156)
Assignee analysis — Kristen Mohr (157), John Dooley (152), Lorraine Bahringer (145)
Customer breakdown — Hessel-Muller (73), King Feeney and Kutch (67)

Also ran Equipment Analysis on parts dataset:

3,428 unique parts across 5 equipment types
Columns: part_id, eq_id, date, type, weight, material, color, dimensions


🖥️ Module 5 — Workshop App Development
App 1: Shipment Operations Centre

Object Type: [Kashish] Shipment (83 records)
Visualizations:

Bar chart — Count of shipments by Arriving Destination Date
Stacked bar + line chart — Product quantities by date (Blue Triangles · Red Squares · Yellow Circles)
Interactive filters: Origin Location · Destination Location · Date Range · Quantity


Data table: Shipment Name · Origin · Destination · Departing Date · Arriving Date · Product · Quantity · Vehicle

App 2: kashish orders inbox

Object Type: kashish All Oders (1,492 records)
Sections:

ALL ORDERS table — Item Name · Quantity · Order Due Date · Days Until Due · Customer
Pie chart — Status breakdown: Assigned 43% · Closed 42% · Open 16%
Bar chart — Days Until Due distribution
Filter panel — Item Name · Assignee · Customer · Days Until Due · Order Due Date · Status · Unit Price


Actions: Assign button · Analyze Priority with AI button


🤖 Module 6 — AIP Logic (AI Automation)
Built order priority classification logic using Gemini 2.5 Pro via AIP Logic:
priority_level = Case(
  When(days_until_due == 7): "Critical"
  When(days_until_due <= 20): "Medium"
  When(days_until_due <= 40): "High"
  Else: "Low"
)

is_overdue = Case(
  When(days_until_due < 0): "Yes"
  Else: "NO"
)

total_order_value = Multiply numbers([quantity, unit_price])

Function: markShipmentsForConsolidation (TypeScript)
Updates shipment status to "Eligible for Consolidation"
Live Preview tested ✅


🛠️ Tools & Technologies
Palantir Foundry · Pipeline Builder · Ontology Manager · Workshop · Contour · AIP Logic · PySpark · TypeScript · Gemini 2.5 Pro · Data Lineage

👤 Author
Kashish Yadav — Data Analyst

📧 kashishrao68@gmail.com
💼 LinkedIn

