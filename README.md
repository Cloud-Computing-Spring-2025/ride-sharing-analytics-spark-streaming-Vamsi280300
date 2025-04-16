Real-Time Ride-Sharing Analytics with Apache Spark
This project implements a real-time analytics pipeline for a ride-sharing platform using Apache Spark Structured Streaming. The pipeline ingests streaming data, performs real-time aggregations, and analyzes trends over time. The project is split into three main tasks:

Task 1: Ingest and parse real-time ride data.

Task 2: Perform real-time aggregations on driver earnings and trip distances.

Task 3: Analyze trends over time using a sliding time window.

Environment Setup:
------------------
Install Apache Spark and PySpark: Ensure you have Apache Spark and PySpark installed. You can install PySpark via pip if it's not already installed:

```bash
pip install pyspark
```

Run the data_generator.py (provided in the project):

This script simulates real-time ride-sharing data and sends it to a socket (localhost:9999). It's essential for simulating the stream that the tasks will process.

Run the streaming jobs using spark-submit or directly as Python scripts.


Task 1: Ingest and Parse Real-Time Ride Data:

This task reads streaming data from a socket and parses it into a structured format using a JSON schema.

Code Overview:
Schema: Defines the structure for trip_id, driver_id, distance_km, fare_amount, and timestamp.

Stream: Ingests data from localhost:9999 and parses the incoming JSON into structured columns.

Output: Writes the parsed data to CSV files.

How to Run:
Run the script using:

```bash
spark-submit task1.py
```

Task 2: Real-Time Aggregations (Driver-Level):

This task performs real-time aggregations on the parsed data, specifically:

Total fare by driver (driver_id).

Average distance traveled by driver.

Code Overview:
Watermarking: Handles out-of-order data by specifying a watermark (1 minute).

Aggregation: Groups by driver_id and computes the sum of fare_amount and average of distance_km.

Output: Saves each batch's output to CSV files using foreachBatch.

How to Run:
Run the script using:

```bash
spark-submit task2.py
```

Task 3: Windowed Time-Based Aggregations:

This task performs a 5-minute windowed aggregation on the fare_amount column, sliding every 1 minute.

Code Overview:
Watermarking: Ensures the data can be processed even if it arrives late (watermark duration 2 minutes).

Windowing: Uses a sliding window of 5 minutes with a slide duration of 1 minute.

Output: Writes the windowed aggregation results to CSV files using foreachBatch.

How to Run:
Run the script using:

```bash
spark-submit task3.py
```

