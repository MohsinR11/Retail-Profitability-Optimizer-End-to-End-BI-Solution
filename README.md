Project Overview
This project identifies "Profit Leaks" in a $2M retail business. While many dashboards focus solely on Revenue, this solution deep-dives into Unit Economics to uncover why certain products and shipping routes are destroying the company's bottom line.

Business Problem
The Symptom: Record-high Gross Revenue ($2M) but stagnant Net Profit.

The Goal: Pinpoint "Profit Bleeders" (products or logistics routes with negative margins) and provide actionable recommendations for a Founder/CFO.

The Tech Stack
Python: Simulated a "messy" raw dataset of 10,000+ transactions including hidden costs like Shipping Distance (KM) and Return Losses.

SQL: Performed ETL (Extract, Transform, Load) to clean data-entry errors and pre-calculate transaction-level Net Profit.

Power BI (DAX): Developed a high-impact "Executive Dark Mode" dashboard featuring Financial Bridges and Root-Cause Analysis.

Data Engineering Layer (SQL)
Before visualization, I used SQL to ensure data integrity and shift heavy calculations away from the dashboard layer for better performance.

Key Transformations:

Error Handling: Rectified system glitches where Gross_Sales was recorded as -99.

Missing Value Imputation: Handled NULL marketing spend values to ensure accurate ROI tracking.

Metric Engineering: Calculated Net Profit = Gross_Sales - (COGS + Shipping + Marketing + Refunds).

Executive Insights (The "Aha!" Moments)
1. The Financial Bridge (Waterfall Chart)
Revealed that Shipping Costs and Refund Losses are consuming 18% of Gross Revenue. This is the primary driver of margin erosion.

2. Logistics Break-Even Analysis (Scatter Plot)
Discovered a critical threshold: Furniture items shipped over 1,200 KM frequently result in a Net Loss. The weight-to-distance ratio makes these orders "Wealth Destroyers."

3. Root Cause Analysis (Decomposition Tree)
Identified that Bookshelves have a 15% higher return rate than any other category, leading to "double-shipping" costs that wipe out all profit for those units.

Strategic Recommendations for Founders
Dynamic Shipping Surcharge: Implement a distance-based "Heavy Freight" fee for Furniture orders exceeding 1,200 KM.

Return Policy Pivot: For low-value items (under $20), switch to a "Returnless Refund" model to save $15+ in return logistics costs per unit.

Inventory Re-allocation: Shift 10% of the marketing budget from high-return Furniture to high-margin Electronics.

How to Run
Run data_generator.py to create the raw CSV.

Execute transformation.sql in your SQL environment (or view the logic in the SQL folder).

Open Profitability_Optimizer.pbix to explore the interactive dashboard.
