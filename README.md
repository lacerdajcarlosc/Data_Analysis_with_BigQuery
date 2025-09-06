
# **README.md** — Data Analysis with BigQuery

## **📌 Overview**
This project performs **extraction, transformation, and analysis of data** from the public dataset **Chicago Taxi Trips** available in **Google BigQuery**.

The goal is to **query, process, and save the data** into CSV files for further analysis, dashboard creation, and reporting.

---

## **📂 Project Structure**
```
.
├── generate_csvs.py          # Main script for querying and generating CSVs
├── data/                     # Folder where CSV files are saved
│   ├── travells_per_year.csv     # Total trips per year
│   ├── hour_weekday.csv         # Number of trips per hour and weekday
│   └── taxi_trips_sample.csv    # Sample of 5000 trips for analysis
├── README.md                # Project documentation
```

---

## **🛠️ Technologies Used**
- **Python 3.10+**
- **Google BigQuery** → Data querying
- **Pandas** → Data manipulation and export
- **Google Cloud SDK** → Authentication for BigQuery

---

## **📥 Prerequisites**

### **1. Create a project in Google Cloud**
- Go to [https://console.cloud.google.com](https://console.cloud.google.com)
- Create a new project
- Enable the **BigQuery API**

### **2. Configure authentication**
- Generate a **service account key** in Google Cloud:
  - Go to **IAM & Admin → Service Accounts**
  - Click **Create Key**
  - Choose **JSON**
  - Download the file.

- Set the environment variable:
```bash
export GOOGLE_APPLICATION_CREDENTIALS="path/to/your_key.json"
```

On Windows (PowerShell):
```powershell
setx GOOGLE_APPLICATION_CREDENTIALS "C:\path\to\your_key.json"
```

---

## **⚡ How to Run the Project**

### **1. Create a virtual environment**
```bash
python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate       # Windows
```

### **2. Install dependencies**
```bash
pip install --upgrade pip
pip install google-cloud-bigquery pandas
```

### **3. Run the script**
```bash
python generate_csvs.py
```

---

## **📊 Script Functionalities**
The **generate_csvs.py** script runs three main queries:

### **1. Total trips per year**
```sql
SELECT 
    EXTRACT(YEAR FROM trip_start_timestamp) AS year,
    COUNT(*) AS num_trips
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
GROUP BY year
ORDER BY year;
```
📌 Saved to: `data/travells_per_year.csv`

---

### **2. Trips per hour and weekday**
```sql
SELECT 
    EXTRACT(HOUR FROM trip_start_timestamp) AS hour,
    EXTRACT(DAYOFWEEK FROM trip_start_timestamp) AS weekday,
    COUNT(*) AS num_trips
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE trip_start_timestamp >= '2019-01-01'
GROUP BY hour, weekday
ORDER BY weekday, hour;
```
📌 Saved to: `data/hour_weekday.csv`

---

### **3. Sample of 5000 trips**
```sql
SELECT 
    trip_start_timestamp,
    trip_miles,
    fare
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE fare IS NOT NULL
    AND trip_miles IS NOT NULL
LIMIT 5000;
```
📌 Saved to: `data/taxi_trips_sample.csv`

---

## **📂 Expected Output**
After running the script, the `data/` folder will be created with the CSV files:

```
data/
├── travells_per_year.csv
├── hour_weekday.csv
└── taxi_trips_sample.csv
```

---

## **🚀 Next Steps**
- Create exploratory charts using **Matplotlib** and **Seaborn**
- Develop an **interactive dashboard** with **Plotly Dash**
- Generate automatic **PDF reports**

---

## **👨‍💻 Author**
**Carlos Lacerda**  

