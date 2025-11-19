# ETL Pipeline to Process Student Grades

## Function

This project creates an ETL pipeline using AWS compute and storage services to process student grades. It is composed of an front-end UI, where the user can access student grades, as well as input new ones. The students' overall grades get updated as new additions are made to the databse through the UI. The main goals of the project are to implement a pipeline with real-time input and visibility into studnet grades, automated back-end processing with minimal infrastructure, and having a clean, user-friendyl front-end for both grading and viewing. 

## Pipeline Overview

- String/integer input from user in UI --> stored as JSON in S3 bucket
- S3 upload triggers Lambda to calculate grade (based on points scored and type of assignment) --> stored in RDS
- Second Lambda triggered to calculate course average --> stored in S3 as CSV
- Display data in table format in UI (Streamlit dashboard)

## Files

### `app.py`

This is our main file and has our code for running both the input and output end of our project. You can run it locally typing `streamlit run app.py` in terminal. 

### `src/s3_uploader.py`

This is a modified version of the provided code for connecting S3 to python. We added functions for sending JSON data to S3.

### `s3_to_rds.py` and `rds_to_s3.py`

These files contain the code used in our lambdas. First, the fie s3 to rds code is used to get the data that we upload as jsons into one RDS database table. That triggers the rds to s3 lambada which takes the mostly unprocessed rds data and aggregates it by student into a new grade summary table in S3, which is ingested by the streamlit grade viewer.
