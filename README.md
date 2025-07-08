# DrivePro AutoHouse Vehicle Sales Analysis  
**Timeframe:** December 2014 – July 2015  
**Tools Used:** Power BI, Power Query, DAX, Star Schema Modeling

---

## Project Background

DrivePro AutoHouse is a national car dealership specializing in selling a wide variety of vehicles across the United States. In this project, I partnered with the Head of Operations to extract insights from historical sales data and deliver data-driven recommendations to improve the company’s vehicle inventory strategy.

The goal was to identify high-performing vehicle types, understand regional and seasonal sales trends, and uncover pricing dynamics — enabling DrivePro to make smarter, faster decisions about which vehicles to stock, where to allocate them, and how to price them in a highly competitive market.

---

## Executive Summary

This report analyzes over 540,000 used and new vehicle transactions across the U.S. between December 2014 and July 2015. Using a clean star-schema model, interactive DAX measures, and visual storytelling, the Power BI dashboard delivers insights into inventory trends, price performance, and consumer preferences.

The top 5 makes were consistently dominant over the analysis period, while state-by-state performance and mileage brackets revealed clear segmentation opportunities. Patterns in vehicle color and seasonal demand offer further inventory and marketing optimization opportunities.

<img width="991" height="637" alt="Image" src="https://github.com/user-attachments/assets/c3e6c7d7-33d9-43c7-a5f9-e2bcd1148c1f" />

---

## Insights Deep-Dive

### Sales Trends

- **Ford, Chevrolet, Nissan, Toyota, and BMW** consistently led in total sales volume.
- Sales **spiked in January and February 2015**, likely due to seasonal demand, tax refunds, and dealership incentives.
- Vehicles with **under 50,000 miles** commanded significantly higher average prices.
- **Luxury vehicles** such as Aston Martin and Hummer sold above market value (MMR), while brands like **Tesla** often sold closer to or below MMR.
- The **top five most-sold makes** showed selling prices closely aligned with MMR, indicating effective pricing strategies.
- **Florida, California, and Pennsylvania** recorded the highest total sales during the analysis period.
- **Black, white, and silver** were the most commonly sold vehicle colors.

---

<img width="800" height="500" alt="Image" src="https://github.com/user-attachments/assets/411815c3-cbfd-4486-9485-78c39ea4598c" />

---

<img width="500" height="500" alt="Image" src="https://github.com/user-attachments/assets/d8dba6b9-5f16-42ab-8e8a-1e428b0a5b00" />

---

<img width="350" height="400" alt="Image" src="https://github.com/user-attachments/assets/06d75475-936d-4983-a939-2d7cf8b728e3" />

---

<img width="350" height="400" alt="Image" src="https://github.com/user-attachments/assets/2f125c0f-8c63-4392-bc0c-b4f9b709aa7a" /> 

---

## Recommendations

- **Source What Sells:** Focus on the top 5 makes and most popular colors for inventory planning.
- **Geo-Targeted Distribution:** Align stock delivery with states showing the highest demand.
- **Mileage Strategy:** Prioritize vehicles with under 50,000 miles to maximize profit margins.
- **Seasonal Forecasting:** Time marketing and promotional efforts at the beginning of the year to align with demand spikes.
- **Inventory Control:** Avoid makes and models that consistently underperform relative to market value.

---

## Considerations & Limitations

- The dataset only includes sales from **December 2014 to July 2015**.
- **MMR** is used as a benchmark; it is assumed accurate per vehicle at the time of sale but may vary regionally or seasonally.

---

## Technical Factors

### Data Model Design

A **star schema** model was used with a central fact table and multiple supporting dimension tables to enable clean, efficient filtering and drill-down functionality in Power BI.

### Data Cleaning Process (Power Query)

- Removed duplicates using the `vin` field
- Standardized text formatting (e.g., "Ford" vs. "FORD")
- Removed records from outside the U.S.
- Created `ParsedSaleDate` for accurate time-based analysis
- Built `MakeModelID` by concatenating cleaned `make`, `model`, `trim`, and `body` fields

### Key DAX Measures

```dax
Sales Count = COUNTROWS(car_prices)

Average Price = AVERAGE(car_prices[sellingprice])

Price Delta = car_prices[sellingprice] - car_prices[mmr]

OdometerBracket =
SWITCH(TRUE(),
  car_prices[odometer] <= 20000, "<= 20k",
  car_prices[odometer] <= 50000, "20k - 50k",
  car_prices[odometer] <= 100000, "50k - 100k",
  car_prices[odometer] <= 150000, "100k - 150k",
  "> 150k"
)
