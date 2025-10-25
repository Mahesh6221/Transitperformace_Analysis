SWIFT Assignment Transit Performance Analysis

Project Overview
This project analyzes shipment transit performance for a logistics analytics company.
The dataset contains detailed tracking information of shipments moving through courier networks.
The goal is to examine how shipments move through facilities, calculate performance metrics, and output summarized datasets.


How to Use This Project
To use or reproduce this project, simply clone the repository from GitHub:
git clone https://github.com/Mahesh6221/Transitperformace_Analysis.git


Tools and Environment

1. Platform: Databricks

2. Language: PySpark (using Spark DataFrame APIs)

3. File Format: JSON (input) → CSV (output)

4. Volumes Used:

i. project_transit_performance_analysis (Input)(JSON Format)
ii. transittarget (Detailed Transit Output) (CSV Format)
iii. transitperformance (Summary Output) (CSV Format)


Data Source and Setup

Step 1: Download the Data
The dataset was downloaded from the provided resource in the assignment instructions.

Step 2: Upload to Databricks
The JSON dataset was uploaded to Databricks under a volume named: project_transit_performance_analysis

Step 3: Read JSON Data into Spark
The dataset was read using Spark with multiline JSON support:

df = spark.read.option("multiline", "true").json(
    "/Volumes/workspace/default/project_transit_performance_analysis/Swift Assignment 4 - Dataset (1).json"
)

step 4: Initial exploration (e.g., df.printSchema(), df.count(), df.show()) was performed to understand data structure and nested fields.



Project Workflow (Assignment Parts)

Part 1: Load and Explore Data
i. Download the data
ii. Loaded the dataset into Spark DataFrame.
iii. Explored schema, checked for nested structures and null values.
iv. Validated the JSON parsing and identified the main fields.

Part 2: Flatten and Extract Transit Data

i. Extracted shipment-level details such as:
Tracking number, service type, service description, carrier code

ii. Package weight, packaging type
iii. Location info such as Origin and destination details(city,state)
iv. Flattened all transit events (events array) into a structured tabular format including:
eventType, timestamp, eventDescription, and address details.

Part 3: Compute Transit Performance Metrics
Derived the following shipment-level metrics:

i. Facility Touchpoints: Counted unique facilities visited.
ii. Transit Time: Calculated total transit hours (pickup → delivery).
iii. Transit Velocity: Average hours per facility.
iv. Delivery Performance: Out-for-delivery attempts and first-attempt success rate.
v. Service Classification: Grouped services as express or standard.

Part 4: Handle Edge Cases

i. Implemented logic to manage:
ii. Missing or null fields.
iii. Different timestamp formats ($numberLong, ISO).
iv. Incomplete event sequences and duplicate events.
v. Missing address data.
vi.Empty or missing event arrays.

Part 5: Output Detailed Transit CSV
Created a detailed shipment-level CSV containing metrics for each shipment.

Volume Created:
transittarget

Output Path:
output_path = "/Volumes/workspace/default/transittarget/transit_performance_detailed.csv"

Output Columns Include:

i. tracking_number, service_type, carrier_code, package_weight_kg, origin_city, destination_city, etc.
ii. total_transit_hours, num_facilities_visited, avg_hours_per_facility, num_out_for_delivery_attempts, etc.


Part 6: Output Network Performance Summary CSV

Generated an aggregated summary CSV showing overall transit network performance.

Volume Created:
transitperformance

Output Path:
output_path_combined = "/Volumes/workspace/default/transitperformance/transit_performance_summary.csv"


Metrics Included:
i. Overall averages: total shipments, avg/median/std transit hours.
ii. Facility metrics per shipment.
iii. Service type comparison (express vs standard).
iv. Delivery performance summary (first attempt %, avg delivery attempts).


Final Deliverables:

i. Source Code Python
ii. transit_performance_detailed.csv
(Detailed shipment-level performance data)
iii.transit_performance_summary.csv
(Network-level summary metrics)


transitperformance (Summary Output)