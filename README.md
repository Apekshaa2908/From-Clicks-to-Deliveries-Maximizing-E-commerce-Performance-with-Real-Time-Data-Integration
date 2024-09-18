# From-Clicks-to-Deliveries-Maximizing-E-commerce-Performance-with-Real-Time-Data-Integration

**Project Overview**
The project aims to integrate and optimize an e-commerce platform with logistics management by leveraging real-time data streams. We are focusing on two key areas:

** Clicks**
**1. Table Creation**
This script uses the Boto3 library to create a DynamoDB table named Clicks. The table has a single partition key, item_id, of type string. The provisioned throughput is set to 5 units for both reads and writes. Once created, the script waits for the table to be fully set up before printing a success message.

**2. Lambda Function**
This AWS Lambda function processes clickstream data from Kinesis streams and stores it in the DynamoDB Clicks table. The function decodes base64-encoded Kinesis data, converts it to JSON, validates the necessary fields (item_id, item_name, click_counts, timestamp), and inserts the record into DynamoDB. The function logs key steps and handles any errors, ensuring the reliability of the data processing pipeline.

**3. Data Generation**
This script simulates clickstream data generation for three products: Mobile Phone, Laptop, and Camera. It generates random click counts and timestamps for each item and sends the data to an Amazon Kinesis stream. This stream feeds the data into the Lambda function for processing. The data generation loop continuously streams real-time data to Kinesis at set intervals.

These three components together enable real-time clickstream data processing: the table stores the data, the Lambda function processes it, and the generator simulates the data feed.
