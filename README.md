# uber-trip-analysis

## 📌 Project Objective

The goal of this project is to analyze Uber trip data to extract meaningful insights related to **bookings, revenue, trip patterns, and location preferences**, enabling stakeholders to make data-driven decisions about **driver allocation, pricing strategies, and customer engagement**.

## ⚙ Data Modeling & Relationships
- Built a Calendar Table for time intelligence.
- Created relationships:

  `Trip Details[Pickup Date] → Calendar[Date]` (active)
  
  `Trip Details[Drop-off Date] → Calendar[Date]` (inactive, activated using USERELATIONSHIP)
```
Calendar Table = 
CALENDAR(MIN('Trip Details'[Pickup Date]), MAX('Trip Details'[Pickup Date]))
```
## 📊 Dashboards

1️⃣ **Overview Dashboard**

- KPIs: Total Bookings, Total Revenue, Avg Fare, Total Distance, Avg Distance, Avg Trip Time
- Visuals: Donut charts (Payment Type, Day vs Night trips), Matrix (Vehicle Type comparison), Card visuals (Frequent Pickup/Drop-off, Farthest Trip)

```
Total Bookings = COUNT('Trip Details'[Trip ID])

Total Revenue = SUM('Trip Details'[Fare_Amount])

Avg Trip Distance = AVERAGE('Trip Details'[Trip_Distance])

Trip Type (Day/Night) =
IF(
   HOUR('Trip Details'[Pickup Time]) >= 17 || HOUR('Trip Details'[Pickup Time]) < 6,
   "Night Trip",
   "Day Trip"
)
```

## 2️⃣ Time Analysis Dashboard

- **Area Chart** → Bookings by Pickup Time (10-min intervals)
- **Line Chart** → Weekday vs Weekend trends
- **Heatmap** → Hourly booking density across weekdays

```
Bookings by Hour = 
CALCULATE(
    COUNT('Trip Details'[Trip ID]),
    GROUPBY('Trip Details'[Pickup Hour])
)
```

## 3️⃣ Trip Details (Drill-through Tab)
- Full trip-level details: Trip ID, Vehicle, Pickup/Drop-off Location, Payment Mode, Distance, Fare
- Drill-through → From any visual into specific trip details
- Bookmark toggle → Switch between summary and detail view
_____________________________________________________________________________________________________________________________________________________________________________________________
## 🔍 Key Insights

✔ Night trips contributed ~40% of revenue but had fewer drivers → Driver allocation gap

✔ Sundays showed the highest demand, Fridays the lowest → Staffing & promotions adjustment

✔ Wallet payments had highest Avg Fare → Premium customer segment

✔ Top 5 locations contributed ~60% of total trips → Geo-focused strategies

## 💡 Business Impact
- Helped optimize driver distribution in high-demand zones
- Improved pricing model decisions during peak times
- Identified high-value customer segments based on payment behavior
- Supported marketing campaigns targeting low-demand days
