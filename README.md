



# Project Title: Plastic Windows Analysis 🪟📊

- **Author:** Szymon Swiezy
- **Email:** szymon.swiezy1@gmail.com
- **Website:** www.datascienceportfol.io/szymonswiezy
- **LinkedIn:** www.linkedin.com/in/szymon-świeży

The aim of the project is to analyze the global PVC window market in terms of exports and imports over the last 24 years. This will help companies involved in PVC window manufacturing to understand global trade trends and make informed business decisions. The analysis will cover the main trading directions, key market players, export and import values in various regions. As a result, companies will be able to adjust their marketing strategies, production, and distribution to changing market conditions, thus increasing their competitiveness and profitability.

The goal is to demonstrate the ability to **clean, analyze, transform, model, visualize, and extract insights driving actionable recommendations using Power BI**.

## Data Sources 📂
The data in the project can be divided into:
- **Dimensional Data**, consisting of [csv and json](https://github.com/SimonAnalyst/Plastic-Windows-Analysis/tree/main/Files) files, which will be used to build dimension tables in the Star Schema model in Power BI and visualization in the report.
- **Fact Table**, where all important information regarding international trade over the last 24 years is stored. The fact table practically consists only of ID and value columns.

The data was retrieved using APIs of UN Comtrade. Due to limitations to 100k rows, each month had to be downloaded in a separate file, resulting in a total of 248 CSV files(1 file per month).
Detailed API documentation is available at the following [link](https://github.com/uncomtrade/comtradeapicall/blob/main/README.md).



Below is a detailed description that helped in generating the query.

Selection Criteria

- typeCode(str): Product type. Goods (C) or Services (S)
- freqCode(str): The time interval at which observations occur. Annual (A) or Monthly (M)
- clCode(str): Indicates the product classification used and which version (HS, SITC)
- period(str): Combination of year and month (for monthly), year for (annual)
- reporterCode(str): The country or geographic area to which the measured statistical phenomenon relates
- cmdCode(str): Product code in conjunction with classification code
- flowCode(str): Trade flow or sub-flow (exports, re-exports, imports, re-imports, etc.)
- partnerCode(str): The primary partner country or geographic area for the respective trade flow
- partner2Code(str): A secondary partner country or geographic area for the respective trade flow
- customsCode(str): Customs or statistical procedure
- motCode(str): The mode of transport used when goods enter or leave the economic territory of a country

Query Options

- maxRecords(int): Limit number of returned records
- format_output(str): The output format. CSV or JSON
- aggregateBy(str): Option for aggregating the query
- breakdownMode(str): Option to select the classic (trade by partner/product) or plus (extended breakdown) mode
- countOnly(bool): Return the actual number of records if set to True
- includeDesc(bool): Option to include the description or not


## Connect and transform the raw data 🛠️📈

The following steps apply to:

- **Data Exploration**
- **Data Understanding**
- **Data Cleaning**
- **Data Preparation**
- **Data Modelling**
- **Data Transformation**
- **Visualization Design**
- **Dashboard Development**
- **Dynamic Filtering**
- **Insights**

### Retrieving data

After preliminary analysis of the source files in Python, the data was [retrieved via API](Code/Data_retrieval.ipynb) to the appropriate folder and imported into Power BI using Power Query.

### Power Query
In Power Query, data was imported from various sources, cleaned of unnecessary columns (the fact table was reduced from 48 columns to 16), and standardized. Some tables were joined. Additionally, a date table was created in the form of a calendar.
M code is available in the [file](https://github.com/SimonAnalyst/Plastic-Windows-Analysis/blob/main/Code/Power%20Query%20M%20code.txt).

### Data modeling in Power BI
Based on the imported tables, a classic "Star Schema" data model with one-to-many relationships was created, which will help avoid errors associated with overcomplicating the model and facilitate writing measures in DAX. The entire data model fits into 16 tables.
Additionally, some tables without relationships and parameter tables were created, which will allow for the execution of some visualizations and measures.

![Data model](https://github.com/SimonAnalyst/Plastic-Windows-Analysis/assets/154997462/deb36b86-9616-427c-85bc-7c365d2f6f35)




### Data exploratory in DAX
Using the DAX Query View, I performed [data exploration](Code/DAX_fact_table_exploratory.txt), which allowed me to accurately remove unnecessary columns in Power Query.

### Measures in DAX:
In the DAX language, [50 measures](https://github.com/SimonAnalyst/Plastic-Windows-Analysis/blob/main/Code/DAX%20measures.txt) were written, which were used to create the dashboard. Measures can be divided into 2 types:
-**analytical measures** used to convey insights
-**interactive measures** used to change titles, change colors, increase dashboard interactivity

### Visualization:
The dashboard consists of 3 pages:

- **Overview** - allows for a general view of PVC window exports and imports for all countries associated with the industry and how trade has changed over time. The central point of the page is an interactive map.
- **Exploration** - allows checking correlations between different computational measures and seeing how selected KPIs have changed over time. Everything in a scatter chart. You can also check each country in detail in terms of various KPIs and in terms of the method of window transport in a matrix.
- **Trade** - allows checking exports and imports for a specific country and how YoY change. By selecting a specific country, you can check to which continent/region/country and in which year the most or least was exported. The central point of the page is a Decomposition tree visualization.

Dashboard's appearance can be seen [here](https://github.com/SimonAnalyst/Plastic-Windows-Analysis/blob/main/Files/Plastic%20Windows%20Analysis.pdf).

![Zrzut ekranu 2024-02-20 113009](https://github.com/SimonAnalyst/Plastic-Windows-Analysis/assets/154997462/f89bfbc3-70fc-453d-a823-16d4db7c4cf8)

## Conclusions 📋

Analyzing the PVC window market using a Power BI dashboard can bring many benefits to companies involved in manufacturing these windows. Here are a few conclusions that may be valuable for the user/company:

**Global trade trends**: The dashboard allows tracking global trends in PVC window exports and imports over the past 24 years. This enables companies to understand how trade in this product has evolved over time and where the main areas of growth or decline are.

**Key market players**: The analysis enables identification of the largest players in the PVC window market, both in terms of exports and imports. This allows companies to better understand who dominates the market and what their shares are in trading this product.

**Trade value in various regions**: The dashboard shows the value of PVC window exports and imports in different regions of the world. This allows companies to identify the most promising markets and understand where there may be opportunities for business expansion.

**Adjustment of business strategy**: Based on the data collected and indications from the dashboard, companies can adjust their marketing strategies, production, and distribution to changing market conditions. The ability to analyze global trends enables making informed business decisions, increasing competitiveness, and profitability of the company.
