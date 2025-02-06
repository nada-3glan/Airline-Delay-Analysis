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






