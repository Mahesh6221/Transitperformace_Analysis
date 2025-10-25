# SWIFT Assignment: Transit Performance Analysis

## Project Overview

This project analyzes shipment transit performance for a logistics analytics company.  
The dataset contains detailed tracking information of shipments moving through courier networks.  
The goal is to examine how shipments move through facilities, calculate performance metrics, and output summarized datasets.

---

## Table of Contents

- [Project Overview](#project-overview)
- [How to Use This Project](#how-to-use-this-project)
- [Tools and Environment](#tools-and-environment)
- [Data Source and Setup](#data-source-and-setup)
- [Project Workflow](#project-workflow-assignment-parts)
- [Final Deliverables](#final-deliverables)
- [Credits](#credits)
- [License](#license)

---

## How to Use This Project

To use or reproduce this project, simply clone the repository from GitHub:

git clone https://github.com/Mahesh6221/Transitperformace_Analysis.git



Follow the instructions in the Notebooks or Python scripts as documented.

---

## Tools and Environment

- Platform: Databricks  
- Language: PySpark (using Spark DataFrame APIs)  
- File Format: JSON (input) → CSV (output)
- Volumes:
    - `project_transit_performance_analysis` (Input, JSON format)
    - `transittarget` (Detailed Transit Output, CSV format)
    - `transitperformance` (Summary Output, CSV format)

---

## Data Source and Setup

### Step 1: Download the Data
The dataset was downloaded from the resource provided in the assignment instructions.

### Step 2: Upload to Databricks
Upload the JSON dataset to Databricks under the volume:
- `project_transit_performance_analysis`

### Step 3: Read JSON Data into Spark

df = spark.read.option("multiline", "true").json(
"/Volumes/workspace/default/project_transit_performance_analysis/Swift Assignment 4 - Dataset (1).json"
)



### Step 4: Initial Exploration
Explored schema, row counts, samples, and nested fields using:
- `df.printSchema()`
- `df.count()`
- `df.show()`

---

## Project Workflow (Assignment Parts)

### Part 1: Load and Explore Data

- Download and load dataset into a Spark DataFrame.
- Validate JSON parsing and explore schema for nested and null fields.

### Part 2: Flatten and Extract Transit Data

- Extracted shipment-level details: tracking number, service type, carrier code, package weight, packaging type, origin/destination, and all transit events.
- Flattened 'events' array to structured rows: eventType, timestamp, description, address.

### Part 3: Compute Transit Performance Metrics

- Facility Touchpoints: counted unique facilities visited.
- Transit Time: calculated pickup-to-delivery hours.
- Transit Velocity: average hours per facility.
- Delivery Performance: out-for-delivery attempts and first-attempt success rate.
- Service Classification: express/standard.

### Part 4: Handle Edge Cases

- Handled missing/null fields, inconsistent timestamps, incomplete/duplicate events, and missing address/event arrays.

### Part 5: Output Detailed Transit CSV

- Output: `transittarget`
- Path: `/Volumes/workspace/default/transittarget/transit_performance_detailed.csv`
- Columns: tracking_number, service_type, carrier_code, package_weight_kg, origin_city, destination_city, total_transit_hours, num_facilities_visited, avg_hours_per_facility, num_out_for_delivery_attempts, etc.

### Part 6: Output Network Performance Summary CSV

- Output: `transitperformance`
- Path: `/Volumes/workspace/default/transitperformance/transit_performance_summary.csv`
- Metrics: shipment count, avg/median/std transit hours, facility metrics, service type comparison, delivery summary.

---

## Final Deliverables

- Python Source Code
- `transit_performance_detailed.csv`: Detailed shipment-level data
- `transit_performance_summary.csv`: Network-level summary metrics


transitperformance (Summary Output)