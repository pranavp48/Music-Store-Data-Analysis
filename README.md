# Music Store Data Dashboard

## Overview

This project showcases a Power BI dashboard built using SQL for data extraction, Power Query for transformation, and Power BI for visualization. The dashboard provides insights into a music store's data, such as customer spending, genre distribution, and billing trends across countries.

## Key Features

1. **High-Level Metrics:**
   - Total Genres: **25**
   - Total Tracks: **3,497**
   - Total Customers: **59**
   - Total Countries: **24**

2. **Visualizations:**
   - **Employee by Levels**: Hierarchical categorization of employees.
   - **Top 10 Countries by Invoice Count**: Highlighting countries with the highest number of invoices.
   - **Top 10 Customers by Expenditure**: Displaying customers with the highest spending.
   - **Count of Countries by Invoices**: Distribution of invoices by country.
   - **Top 10 Billing Cities**: Cities generating the most revenue.
   - **Number of Tracks by Genre**: Detailed genre-wise track count.

3. **Tools Used:**
   - **SQL**: Extracted raw data from a relational database.
   - **Power Query**: Performed data cleaning, filtering, and transformation.
   - **Power BI**: Built interactive visualizations for the analysis.

---

## Data Pipeline

### **1. Data Extraction (SQL)**
- **Database Structure**: The database includes tables for customers, invoices, employees, tracks, and genres.
- **SQL Queries**:
  - Extract customer and invoice data using `JOIN` operations.
  - Aggregate sales and spending data at the country, customer, and city levels.
  - Retrieve genre and track information for detailed genre analysis.

### Example Query:
```sql
SELECT 
    c.Country AS Country,
    COUNT(i.InvoiceId) AS InvoiceCount,
    SUM(i.Total) AS TotalSales
FROM 
    Customers c
JOIN 
    Invoices i ON c.CustomerId = i.CustomerId
GROUP BY 
    c.Country
ORDER BY 
    TotalSales DESC;
```

### **Detailed Steps Involved in Building the Music Store Dashboard**

This project utilizes SQL for data extraction, Power Query for transformation, and Power BI for creating the visualizations. 
Below is a step-by-step guide to reproduce the Music Store Dashboard:

---

## **Step 1: Data Preparation with SQL**

1. **Understand the Database Schema:**
   - Familiarize yourself with the structure of the database, which likely contains tables such as:
     - `Customers`
     - `Invoices`
     - `Employees`
     - `Tracks`
     - `Genres`

2. **Write SQL Queries:**
   - Extract data from the database for analysis. Examples:
     - **Customer Spending:**
       ```sql
       SELECT 
           c.CustomerId, 
           c.FirstName || ' ' || c.LastName AS CustomerName, 
           SUM(i.Total) AS TotalSpending
       FROM 
           Customers c
       JOIN 
           Invoices i ON c.CustomerId = i.CustomerId
       GROUP BY 
           c.CustomerId, CustomerName
       ORDER BY 
           TotalSpending DESC;
       ```
     - **Genre and Track Count:**
       ```sql
       SELECT 
           g.Name AS Genre, 
           COUNT(t.TrackId) AS TrackCount
       FROM 
           Genres g
       JOIN 
           Tracks t ON g.GenreId = t.GenreId
       GROUP BY 
           g.Name
       ORDER BY 
           TrackCount DESC;
       ```
     - **Invoices by Country:**
       ```sql
       SELECT 
           c.Country, 
           COUNT(i.InvoiceId) AS InvoiceCount, 
           SUM(i.Total) AS TotalSales
       FROM 
           Customers c
       JOIN 
           Invoices i ON c.CustomerId = i.CustomerId
       GROUP BY 
           c.Country
       ORDER BY 
           TotalSales DESC;
       ```

3. **Export the Data:**
   - Export the query results to CSV, Excel, or a similar format for further transformation in Power BI.

---

## **Step 2: Data Cleaning and Transformation in Power Query**

1. **Load the Data:**
   - Import the extracted data files into Power BI through **Home > Get Data**.

2. **Transform Data:**
   - Open the **Power Query Editor** to clean and preprocess the data.
   - **Handle Missing Data:**
     - Replace null or empty fields with appropriate placeholders (e.g., `Unknown` for customer names or genres).
   - **Remove Duplicates:**
     - Eliminate duplicate rows, especially in customer, genre, or invoice data.
   - **Standardize Column Names:**
     - Rename columns for consistency and clarity (e.g., `FirstName + LastName` → `Customer Name`).
   - **Merge Queries:**
     - Combine data from multiple tables (e.g., customers and invoices) to create a unified dataset.

