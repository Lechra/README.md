# Austin Bikeshare Analysis: Longest Used Bike

## 📘 Project Overview
This project analyzes the **Austin Bikeshare** dataset from Google BigQuery to identify the **bike with the highest total usage time**. Using SQL, we calculate total trip duration per bike, determine the longest-used bike, and explore the first 10 trips associated with that bike.

This project demonstrates skills in:
- Writing clean and modular SQL using CTEs
- Aggregating and analyzing large public datasets
- Performing joins between temporary results and main tables
- Presenting results clearly for stakeholders

---

## 🧩 Step 1: Create a CTE to Find the Longest‑Used Bike
We begin by calculating total trip duration for every bike.

```sql
WITH longest_used_bike AS (
  SELECT
    bike_id,
    SUM(duration_minutes) AS bike_trip_duration
  FROM
    `bigquery-public-data.austin_bikeshare.bikeshare_trips`
  GROUP BY bike_id
  ORDER BY bike_trip_duration DESC
  LIMIT 1
)
```

### ✅ Result
- **bike_id:** 370  
- **bike_trip_duration:** 137,641 minutes

This identifies **Bike 370** as the most-used bike in the dataset.

---

## 🧩 Step 2: Join the CTE Back to the Main Table
Now we retrieve the first 10 trips taken by bike 370.

```sql
-- Retrieve the first 10 trips for the longest-used bike
SELECT *
FROM `bigquery-public-data.austin_bikeshare.bikeshare_trips`
WHERE bike_id = 370
ORDER BY start_time
LIMIT 10;
```

---

## 📊 Sample Results (First 10 Trips for Bike 370)
Below is a sample of the first 10 trips associated with this bike.

| Row | trip_id | subscriber_type        | bike_id | bike_type | start_time               | start_station_id | start_station_name                     | end_station_id | end_station_name                     | duration_minutes |
|-----|----------|-------------------------|---------|-----------|---------------------------|-------------------|-----------------------------------------|-----------------|---------------------------------------|------------------|
| 1   | 15189390 | Local365               | 370     | classic   | 2017-06-22 13:18:54 UTC  | 2563              | Davis at Rainey Street                 | 3291            | 11th & San Jacinto                   | 39               |
| 2   | 7288365  | 24 Hour Walk Up Pass   | 370     | classic   | 2015-10-19 12:38:24 UTC  | 2497              | 11th/Congress @ The Texas Capitol      | 2497            | 11th/Congress @ The Texas Capitol    | 10               |
| 3   | 6463167  | 24 Hour Walk Up Pass   | 370     | classic   | 2015-08-29 16:14:31 UTC  | 2497              | 11th/Congress @ The Texas Capitol      | 2497            | 11th/Congress @ The Texas Capitol    | 67               |
| 4   | 5513278  | 24 Hour Walk Up Pass   | 370     | classic   | 2015-06-28 14:07:25 UTC  | 2497              | 11th/Congress @ The Texas Capitol      | 2497            | 11th/Congress @ The Texas Capitol    | 37               |
| 5   | 4107388  | 24 Hour Walk Up Pass   | 370     | classic   | 2015-03-13 17:09:02 UTC  | 2497              | 11th/Congress @ The Texas Capitol      | 2497            | 11th/Congress @ The Texas Capitol    | 21               |
| 6   | 5737210  | 24 Hour Walk Up Pass   | 370     | classic   | 2015-07-13 14:24:00 UTC  | 2494              | 2nd/Congress                           | 2497            | 11th/Congress @ The Texas Capitol    | 10               |
| 7   | 4363388  | 24 Hour Walk Up Pass   | 370     | classic   | 2015-04-04 16:21:07 UTC  | 2501              | 5th/Bowie                              | 2497            | 11th/Congress @ The Texas Capitol    | 14               |
| 8   | 4107119  | 24 Hour Walk Up Pass   | 370     | classic   | 2015-03-13 16:52:38 UTC  | 2496              | 8th/Congress                           | 2497            | 11th/Congress @ The Texas Capitol    | 15               |
| 9   | 4105214  | 24 Hour Walk Up Pass   | 370     | classic   | 2015-03-13 15:19:20 UTC  | 2496              | 8th/Congress                           | 2497            | 11th/Congress @ The Texas Capitol    | 3                |
| 10  | 3308814  | 24 Hour Walk Up Pass   | 370     | classic   | 2014-09-22 00:14:15 UTC  | 2711              | Barton Springs/Kinney                  | 2497            | 11th/Congress @ The Texas Capitol    | 110              |

---

## 🧠 Key Insights
- **Bike 370** was used for **137,641 total minutes**, making it the most-used bike in the Austin Bikeshare system.
- Many of its trips began or ended at **11th/Congress @ The Texas Capitol**, suggesting it was heavily used in the downtown corridor.
- Trip durations varied significantly, ranging from **3 minutes** to **110 minutes** within the first 10 trips alone.

---

## 📌 Conclusion
This project demonstrates how SQL can be used to:
- Aggregate and analyze public transportation data
- Identify high-usage assets
- Join intermediate results back to a main dataset for deeper insights

This type of analysis is useful for fleet optimization, maintenance planning, and improving service coverage.

---





