# 🚕 Ola Data Analyst Project – Power BI & SQL

## 📌 Project Overview

This project simulates an Ola ride-sharing data analysis using synthetic data (~100,000 rows and 18 columns). It involves extensive data cleaning, transformation, and visualization using Power BI, as well as business queries using SQL.

### 🔧 Tools & Technologies
- **Power BI** (for visualization)
- **SQL** (for data querying and analysis)
- **Excel** (for initial dataset generation and cleaning)
- **ChatGPT** (used for synthetic data generation)

---

## 📊 Power BI Dashboard

Created a **5-page interactive dashboard** including:
1. **Ride Volume Over Time**
2. **Booking Status Breakdown**
3. **Top 5 Vehicle Types by Ride Distance**
4. **Average Customer Ratings by Vehicle Type**
5. **Cancelled Rides Analysis**
6. **Top 5 Customers by Total Booking Value**
7. **Ride Distance Distribution Per Day**
8. **Driver Ratings Distribution**
9. **Customer vs. Driver Ratings**


---

## 🧮 SQL Business Questions

```sql
-- 1. Retrieve all successful bookings:
SELECT * FROM bookings WHERE status = 'Successful';

-- 2. Find the average ride distance for each vehicle type:
SELECT vehicle_type, AVG(ride_distance) AS avg_distance
FROM bookings
GROUP BY vehicle_type;

-- 3. Get the total number of cancelled rides by customers:
SELECT COUNT(*) AS cancelled_by_customer
FROM bookings
WHERE status = 'Cancelled' AND cancel_reason_by = 'Customer';

-- 4. List the top 5 customers who booked the highest number of rides:
SELECT customer_id, COUNT(*) AS total_rides
FROM bookings
GROUP BY customer_id
ORDER BY total_rides DESC
LIMIT 5;

-- 5. Get the number of rides cancelled by drivers due to personal and car-related issues:
SELECT cancel_reason, COUNT(*) AS count
FROM bookings
WHERE status = 'Cancelled' AND cancel_reason_by = 'Driver'
AND cancel_reason IN ('Personal', 'Car Issue')
GROUP BY cancel_reason;

-- 6. Find the maximum and minimum driver ratings for Prime Sedan bookings:
SELECT MAX(driver_rating) AS max_rating, MIN(driver_rating) AS min_rating
FROM bookings
WHERE vehicle_type = 'Prime Sedan';

-- 7. Retrieve all rides where payment was made using UPI:
SELECT * FROM bookings WHERE payment_method = 'UPI';

-- 8. Find the average customer rating per vehicle type:
SELECT vehicle_type, AVG(customer_rating) AS avg_rating
FROM bookings
GROUP BY vehicle_type;

-- 9. Calculate the total booking value of rides completed successfully:
SELECT SUM(booking_value) AS total_value
FROM bookings
WHERE status = 'Successful';

-- 10. List all incomplete rides along with the reason:
SELECT booking_id, status, cancel_reason
FROM bookings
WHERE status != 'Successful';
