# Homework_2
Question 1. Within the execution for Yellow Taxi data for the year 2020 and month 12: what is the uncompressed file size (i.e. the output file yellow_tripdata_2020-12.csv of the extract task)
134.5MiB 
Found this information by 
1. run backfill for yello taxi data on 12/2020
2. natigating to the GCP Bucket and look for the file size in the bucket

Question 2: What is the rendered value of the variable file when the inputs taxi is set to green, year is set to 2020, and month is set to 04 during execution? (1 point)
green_tripdata_2020-4.csv 
base on 
variables:
  file: "{{inputs.taxi}}_tripdata_{{trigger.date | date('yyyy-MM')}}.csv"

Question 3. How many rows are there for the Yellow Taxi data for all CSV files in the year 2020? 
running the 05_postgres_taxi_scheduled.yaml in Kestra to 
run the yellow taxi data from 01/01/2020 to 01/01/2021
SELECT COUNT(*) as record_count_2020_range
FROM public.yellow_tripdata
WHERE tpep_pickup_datetime >= '2020-01-01 00:00:00' 
  AND tpep_dropoff_datetime <= '2020-12-31 23:59:59';

Question 4. How many rows are there for the Green Taxi data for all CSV files in the year 2020? (1 point)
I picked 1,734,051 by running the 05_postgres_taxi_scheduled.yaml in Kestra to 
run the green taxi data from 01/01/2020 to 01/01/2021

then do the following :

SELECT COUNT(*) as record_count_2020_range
FROM public.green_tripdata
WHERE lpep_pickup_datetime >= '2020-01-01 00:00:00' 
  AND lpep_dropoff_datetime <= '2020-12-31 23:59:59';

Question 5. How many rows are there for the Yellow Taxi data for the March 2021 CSV file? (1 point)
I run the 09_gcp_taxi_scheduled.yaml from to grab the March 2021 to have all the March data
insert into the Google Bucket then check the yellow_tripdata_2021_03 table for records COUNT
select count(*)
from yellow_tripdata_2021_03

Question 6. How would you configure the timezone to New York in a Schedule trigger?
add timezone (America/New_york)underneath the cron entry 
triggers:
  - id: green_schedule
    type: io.kestra.plugin.core.trigger.Schedule
    cron: "0 9 1 * *"
    inputs:
      taxi: green
