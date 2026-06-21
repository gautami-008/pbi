# PBI

Maven Market Business Intelligence Project📋 
  
   1.Business Problem
   
Maven Market is a multinational retail grocery chain operating across multiple countries (primarily the United States, Mexico, and Canada). Management faced significant visibility gaps due to isolated data silos, making it difficult to track overarching performance efficiently.

   
   2.Key Challenges:
   
1.Fragmented Reporting: Executive leadership lacked a single source of truth to monitor regional sales trends, store-level efficiency, and product-line profitability simultaneously.

2.Product Returns & Quality Control: Certain brands and categories suffered from high return rates, causing hidden logisitical costs and eroding net profit margins, but regional managers could not quickly isolate the root causes.

3.Inventory & Store Type Optimization: Decisions regarding inventory distribution across different store formats (e.g., Supermarkets vs. Small Grocery stores) were largely reactionary rather than data-driven.🎯 
  
   3.Dashboard Goal
   
The primary objective of this multi-page Power BI dashboard is to deliver a strategic, end-to-end analytical tool that transforms raw transactional, product, and geographic data into actionable insights.
The dashboard serves a dual purpose:

1.Executive Overview: Provides senior stakeholders with high-level corporate KPIs (Revenue, Profit, Transactions) at a glance.Operational 

2.Drill-Down: Empowers regional and store managers to filter performance down to specific countries, states, store types, and individual product brands to optimize supply chains and marketing efforts.

📊Key Visuals & Layout Strategy

The canvas is designed following strict UI/UX best practices, prioritizing visual hierarchy, high scannability, and immediate cognitive clarity.

Visual Type                        Component                                                              Business / FunctionalPurpose
KPI Summary Cards       Total Revenue, Total Profit, Total Transactions, Return Rate      Placed at the top of the canvas to establish an immediate baseline of                                                                                                             current business health.
Line Chart                            Monthly RevenueTrend                                 Visualizes temporal patterns, seasonal shopping spikes, and macro-level                                                                                             revenue trajectories over    time.
Geographic Map          Total Revenue by Store Location                                   Uses bubble size/density to immediately reveal high-performing                                                                                                      territories versus underperforming regional markets.
Bar / Matrix Chart      Profit vs. Return Rate by Product Brand                            Explicitly contrasts highly lucrative brands against vendor products                                                                                                responsible for severe return-logistics costs.
Donut Chart             Transactions by Store Type                                         Evaluates retail format efficiency (e.g., Supermarkets vs. Gourmet                                                                                                  Markets) to guide real estate and space planning.

⚡ Derived Metrics (Core DAX Formulas)

To move past basic data aggregation, the model leverages specialized Data Analysis Expressions (DAX) to build dynamic, context-aware business metrics:

1. Total Transactions
 Tracks the baseline checkout velocity across all retail locations.
 

 Transactions = COUNTROWS('Transaction_Data')

2. Total Revenue
 Calculates gross sales revenue by iterating through transactional quantities and matching them with individual retail prices.



    Revenue = SUMX(
    'Transaction_Data', 
    'Transaction_Data'[quantity] * RELATED('Products'[product_price])
)

3. Total Profit
 Determines net product earnings by taking the gross revenue and subtracting the underlying product wholesale cost.


Total Profit = [Total Revenue] - SUMX(
    'Transaction_Data', 
    'Transaction_Data'[quantity] * RELATED('Products'[product_cost])
)

4. Profit Margin

    Normalizes profitability, allowing direct performance comparison between small local grocery branches and massive regional supermarkets.


Profit Margin = DIVIDE([Total Profit], [Total Revenue], 0)
 
5. Return Rate

 Monitors supply chain quality and potential customer dissatisfaction by comparing items returned against total items sold.
 

Return Rate = DIVIDE(
    SUM('Return_Data'[return_quantity]), 
    SUM('Transaction_Data'[quantity]), 
    0
)




🚀 Business ImpactDeploying this BI solution enables Maven Market to pivot toward a proactive, data-first corporate strategy:



Mitigation of Revenue Leakage:
By setting automated data thresholds on the Return Rate metric, procurement teams can instantly flag faulty vendor batches and renegotiate or terminate underperforming product supply agreements.


Optimized Operational Overhead: Store managers can optimize floor layout and inventory stock based on Transactions by Store Type, ensuring high-demand items are allocated to retail formats that move them fastest.


Targeted Regional Expansion: Corporate planners can leverage the geographic performance map to identify lucrative demographic pockets, reducing the financial risk associated with opening new brick-and-mortar storefronts.












https://github.com/gautami-008/pbi/blob/main/mavan%20ss.png
