# PBI

Maven Market Business Intelligence Project📋 
Business ProblemMaven Market is a multinational retail grocery chain operating across multiple countries (primarily the United States, Mexico, and Canada). Management faced significant visibility gaps due to isolated data silos, making it difficult to track overarching performance efficiently.
Key Challenges:
Fragmented Reporting: Executive leadership lacked a single source of truth to monitor regional sales trends, store-level efficiency, and product-line profitability simultaneously.
Product Returns & Quality Control: Certain brands and categories suffered from high return rates, causing hidden logisitical costs and eroding net profit margins, but regional managers could not quickly isolate the root causes.
Inventory & Store Type Optimization: Decisions regarding inventory distribution across different store formats (e.g., Supermarkets vs. Small Grocery stores) were largely reactionary rather than data-driven.🎯 
Dashboard Goal
The primary objective of this multi-page Power BI dashboard is to deliver a strategic, end-to-end analytical tool that transforms raw transactional, product, and geographic data into actionable insights.
The dashboard serves a dual purpose:
Executive Overview: Provides senior stakeholders with high-level corporate KPIs (Revenue, Profit, Transactions) at a glance.Operational 
Drill-Down: Empowers regional and store managers to filter performance down to specific countries, states, store types, and individual product brands to optimize supply chains and marketing efforts.
📊Key Visuals & Layout StrategyThe canvas is designed following strict UI/UX best practices, prioritizing visual hierarchy, high scannability, and immediate cognitive clarity.
Visual TypeComponentBusiness / Functional PurposeKPI Summary CardsTotal Revenue, Total Profit, Total Transactions, Return RatePlaced at the top of the canvas to establish an immediate baseline of current business health.
Line ChartMonthly Revenue TrendVisualizes temporal patterns, seasonal shopping spikes, and macro-level revenue trajectories over time.
Geographic MapTotal Revenue by Store LocationUses bubble size/density to immediately reveal high-performing territories versus underperforming regional markets.
Bar / Matrix ChartProfit vs. Return Rate by Product BrandExplicitly contrasts highly lucrative brands against vendor products responsible for severe return-logistics costs.
Donut ChartTransactions by Store TypeEvaluates retail format efficiency (e.g., Supermarkets vs. Gourmet Markets) to guide real estate and space planning.
⚡ Derived Metrics (Core DAX Formulas)To move past basic data aggregation, the model leverages specialized Data Analysis Expressions (DAX) to build dynamic, context-aware business metrics:
1. Total TransactionsTracks the baseline checkout velocity across all retail locations.Code snippetTotal Transactions = COUNTROWS('Transaction_Data')
2. Total RevenueCalculates gross sales revenue by iterating through transactional quantities and matching them with individual retail prices.Code snippetTotal Revenue = 
SUMX(
    'Transaction_Data', 
    'Transaction_Data'[quantity] * RELATED('Products'[product_price])
)
3. Total ProfitDetermines net product earnings by taking the gross revenue and subtracting the underlying product wholesale cost.Code snippetTotal Profit = 
[Total Revenue] - SUMX(
    'Transaction_Data', 
    'Transaction_Data'[quantity] * RELATED('Products'[product_cost])
)
4. Profit MarginNormalizes profitability, allowing direct performance comparison between small local grocery branches and massive regional supermarkets.Code snippetProfit Margin = DIVIDE([Total Profit], [Total Revenue], 0)
5. Return RateMonitors supply chain quality and potential customer dissatisfaction by comparing items returned against total items sold.Code snippetReturn Rate = 
DIVIDE(
    SUM('Return_Data'[return_quantity]), 
    SUM('Transaction_Data'[quantity]), 
    0
)
🚀 Business ImpactDeploying this BI solution enables Maven Market to pivot toward a proactive, data-first corporate strategy
:Mitigation of Revenue Leakage:
By setting automated data thresholds on the Return Rate metric, procurement teams can instantly flag faulty vendor batches and renegotiate or terminate underperforming product supply agreements.
Optimized Operational Overhead: Store managers can optimize floor layout and inventory stock based on Transactions by Store Type, ensuring high-demand items are allocated to retail formats that move them fastest.Targeted Regional Expansion: Corporate planners can leverage the geographic performance map to identify lucrative demographic pockets, reducing the financial risk associated with opening new brick-and-mortar storefronts.
