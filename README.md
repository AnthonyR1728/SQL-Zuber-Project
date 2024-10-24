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

## Project Steps

# Step 1: Exploratory Data Analysis

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

     - Find the number of rides for these two companies and name the resulting variable trips_amount.
     - Join the rides for all other companies in the group "Other." Group the data by taxi company names.
     - Name the field with taxi company names company. Sort the result in descending order by trips_amount.
  
Example Query:


# Step 2: Analyze Ride Duration Based on Weather Conditions

  4. Retrieve the identifiers of the O'Hare and Loop neighborhoods  from the neighborhoods table.

Example Query:

  
  5. For each hour, retrieve the weather condition records from the weather_records table.

     - Using the CASE operator, break all hours into two groups: Bad if the description field contains the words rain or storm, and Good for others.
     - Name the resulting field weather_conditions.
     - The final table must include two fields: date and hour (ts) and weather_conditions.

Example Query:


  6. Retrieve from the trips table all the rides that started in the Loop (pickup_location_id: 50) on a Saturday and ended at O'Hare (dropoff_location_id: 63).

     - Get the weather conditions for each ride.
     - Retrieve the duration of each ride.
     - Ignore rides for which data on weather conditions is not available.

      The table columns should be in the following order:

        A. start_ts
        B. weather_conditions
        C. duration_seconds

     - Sort by trip_id.

Example Query:






Key SQL Concepts Used:
  - JOINs: Used to combine data from multiple tables.
  - Aggregations: Functions like COUNT(), SUM(), and AVG() to calculate key metrics.
  - Conditional Logic: Use of CASE statements for categorizing data.
  - Date Functions: Extract specific parts of date values (e.g., day of the week) using DATEPART().
  - Filtering: Use of WHERE and LIKE to filter data based on specific criteria.
