# Airline Flight Delay Analysis Using Power BI

# Project Describtion
The dataset offers comprehensive flight information, including flight dates, airline details, origin and destination airports, as well as scheduled and actual departure/arrival times. It also includes insights into delay causes, such as weather conditions, carrier-related issues, and air traffic delays. We will thoroughly analyze this data to uncover key patterns and trends, delivering actionable insights through a well-designed Power BI dashboard. The analysis will focus on identifying the primary contributors to delays, measuring airline performance, and exploring the impact of delays on overall operations, ensuring a professional and data-driven approach.

# Content 

1- Project Overview

2- DataSet Describtion

3- Tools and Technologies Used

4- Data Preparation and Transformation

5- Dimensional Tables Creation

6- Data Model

7- Analysis Process/Methodology

8- Visualization


# (1/8) Project Overview

This project analyzes flight delays using three datasets: Delayed Flights, Carrier, and Airport. The goal is to uncover key insights about flight delays, their causes, and their operational impacts. The analysis was performed using Power BI with DAX for data modeling and measures.

# (2/8) DataSet Describtion

Delayed Flights File: Contains detailed flight information, including delays and their causes.

Carrier File: Provides details about airlines.

Airport File: Lists information about airports.

# (3/8) Tools and Technologies Used

Power BI for creating interactive data visualizations and dashboards.

Power Query for data transformation.

DAX for Creating Measures, Calculated Columns, Time Intelligence Calculations, and Create dimensional tables.

# (4/8) Data Preparation and Transformation

The project began with an in-depth understanding of the datasets and relationships between the columns. The following transformations were applied:

### Date Column Creation: 

A new date column was created in the Delayed Flights dataset.

