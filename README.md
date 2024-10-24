# SQL-Zuber-Project

# Zuber Ride-Sharing Data Analysis - Chicago

# Project Overview

This project involves analyzing taxi ride data in Chicago for Zuber, a new ride-sharing company. The aim is to discover patterns in passenger preferences and understand the impact of external factors, such as weather, on ride frequency and duration. Using SQL, this project will explore the relationships between rides, weather conditions, and other key variables, applying various queries to draw insights from the database.


# Project Objectives

1. Exploratory Data Analysis: Analyze the number of rides per taxi company over specific periods and compare results between different companies.

2. Weather Impact on Rides: Investigate the effect of weather conditions (such as rain) on the duration of rides between key neighborhoods (Loop and O’Hare) during specific time frames (rainy Saturdays vs other days).

3. SQL Queries and Hypothesis Testing: Use SQL joins, aggregate functions, and conditional logic to extract meaningful insights from the database.

# Dataset Description

The data is provided through several tables stored in a database. Below are the key tables used in the analysis:

# neighborhoods
- name: Name of the neighborhood.

- neighborhood_id: Neighborhood code.

# cabs

- cab_id: Vehicle code.

- vehicle_id: The vehicle's technical ID.

- company_name: The company that owns the vehicle.

# trips

- trip_id: Ride code.

- cab_id: Code of the vehicle operating the ride.

- start_ts: Start date and time of the ride (rounded to the hour).

- end_ts: End date and time of the ride (rounded to the hour).

- duration_seconds: Ride duration in seconds.

- distance_miles: Ride distance in miles.

- pickup_location_id: Pickup neighborhood code.

- dropoff_location_id: Dropoff neighborhood code.

- weather_records

- record_id: Weather record code.

- ts: Date and time of the weather record (rounded to the hour).

- temperature: Temperature at the time of the record.

- description: Description of the weather conditions (e.g., "light rain", "scattered clouds").


# Table Relationships

- There is no direct relationship between the trips and weather_records tables, but they can be joined based on the time the ride started (trips.start_ts) and the time the weather record was taken (weather_records.ts).

# Project Steps

  Step 1: Exploratory Data Analysis

  1. Total Rides per Taxi Company (Nov 15-16, 2017):

      - Find the total number of rides per company for Nov 15-16, 2017.

      - Use COUNT() to calculate the number of rides and name the resulting field trips_amount.
  
      - Sort the results by trips_amount in descending order.

Example Query:


2. Rides for Taxi Companies "Yellow" and "Blue" (Nov 1-7, 2017):

     - Find the number of rides for taxi companies whose names contain "Yellow" or "Blue" during Nov 1-7, 2017.
    
     - Group the results by the company_name field.
  
Example Query:


3. Top Companies vs Other (Nov 2017):

     - Group rides for the two top companies, Flash Cab and Taxi Affiliation Services, under their names and group all other companies as "Other".

     - Sum up the total rides for each group and order by total rides.


## Step 2: Analyze Ride Duration Based on Weather Conditions
Weather Grouping:

Create a query to group weather conditions as "Bad" (if description contains "rain" or "storm") or "Good" for other conditions.
Use the CASE statement to categorize weather conditions and return the results alongside timestamps.
Example Query:

sql
Copy code
SELECT ts, 
       CASE 
           WHEN description LIKE '%rain%' OR description LIKE '%storm%' THEN 'Bad'
           ELSE 'Good'
       END AS weather_conditions
FROM weather_records;
Rides from Loop to O'Hare (Saturdays Only):

Retrieve ride details for trips starting in the Loop (neighborhood_id: 50) and ending at O'Hare (neighborhood_id: 63) on Saturdays.
Use the DATEPART() function to filter rides that occurred on Saturdays and join weather data based on time.
Example Query:

sql
Copy code
SELECT trips.trip_id, duration_seconds, weather_conditions
FROM trips
JOIN weather_records 
  ON trips.start_ts = weather_records.ts
WHERE pickup_location_id = 50 
  AND dropoff_location_id = 63
  AND DATEPART(dw, trips.start_ts) = 7;  -- 7 represents Saturday
Comparison of Ride Durations:

Compare ride durations on rainy Saturdays with those on other days and under other weather conditions.
How to Use This Project
Clone the Repository: Clone the repository to your local machine to access the SQL scripts and related files.

bash
Copy code
git clone https://github.com/yourusername/zuber-ride-analysis.git
SQL Execution: Run the provided SQL scripts in a SQL environment (e.g., MySQL, PostgreSQL) to replicate the analysis.

Modify Queries: Customize the queries to explore additional insights or apply them to different timeframes.

Key SQL Concepts Used
JOINs: Used to combine data from multiple tables.
Aggregations: Functions like COUNT(), SUM(), and AVG() to calculate key metrics.
Conditional Logic: Use of CASE statements for categorizing data.
Date Functions: Extract specific parts of date values (e.g., day of the week) using DATEPART().
Filtering: Use of WHERE and LIKE to filter data based on specific criteria.
Next Steps
Explore how different weather patterns (e.g., snow, wind) affect ride durations.
Analyze peak times for ride requests based on neighborhood or time of day.
Investigate pricing trends based on ride distance and weather conditions.
This README provides a clear structure for anyone working on the SQL project, guiding them through the steps, key queries, and SQL concepts used in the analysis.
