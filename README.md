# Airline Data Ingestion

This solution automates the daily ingestion and transformation of flight transactional data into Amazon Redshift through a fully managed, AWS-native pipeline architecture.




## Project Overview
In the airline sector, the ability to process flight data accurately and promptly is essential for analytics, reporting, and informed decision-making. This project replicates the process of ingesting daily flight data into an AWS-based data lake architecture. The data is then transformed and stored in Amazon Redshift for advanced analysis. The pipeline is designed to be fully automated, fault-tolerant, and capable of sending real-time notifications about the processing status.
## Motivation

 Motivation
Modern data engineering systems must manage high volumes of data with minimal manual effort. This project showcases how to create an automated data ingestion pipeline using AWS services such as S3, Glue, Step Functions, and Redshift. The primary goal is to build a robust and resilient pipeline that can handle failures efficiently while keeping stakeholders informed through timely alerts.
## AWS Services used in the project

1-Amazon S3 (Simple Storage Service):
Serves as the central data lake for storing daily flight data in a Hive-style partitioned format. Raw data files are uploaded to S3 on a daily schedule.

2-Amazon EventBridge:
Configured with rules to automatically trigger AWS Step Functions whenever new flight data lands in S3. This eliminates the need for manual intervention and ensures real-time pipeline execution.

3-AWS Step Functions:
Acts as the workflow orchestrator for the ETL process. It coordinates tasks by first running the Glue Crawler to update the Data Catalog, then executing the Glue Job for transformations. On successful completion, data is loaded into the Redshift fact table. In case of failure, an SNS alert is sent via email.

4-AWS Glue:

Glue Crawler: Scans and catalogs the raw data in S3, updating metadata in the AWS Glue Data Catalog.

Glue Job: Handles transformation tasks such as data cleaning and formatting to match the Redshift schema.

5-Amazon Redshift:
A fully managed data warehouse used to store processed flight data in a fact table, enabling fast queries and advanced analytics.

6-Amazon SNS (Simple Notification Service):
Delivers email notifications on pipeline execution status (success or failure), ensuring stakeholders receive real-time updates.


## Requirements
1-AWS Account

2-Amazon S3 bucket for storing raw flight data

3-AWS Glue: Glue Crawler and Glue Job set up for cataloging and transforming data

4-AWS Step Functions: Configured state machine for orchestrating the workflow

5-Amazon Redshift: A flights fact table for storing processed data

6-Amazon SNS: An SNS topic and subscription for receiving notifications

7-IAM Roles with appropriate permissions for accessing S3, Glue, Redshift, SNS, and Step Functions

8-SQL queries


## Workflow

CSV → S3 → EventBridge → Step Functions → Glue Crawler → Glue ETL Job → Redshift
                                                       ↘︎ SNS (Success/Failure)

                                                       
## Step-Step- Implementation

Step-by-Step Implementation
Set Up Amazon S3 Bucket:

Create an S3 bucket to store daily flight data in Hive-style partitions.
Configure Amazon EventBridge Rule:

Set up an EventBridge rule that triggers the Step Function when new files are uploaded to the S3 bucket.
Define AWS Step Function Workflow:

Create a Step Function state machine that orchestrates the Glue Crawler, Glue Job, data loading to Redshift, and SNS notifications.
Create AWS Glue Crawler and Job:

Define a Glue Crawler to crawl the S3 bucket and update the Glue Data Catalog.
Create a Glue Job using Python or Scala to perform data transformations.
Set Up Amazon Redshift:

Create a Redshift cluster and define the flights fact table schema to store processed data.
Integrate SNS for Notifications:

Configure an SNS topic and subscription to receive email notifications on the ETL process's success or failure.
Testing and Validation:

Upload sample data to the S3 bucket and verify that the entire pipeline triggers correctly. Check the data loaded in Redshift and ensure notifications are sent via SNS.

## Architecture

<img width="821" height="801" alt="Architecture Diagram of Airline-Data-Ingestion-Pipeline (1)" src="https://github.com/user-attachments/assets/cea85ed0-eacd-4e2f-b2f6-c8ce1e1b51c0" />


## Outcomes

Automated and Scalable: The pipeline is fully automated and scales seamlessly with data volume.
Real-Time Processing: Reduces the latency of getting insights from daily flight data.
Error Handling and Notifications: Provides robust error handling and instant notifications, ensuring transparency and reliability.
