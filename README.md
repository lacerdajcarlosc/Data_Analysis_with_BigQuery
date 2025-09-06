Data Analysis with BigQuery

📌 Overview
This project focuses on the extraction, transformation, and analysis of data from the public dataset Chicago Taxi Trips available on Google BigQuery.

The main goal is to query, process, and save the data into CSV files for further analysis, such as creating dashboards and reports.

📂 Project Structure
.
├── generate_csvs.py          # Main script for querying and generating CSVs
├── data/                     # Folder where CSV files will be saved
│   ├── travells_per_year.csv     # Total number of trips per year
│   ├── hour_weekday.csv         # Number of trips by hour and weekday
│   └── taxi_trips_sample.csv    # A sample of 5000 trips for analysis
├── README.md                # Project documentation
🛠️ Technologies Used
Python 3.10+

Google BigQuery → Data querying

Pandas → Data manipulation and export

Google Cloud SDK → BigQuery authentication

📥 Prerequisites
Create a Google Cloud Project

Go to https://console.cloud.google.com

Create a new project.

Enable the BigQuery API.

Configure Authentication

Generate a service account key in Google Cloud:

Go to IAM & Admin → Service Accounts.

Click Create Key.

Choose JSON.

Download the file.

Set up the environment variable:

Linux/Mac: export GOOGLE_APPLICATION_CREDENTIALS="path/to/your_key.json"

Windows (PowerShell): setx GOOGLE_APPLICATION_CREDS "C:\path\to\your_key.json"

⚡ How to Run the Project
Create a Virtual Environment

python -m venv venv

source venv/bin/activate      # Linux/Mac

venv\Scripts\activate         # Windows

Install Dependencies

pip install --upgrade pip

pip install google-cloud-bigquery pandas

Run the Script

python generate_csvs.py

📊 Script Functionalities
The generate_csvs.py script executes three main queries:

Total trips per year

SQL

SELECT 
    EXTRACT(YEAR FROM trip_start_timestamp) AS year,
    COUNT(*) AS num_trips
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
GROUP BY year
ORDER BY year;
📌 Saved to: data/travells_per_year.csv

Trips by hour and weekday

SQL

SELECT 
    EXTRACT(HOUR FROM trip_start_timestamp) AS hour,
    EXTRACT(DAYOFWEEK FROM trip_start_timestamp) AS weekday,
    COUNT(*) AS num_trips
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE trip_start_timestamp >= '2019-01-01'
GROUP BY hour, weekday
ORDER BY weekday, hour;
📌 Saved to: data/hour_weekday.csv

Sample of 5000 trips

SQL

SELECT 
    trip_start_timestamp,
    trip_miles,
    fare
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE fare IS NOT NULL
    AND trip_miles IS NOT NULL
LIMIT 5000;
📌 Saved to: data/taxi_trips_sample.csv

📂 Expected Output
After running the script, the data/ folder will be created with the following CSV files:

data/
├── travells_per_year.csv
├── hour_weekday.csv
└── taxi_trips_sample.csv
🚀 Next Steps
Create exploratory plots using Matplotlib and Seaborn.

Develop an interactive dashboard with Plotly Dash.

Generate automated reports in PDF format.

👨‍💻 Author
Carlos Lacerda