3. **Add Calculated Columns:**
   - Create new columns for specific metrics:
     - **Customer Level:**
       - Assign levels to employees based on roles or performance (e.g., L1 for junior employees, L6 for senior employees).
     - **Track Percentage by Genre:**
       ```DAX
       Track Percentage = ( [TrackCount] / SUM( [TrackCount] ) ) * 100
       ```
   - Format columns to match their data types (e.g., `Country` as text, `Invoice Date` as date).

4. **Data Filtering:**
   - Filter out unnecessary rows or values (e.g., exclude inactive customers or redundant genres).

5. **Apply Changes:**
   - Click **Close & Apply** to save transformations and load the cleaned data into Power BI.

---

## **Step 3: Build the Dashboard in Power BI**

1. **Set Up the Report Page:**
   - Choose a layout theme and set the page size to suit your dashboard design.
   - Add background images, logos, and titles for branding (e.g., "Music Store Data Dashboard").

2. **Create Summary Cards:**
   - Use **Card Visuals** to display KPIs like:
     - Total Genres
     - Total Tracks
     - Total Customers
     - Total Countries

-
### Use of Power Query

#. Data Transformation (Power Query)**
- **Steps Performed**:
  - Removed duplicates and null values from columns like `Country`, `Customer Name`, and `Genre`.
  - Standardized column names for consistency.
  - Created calculated columns for metrics such as `Customer Spending` and `Invoice Count`.
  - Merged datasets to generate a consolidated view of the store's operations.

---

### **3. Data Visualization (Power BI)**
- **Visual Elements**:
  - **Pie Chart**: Top countries by invoice and customer spending.
  - **Bar Charts**: Invoice distribution by country and city.
  - **Table**: Genre-wise track count with totals.
  - **Cards**: Summary statistics like total genres, tracks, customers, and countries.

- **Slicers**: Enable dynamic filtering by country, employee level, and genre.

---
 **Top Countries by Invoice Count:**
     - Use a **Pie Chart** to show the proportion of invoices across the top 10 countries.
   - **Top 10 Customers by Expenditure:**
     - Create a **Donut Chart** displaying customer names and their spending percentages.
   - **Track Count by Genre:**
     - Use a **Table Visual** to display genres with their respective track counts.
   - **Invoices by Country:**
     - Use a **Bar Chart** to show the invoice count for each country.
   - **Top 10 Billing Cities:**
     - Use a **Clustered Bar Chart** to highlight cities generating the most revenue.

4. **Add Slicers for Interactivity:**
   - Insert slicers to filter the data dynamically:
     - By country
     - By genre
     - By employee level

5. **Format Visuals:**
   - Apply consistent colors and font sizes to enhance readability.
   - Add tooltips for more details when users hover over visuals.

6. **Test Interactivity:**
   - Check that slicers and visual interactions are working as intended.
   - Ensure that data updates correctly when filters are applied.
## Files in This Repository

- **`MusicStoreDashboard.pbix`**: Power BI project file containing the final dashboard.
- **`SQL-Scripts.sql`**: SQL scripts for data extraction and pre-processing.
- **`README.md`**: Documentation file (this file).
- **`Screenshots/`**: Folder with images of the dashboard.

---

## Steps to Recreate the Project

### **1. Setup**
- Clone the repository:
  ```bash
  git clone https://github.com/your-username/music-store-dashboard.git
  ```
- Set up the database using the provided schema and sample data.

### **2. Extract Data Using SQL**
- Run the provided SQL scripts (`SQL-Scripts.sql`) to generate the required data tables.
- Export the queried data into a compatible format (e.g., CSV or Excel).

### **3. Clean Data Using Power Query**
- Import the extracted data into Power BI.
- Use **Transform Data** to:
  - Remove nulls and duplicates.
  - Create calculated columns for `Levels` or aggregated fields like `Sum of Total`.

### **4. Build Visualizations in Power BI**
- Create cards, charts, and slicers as per the dashboard layout.
- Format the visuals to enhance readability and aesthetics.

### **5. **Step 4: Publish and Share**

1. **Save the Report:**
   - Save the Power BI file (`.pbix`) locally.

2. **Publish to Power BI Service:**
   - Use **File > Publish > Publish to Power BI Service** to upload the report to your workspace.

3. **Create Dashboards in Power BI Service:**
   - Pin visuals from the report to a new dashboard in the Power BI service for easy sharing.

4. **Share the Report:**
   - Share the dashboard or report link with stakeholders.
   - Set access permissions for viewers or collaborators.
