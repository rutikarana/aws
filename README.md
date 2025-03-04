AWS Glue ETL Pipeline with CloudFormation
Project Overview
This project demonstrates how to set up an AWS Glue ETL pipeline using CloudFormation to deploy the required infrastructure. The workflow extracts raw CSV data from Amazon S3, transforms it using AWS Glue, and loads processed data in Parquet format back to S3. Finally, AWS Athena is used to query the processed data.
Key Components
AWS CloudFormation – Deploys S3 bucket, IAM Role for Glue, and Athena Workgroup
AWS Glue – Handles ETL jobs for transforming data
AWS S3 – Stores raw and processed data
AWS Athena – Queries the processed data
Glue Crawlers – Creates metadata tables
Glue Workflows – Orchestrates ETL jobs
Project Architecture
1. Infrastructure Deployment (CloudFormation YAML File)
The following resources were created using CloudFormation:
S3 Bucket: Stores raw data, processed data, scripts, and logs
IAM Role: Provides necessary permissions for AWS Glue
Athena Workgroup: Manages query execution
2. Folder Structure in S3
└── S3-Bucket-Name
    ├── athena  # Stores Athena query results
    ├── processedData  # Stores transformed data in Parquet format
    ├── rawData  # Contains raw CSV files
    │   ├── customers
    │   │   └── customers.csv
    │   ├── orders
    │   │   └── orders.csv
    ├── scriptLocation  # Stores Glue job scripts
    └── tmpDir  # Stores logs and temporary data
3. ETL Process with AWS Glue
Created two Glue databases:
Raw_data (for raw CSV files)
Processed_data (for transformed Parquet files)
Used Glue Crawlers to create metadata tables from raw data
Developed Glue ETL Jobs using AWS Glue Studio (Visual Editor)
ETL Transformations:
Convert CSV to Parquet format for better query performance
Add a timestamp column and set it as a partition key
Target Data Store: Processed data is stored in Parquet format in the processedData folder in S3
4. Querying Data with AWS Athena
Athena was configured to read from the Processed_data database
Queries were executed in the Athena Workgroup to analyze the processed data
5. Orchestrating with AWS Glue Workflow
Created a workflow to integrate both Customer and Order ETL jobs
Ensured the sequential execution of ETL tasks
How to Deploy the Project
Step 1: Deploy Infrastructure using CloudFormation
1.Upload the YAML file to AWS CloudFormation
2.Create a new stack and provide an S3 bucket name
3.Wait for the stack to complete
Step 2: Upload Raw Data to S3
1.Place customers.csv and orders.csv into the rawData folder
Step 3: Configure AWS Glue
1.Create Glue databases (Raw_data, Processed_data)
2.Run Glue Crawlers to generate metadata tables
3.Create and configure Glue ETL Jobs
Step 4: Run the ETL Workflow
1.Start the Glue Workflow to process both customer and order data
2.Verify that processed Parquet files are stored in S3
Step 5: Query Data with Athena
1.Use Athena Workgroup to query the Processed_data database
Conclusion
This project successfully demonstrates how to:
Deploy infrastructure using AWS CloudFormation
Set up an ETL pipeline with AWS Glue
Use Athena to query transformed data
Automate data processing using Glue Workflows