![date column creation](https://github.com/user-attachments/assets/1fe91d66-bdc4-4977-8dce-6910b3ed4041)



Handling Missing Values:

Null values were replaced with zeros for consistency.


![Replecing Null Values by zero](https://github.com/user-attachments/assets/30c8951e-a07b-467d-8bda-1af68cecf7fd)


Unknown Reasons for Delay: 

A calculated column was added to account for unknown delay reasons by assigning the value from the Arrival Delay column if the other five delay reason columns (or four) contained null or zero values.


<img width="130" alt="Unkown Delay Reasons" src="https://github.com/user-attachments/assets/f4c41191-a32b-4cdd-8020-b94ee455e84f" />



# (5/8) Dimensional Tables Creation

1. Time Dimension:

Built using DAX to include fields such as hour, minute, time of day, and a unique time key.


![Time Dim](https://github.com/user-attachments/assets/0945302e-06f4-4e07-897f-f80d167bb9bc)

2. Date Dimension:

Created using DAX to organize and structure date-related information effectively.


![Date Dim](https://github.com/user-attachments/assets/abba1476-7dd2-4aa1-bf53-7182852a716f)


3. Cancellation Reason Dimension:

Includes the cancellation code and its corresponding reason to provide detailed insights into canceled flights.



![Cancelletaion reasons](https://github.com/user-attachments/assets/fc531884-58cb-4375-a0f8-923014685b2e)




# (6/8) Data Model

We Create Star Schema

![Data Model](https://github.com/user-attachments/assets/28cacd63-b950-4cf7-8e2d-59c11c0e0289)


# (7/8) Analysis Process/Methodology

# 1. Flight Performance NPS Calculation

        
![NPS](https://github.com/user-attachments/assets/4fb3f9ef-6708-411a-a23e-27142572158c)


Key Components
1. Total Flights:
   
           Counts the total number of flights in the dataset. This value serves as the denominator for the NPS calculation.

 3. Promoters:

         Represents flights that meet the following conditions:
    
          Arrival delay is within an acceptable range (between -10 and 10 minutes).
            The flight was neither canceled nor diverted.
    
          These flights are considered "on-time" and are seen as positive contributors to performance.

  3. Detractors:

          Represents flights that negatively impact performance. These include:
            Flights that were canceled.
          Flights with an arrival delay greater than 10 minutes (excluding canceled or diverted flights).

  4. NPS Calculation:

             Computes the percentage difference between Promoters and Detractors relative to the total number of flights.
              If the denominator (TotalFlights) is zero, the DIVIDE function ensures no division errors occur, returning 0 as the result.

## Interpretation of Results
Positive NPS: Indicates a higher proportion of "on-time" flights (Promoters) compared to disrupted flights (Detractors).
Negative NPS: Suggests significant operational challenges, with more canceled or delayed flights than those arriving on time.
Zero NPS: Implies an equal number of Promoters and Detractors, reflecting a neutral flight performance.



# 2. On Time Performance Rate %

This DAX measure calculates the percentage of flights that arrived on time (within a specified range of delay) compared to the total number of flights that were neither canceled nor diverted. It provides a focused measure of punctuality for flights that successfully operated without major disruptions.

![ONTime Performance Rate](https://github.com/user-attachments/assets/1f966c20-ab7b-4e3f-9299-940c5e703f04)


1. On-Time Flights (Numerator):

           Filters and counts flights meeting the following conditions:
           Arrival delay is between 0 and 10 minutes (inclusive).
           The flight was not canceled (Cancelled = 0).
           The flight was not diverted (Diverted = 0).
           These are considered "on-time" flights.

2. Total Operated Flights (Denominator):
   
           Filters and counts flights that:
           Were not canceled (Cancelled = 0).
           Were not diverted (Diverted = 0).
           Represents all flights that were successfully operated, regardless of their punctuality.

3. On-Time Arrival Percentage:

        Divides the number of on-time flights (Numerator) by the total number of operated flights (Denominator).
        If the denominator is zero (to prevent division errors), the formula returns 0 as the result.


# 3. Peak Delay Hour

This DAX formula calculates the hour of the day when delays are at their highest, known as the Peak Delay Hour. Here’s how it works in simple terms:


![Peak Delay Hour](https://github.com/user-attachments/assets/0201d2e2-e301-42f6-b8ba-b914e559ff5d)


1. Identify the Maximum Delay:

        The formula first scans through all the hours in the DimTime table and finds the maximum value of the total delay (a measure that sums up all delays). T
        his maximum value represents the peak delay during a specific hour of the day.

2. Locate the Peak Hour:

        After identifying the maximum delay, the formula filters the time dimension (DimTime) to find the specific hour where the total delay equals this maximum value.

3. Return the Hour:

        Finally, the formula returns the hour of the day (e.g., 15 for 3 PM) that corresponds to the peak delay.


# 4. AVG Delay Weather Time 

This formula calculates the average weather delay time for flights that were successfully operated (i.e., not canceled or diverted). Here’s how it works:

![AVG Delay Weather](https://github.com/user-attachments/assets/e10ced3a-bac8-4f09-af55-3363f2795e49)


1. Focus on Weather Delays:

        The formula looks specifically at the weather delay times recorded for flights.
        
2. Exclude Non-Operated Flights:

        It filters out flights that were canceled or diverted, ensuring that only flights that actually departed and arrived are included in the calculation.

3. Calculate the Average:

        After applying the filter, it calculates the average of the weather delay times across the remaining flights.


### 5. Average Late AirCraft Delay Time, AVG Carrier Delay reasons in minutes, AVG NAS delay in minutes and AVG security reason delay

        The same aS AVG Delay Weather 

### 6. Additionally, I created several measures to enhance the insights provided by our dashboard, enabling a deeper understanding of flight performance, delay trends, and operational efficiency.



 # (8/8) Visualization

This Report describes a 7-page interactive dashboard for analyzing airline flight data from 2008, covering airline performance, airport metrics, flight details, delay reasons, and cancellations/diversions.

## 1. There is a first Page describe a summary about project.

![Summary](https://github.com/user-attachments/assets/265ca482-0380-4a54-bcc1-f36df2426929)


## 2. Airlines Analysis Page


![Airline Analysis](https://github.com/user-attachments/assets/fc79fdf8-e336-41eb-b61a-6ed0c6bc8438)

Key Insights from Airline Analysis Dashboard:

5367 planes, 23 airlines (20 active).

Mesa Airlines has highest delay rate (83%).

American & Southwest have large fleets, but on-time arrival varies.

Arrival/departure punctuality is generally aligned per airline.

Hawaiian & Aloha have lower on-time percentages.

Cancellation rates spike in December.

Overall: Dashboard compares airline performance across various metrics, revealing disparities in delays and on-time percentages, suggesting further investigation into operational factors.


  ## i. Airline Drill Through

![Airline Drill Through](https://github.com/user-attachments/assets/0e5d5121-7b7f-4590-a68c-68d1f9703dd6)

This "Drill Through" page provides a deeper dive into the "Monthly Investigation Analysis" for a specific airline, supplementing the main Airline Analysis dashboard.  Here's a breakdown:

Key Insights:

Daily Flight & Delay Volume: Shows the total flights and total delayed flights for specific days of the month (e.g., the 22nd, 1st, 18th, 13th, 26th). 

This allows for identifying days with unusually high delays or flight volumes.

Delay Reasons Breakdown: Visually represents the proportion of delays attributed to different reasons: Late Aircraft, Weather, Carrier, NAS (National Airspace System), and Unknown causes.

Average Delay Times by Reason: Displays the average delay time (in minutes) for each delay reason. This helps understand which causes lead to the longest delays.

Cancelled Flights by Reason: Indicates the number of cancellations due to each reason.


## 3. Airports Analysis Page


![Airports Analysis](https://github.com/user-attachments/assets/401f0eaa-64bc-48ef-91f9-0dddda85cd4d)

Key Insights from Airport Report:

High average delays: ~43 minutes for both departures and arrivals (8942 airports).

Significant taxi-out time: 18.23 minutes.

Regional distribution: Airports spread globally (map shown), with at least one region labeled "Pacific Ocean".

Delay causes vary by destination: Chart shows average delay times by reason (weather, carrier, etc.) for select airports.

Flight volume vs. cancellations: Chart compares these metrics for key airports (Chicago O'Hare, Atlanta, etc.), revealing potential correlations. Cancellation rates are generally low (under 0.1%).


## i. Airline Drill Through


![Airports Drill Through](https://github.com/user-attachments/assets/c9d969d2-f889-4e20-9dea-0734d92f56d6)

This airport drill-through report reveals the following:

High Volume: 5367 planes handle 2 million flights, resulting in 1 million delayed flights and 633 cancellations.

Hourly Flight Distribution: A bar chart (likely showing a 24-hour period) indicates flight volume by hour, with the highest activity around hour 17 (likely 5 PM) and lowest around hour 11 (11 AM).

Significant Delays: Average delays are shown for various reasons (aircraft, weather, carrier, NAS, security), with a particularly high average delay due to late aircraft (over 15 minutes).

Taxi Times: Average taxi-out and taxi-in times are displayed, with taxi-out slightly higher than taxi-in.

In short: This airport experiences high flight volume, substantial delays (especially due to late aircraft), and exhibits a typical daily flight pattern with a late afternoon peak.




## 4. Flights Analysis Page


![Fleights Analysis](https://github.com/user-attachments/assets/cebe29df-156b-453b-b814-b1eb67eb76a4)


This flight analysis report highlights the following:

High Volume, Low Cancellations: 2 million flights flown with only 633 cancellations (0.03%), despite 7754 diversions.

Negative NPS: A Flight Performance NPS of -90.88 suggests significant customer dissatisfaction.

Peak Flight Times: Busiest flight times are in the late afternoon/evening (5-8 PM), with a lull mid-morning (10-11 AM).

Weekday Dominance: Weekdays account for the majority of flights (73.7%).

On-Time Performance Varies: On-time arrival percentage fluctuates throughout the day and is shown for specific destinations (DEN, LAX, DFW, ATL, ORD), alongside flight volume.

Delays by Cause: Average delay times are broken down by cause (aircraft, weather, NAS, security, unknown), with a wide range in duration.

Cancellation Trend: A line chart shows cancellation rates by month, indicating a recent spike (potentially in November/December).

In short:  Despite high volume and low cancellations, customer satisfaction is a major concern. The report provides detailed insights into flight patterns, delays, and cancellations, allowing for deeper analysis and potential problem identification.



## 5. Delays Analysis Page

![Delays Analysis](https://github.com/user-attachments/assets/b0bac7ea-ce83-465f-ab34-73c89305d5ea)

This "Delay Reasons Analysis" report reveals:

High Volume of Delays: 1 million delayed flights.

Late Aircraft is Major Cause: Average late aircraft delay is 16.29 minutes, significantly higher than other causes (weather 2.4 min, NAS 9.72 min, carrier 12.41 min).

Peak Delay Hour: 5 PM (hour 17) sees the most delays.

Delay Rate by Airline: Southwest has a 72% delay rate, followed by other airlines (specific values unclear).

Early Arrival Rate: Low early arrival rate of ≥9.23%.

On-Time Arrival Percentage: Very low at 18.93%.

Delays by Tail Number: Specific planes (tail numbers) are associated with varying delay counts.

Delays by Day of Week: Friday and Monday show the highest total delay volume.

Delays Over Time: Charts show delay trends by hour, tail number, day of week, and month, with late aircraft delays consistently high.

In short:  Late aircraft are the primary driver of delays, impacting a large portion of flights and resulting in poor on-time performance.  The report identifies specific pain points (peak hours, days of week, tail numbers) for potential intervention.


## 6. Cancellation & Diverted Analysis Page


![Cancellation   Diverted](https://github.com/user-attachments/assets/f09b0a33-d643-4fa8-ae9c-38356379cddd)

This "Cancellation and Diverted Flights Analysis" report shows:

Low Cancellation Rate: Only 0.03% of flights were cancelled (633 out of 2 million flown).

Significant Diversions: A high number of flights were diverted (7754).

Cancellation Reasons: Cancellations were due to NAS (80 flights), airlines (246 flights), and weather (307 flights).

Weekend Impact: More flights were cancelled on weekends (462) than weekdays (171).

Cancellation Trend: A recent spike in cancellations occurred, likely in November or December.

Diversions by Airline: Specific carriers experienced varying levels of diversions.

Cancellation Hotspots: Charts show cancellations by reason and by destination airport, highlighting specific airports and causes with higher cancellation rates.

In short: Despite a very low cancellation rate overall, a significant number of flights were diverted, and specific periods, causes, and locations experienced more cancellations than others.




# Work Environment & Contributors

### Trello  Work Environment:

. [Trello  Work Environment](https://trello.com/b/tS6xTfZg/airline-delay-analysis-prject)


This project was collaboratively managed using Trello, ensuring efficient task tracking, sprint planning, and progress monitoring. Trello facilitated clear communication and assignment of responsibilities among the team members, allowing seamless coordination and timely completion of deliverables. The development team consisted of:

## Contributors:

1- Khalid Sabry Elshafei

2- Nada Mostafa Aglan

3- Dina Ibrahim Hemdan

Each team member played a critical role in achieving the project's objectives, leveraging Trello to stay aligned on priorities and updates throughout the development lifecycle.



