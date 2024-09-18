# From-Clicks-to-Deliveries-Maximizing-E-commerce-Performance-with-Real-Time-Data-Integration

**Project Overview**
The project aims to integrate and optimize an e-commerce platform with logistics management by leveraging real-time data streams. We are focusing on two key areas:

**Clicks**


**1. Table Creation**
This script uses the Boto3 library to create a DynamoDB table named Clicks. The table has a single partition key, item_id, of type string. The provisioned throughput is set to 5 units for both reads and writes. Once created, the script waits for the table to be fully set up before printing a success message.

**2. Lambda Function**
This AWS Lambda function processes clickstream data from Kinesis streams and stores it in the DynamoDB Clicks table. The function decodes base64-encoded Kinesis data, converts it to JSON, validates the necessary fields (item_id, item_name, click_counts, timestamp), and inserts the record into DynamoDB. The function logs key steps and handles any errors, ensuring the reliability of the data processing pipeline.

**3. Data Generation**
This script simulates clickstream data generation for three products: Mobile Phone, Laptop, and Camera. It generates random click counts and timestamps for each item and sends the data to an Amazon Kinesis stream. This stream feeds the data into the Lambda function for processing. The data generation loop continuously streams real-time data to Kinesis at set intervals.

These three components together enable real-time clickstream data processing: the table stores the data, the Lambda function processes it, and the generator simulates the data feed.

**Trucks**

**1. Table Creation**
The script creates a DynamoDB table named TrucksData, with Truck_ID as the partition key and Effective_Date as the sort key. The table uses provisioned throughput with 5 read and write capacity units. It waits for the table to be successfully created before proceeding.

**2. Lambda Function**
This Lambda function processes incoming truck telemetry data via an API request and stores it in the TrucksData DynamoDB table. It manages Slowly Changing Dimension (SCD) Type 2 by deactivating old records and inserting new ones. The function also ensures data integrity, updating existing active records with an expiration date before adding new telemetry data for each truck.

**3. Data Generation**
The script simulates truck telemetry data for 3 trucks, generating random values for GPS location, engine diagnostics, vehicle health, environmental conditions, and more. It sends this data to an API (presumably backed by a Lambda function) every minute. The telemetry data includes Effective_Date, Expiration_Date, and a flag to mark whether a record is active (is_active).
