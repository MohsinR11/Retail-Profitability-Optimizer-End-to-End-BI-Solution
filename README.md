"Revenue is vanity, but Profit is sanity." 💸This project is designed for Founders and Executive Leadership to uncover why a company generating $2.0M in Gross Revenue is suffering from stagnant growth. I have deep-dived into Unit Economics to identify "Wealth Destroyers."### 📌 1. Executive SummaryPrimary Objective: Identify "Profit Leaks" across 10,000+ transactions.Core Insight: Revealed that 18% of potential profit was being consumed by unoptimized shipping routes and high return rates.Target Audience: Founders, CFOs, and Senior Operations Managers.### 🛠 2. The Tech Stack# SQL: Used for ETL (Extract, Transform, Load) and cleaning transaction-level errors.# Power BI: Built an Executive Dark Mode dashboard with DAX-driven business logic.# Python: Generated a "messy" realistic dataset with hidden costs (Marketing Spend, Shipping Distance).# Business Analysis: Focused on Net Profit Margin and Return-on-Ad-Spend (ROAS).### ⚙️ 3. Data Engineering Layer (SQL)Founders value clean data. I used the following SQL logic to transform raw logs into "Business-Ready" insights:SQL/* TRANSFORMATION HIGHLIGHTS:
   * Fixed -99 System Glitches
   * Imputed NULL Marketing Spend
   * Calculated Transactional Net Profit 
*/

WITH CleanedData AS (
    SELECT 
        Order_ID,
        Product,
        Category,
        -- **Fixing Data Entry Errors**
        CASE 
            WHEN Gross_Sales_USD = -99 THEN (Unit_Price_USD * Quantity_Units) 
            ELSE Gross_Sales_USD 
        END AS Gross_Sales_USD,
        COGS_USD,
        Shipping_Cost_USD,
        -- **Standardizing Marketing Attribution**
        COALESCE(Marketing_Spend_USD, 0) AS Marketing_Spend_USD,
        Refund_Loss_USD
    FROM raw_retail_data
)
SELECT 
    *,
    -- **The "Money Maker" Metric**
    (Gross_Sales_USD - (COGS_USD + Shipping_Cost_USD + Marketing_Spend_USD + Refund_Loss_USD)) AS Net_Profit_USD
FROM CleanedData;
### 📊 4. Key Performance Indicators (KPIs)MetricDefinitionBusiness ImpactGross Revenue$2.0MTotal market footprint.Net Profit$398KActual cash retained after all costs.Profit Margin22.18%The efficiency of current operations.### 💡 5. Strategic Insights & "Aha!" Moments# The Financial Bridge (Waterfall Chart):Discovery: Logistics and Refunds are the biggest "Margin Killers."Highlight: While Marketing gets the blame, Shipping Costs eat more profit.# Logistics Efficiency (Scatter Plot):Discovery: Furniture shipped over 1,200 KM is non-profitable.Highlight: Every mile beyond this threshold destroys company value.# Root Cause (Decomposition Tree):Discovery: Bookshelves suffer from a 15% higher return rate.Highlight: High returns create a "Double Shipping" cost that wipes out profits.### 🚀 6. Actionable Recommendations**Dynamic Shipping: Implement a "Distance Surcharge" for orders over 1,200 KM.**Returnless Refunds: For items under $20, stop paying for return shipping; let the customer keep the item.**Budget Pivot: Re-allocate 10% of spend from Furniture to Electronics to maximize ROI.### 📈 7. Connect & CollaborateLinkedIn: [Insert Your Profile Link]Portfolio: [Insert Link to Power BI Web Report]Status: Seeking Data Analyst / Business Intelligence Roles.
