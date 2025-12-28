📌 Executive Summary
This project identifies "Profit Leaks" in a $2M retail business. While many dashboards focus solely on Revenue, this solution deep-dives into Unit Economics to uncover why certain products and shipping routes are destroying the company's bottom line.

📂 Table of Contents
Business Problem

The Tech Stack

Data Engineering Layer (SQL)

Executive Insights

Strategic Recommendations

🎯 Business Problem
The Symptom: Record-high Gross Revenue ($2M) but stagnant Net Profit.

The Challenge: High-volume sales are masking "Wealth Destroyers"—transactions that cost more to fulfill than they generate in revenue.

The Goal: Pinpoint "Profit Bleeders" and provide actionable recommendations for a Founder/CFO to increase the Net Profit Margin.

🛠 The Tech Stack
Python: Simulated a "messy" raw dataset of 10,000+ transactions with hidden variables (Shipping Distance, Return Probabilities).

SQL: Conducted ETL to resolve data-entry errors and pre-calculate transaction-level Net Profit.

Power BI (DAX): Developed a high-impact "Executive Dark Mode" dashboard for strategic decision-making.

⚙️ Data Engineering Layer (SQL)
Before visualization, I used SQL to ensure data integrity and shift heavy calculations away from the dashboard layer to optimize performance.

SQL

/* Cleaning & Metric Engineering
   Handling -99 errors and NULL values 
*/
WITH CleanedData AS (
    SELECT 
        Order_ID,
        Date,
        Product,
        Category,
        Quantity_Units,
        CASE 
            WHEN Gross_Sales_USD = -99 THEN (Unit_Price_USD * Quantity_Units) 
            ELSE Gross_Sales_USD 
        END AS Gross_Sales_USD,
        COGS_USD,
        Shipping_Cost_USD,
        COALESCE(Marketing_Spend_USD, 0) AS Marketing_Spend_USD,
        Is_Returned,
        Refund_Loss_USD
    FROM raw_retail_data
)
SELECT 
    *,
    (COGS_USD + Shipping_Cost_USD + Marketing_Spend_USD + Refund_Loss_USD) AS Total_Expenses_USD,
    (Gross_Sales_USD - (COGS_USD + Shipping_Cost_USD + Marketing_Spend_USD + Refund_Loss_USD)) AS Net_Profit_USD
FROM CleanedData;
📊 Executive Insights
1. The Financial Bridge (Waterfall Chart)
Insight: Revealed that Shipping Costs and Refund Losses consume 18% of Gross Revenue.

Impact: This is the primary driver of margin erosion, proving that "Sales" does not equal "Success."

2. Logistics Break-Even Analysis (Scatter Plot)
Insight: Discovered a critical threshold: Furniture items shipped over 1,200 KM frequently result in a Net Loss.

Impact: The weight-to-distance ratio makes long-haul furniture shipping unsustainable under the current pricing model.

3. Root Cause Analysis (Decomposition Tree)
Insight: Identified that Bookshelves have a 15% higher return rate than any other category.

Impact: "Double-shipping" costs (Initial + Return) wipe out the profit margin for 1 out of every 6 units sold in this category.

💡 Strategic Recommendations
✅ Dynamic Shipping Surcharge: Implement a distance-based "Heavy Freight" fee for Furniture orders exceeding 1,200 KM.

✅ Return Policy Pivot: For low-value items (under $20), switch to a "Returnless Refund" model to save ~$15 in logistics costs per unit.

✅ Marketing Re-allocation: Shift 10% of the marketing budget from high-return/low-margin Furniture to high-margin/low-return Electronics.

🚀 How to Use
Clone the repo: git clone https://github.com/your-username/profitability-optimizer.git

Generate Data: Run python data_generator.py to create the messy CSV.

View SQL Logic: Check the /sql folder for the transformation script.

Open Dashboard: Launch Profitability_Optimizer.pbix in Power BI Desktop.
