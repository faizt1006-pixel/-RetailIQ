RetailIQ — Inventory & Sales Analytics Dashboard
A working local web application for a general retail shop, built with Python, Streamlit, Pandas, Plotly, and SQLite.
Features
Dashboard with net sales, gross profit, gross margin, units sold, and inventory cost value
Sales trend, category mix, top products, and low-stock alerts
Product catalogue: add and edit products, supplier, cost, price, reorder threshold
Record sales with invoice reference, discount, customer, and payment method
Automatic stock deduction when a sale is recorded
Record purchases/restocks and automatically increase stock
Controlled stock adjustments with a stock movement ledger
Sales and purchase histories
CSV exports for products, sales, purchases, and stock movements
30-day demand-based restock suggestions
SQLite database persists data locally
Seeded demo catalogue and historical demo sales on first launch
Requirements
Python 3.10 or newer recommended
Internet connection for the first install of Python packages
Run on Windows
Extract `inventory_sales_analytics.zip` to a folder.
Open that folder in File Explorer.
Click the address bar, type `cmd`, and press Enter.
Create a virtual environment:
```bat
   py -m venv .venv
   .venv\Scripts\activate
   ```
Install dependencies:
```bat
   python -m pip install -r requirements.txt
   ```
Start the application:
```bat
   streamlit run app.py
   ```
Streamlit will open the app in your browser. If it does not, open the local URL shown in the terminal (usually `http://localhost:8501`).
Run on macOS / Linux
```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
streamlit run app.py
```
Database schema
The app automatically creates `inventory.db` on first run. Main tables:
`products`: SKU, name, category, supplier, cost price, selling price, current stock, reorder level
`sales`: invoice, product, quantity, sale price, cost snapshot, discount, date, customer, payment method
`purchases`: purchase reference, product, quantity, cost, date, supplier
`stock_movements`: auditable record of opening stock, sales, purchases, and manual adjustments
The SQL schema is also available in `schema.sql`.
Demo data
The app seeds 12 example products and 95 sample sales spread over the previous 90 days. Values are fictional and are intended for demonstration only. Demo sales are historical records and do not deduct from the opening stock a second time.
Important behavior
Sales cannot exceed current available stock.
Sale creation and stock deduction happen together in a database transaction.
Discounts cannot exceed the line's gross sale value.
Gross profit = net sales after discount − cost of units sold.
Inventory at cost = current stock quantity × current product cost.
Restock recommendations use a simple last-30-day demand heuristic; they are not guaranteed forecasts.
The sidebar's Reset demo database button deletes the local database and recreates demo data. This action discards local changes.
Suggested presentation demo
Open Dashboard and explain the KPIs and charts.
Add a new product.
Record a purchase to increase its stock.
Record a sale and show stock decreasing.
Open Stock alerts and the stock movement ledger.
Export the sales CSV and open it in Excel.
Before real business use
This is a local prototype, not a production-ready POS or accounting system. Add authentication, authorization, backups, audit logs, stronger validation, multi-user concurrency controls, tax and invoice compliance review, and deployment security before handling real business/customer data.
