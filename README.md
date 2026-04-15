# Market Data Pipeline - Exchange Feed Ingestion System (Python / SQL)
## Trading Problem
Market data quality is a first-order driver of trading performance. 

Small inconsistencies propagate into pricing, risk, and execution errors.

## Core Idea
This system transforms raw exchange data into consistent, model-ready inputs for trading systems.

## Trading Role in System
```
Market Data → Pricing Models → Risk Systems → Execution Decisions
```

## Key Components
- Extraction of raw XML exchange feeds
- Structured transformation (ETL pipeline)
- Normalization of market variables
- Persistent storage for reproducibility
- Scheduled updates for time-series consistency

## Trading Mapping
This layer supports:
- Volatility modeling
- Tisk calculations
- Execution strategies
- Microstructure models


## Key Insights
- Data consistency is critical for trading correctness
- Small schema inconsistencies amplify into PnL distortion
- Most model failures originate from data, not modeling
- Market data is a first-order driver of strategy quality

## Core Takeaway
Trading systems are only as reliable as their data infrastructure.


</br></br></br></br>


<details>
<summary><strong>Implementation Details & Usage</strong></summary>


# Automated Market Data Pipeline (XML / SQL)
A production-style automated market data ingestion pipeline designed to extract, process, and persist structured financial data from a dynamic exchange-style dataset provided by The Clearing Corporation of India (CCIL).

The system replicates a simplified version of a market data feed handler, handling structured but dynamically paginated XML-based data and converting it into a clean, queryable format for downstream quantitative and trading applications.

## System Overview
This project implements a full end-to-end data pipeline:
- Automated extraction of multi-page XML-based financial dataset (~80+ pages)
- Structured transformation into a normalized tabular format
- Persistent storage in a cloud-based SQL database (Azure SQL)
- Scheduled automation for continuous dataset refresh
- Integration-ready design for downstream trading and risk systems

The architecture is designed to simulate real-world market data ingestion pipelines used in trading systems, where reliability, automation, and data freshness are critical.

## Trading & Market Relevance
Although built on public financial data, the system mirrors core components of modern trading infrastructure:
- Market data ingestion layer (exchange-style structured feed)
- ETL pipeline for strategy-ready data formatting
- Automated refresh logic simulating real-time data updates
- Cloud-based persistence layer for strategy consumption
- Data pipeline integration for pricing, risk, and execution systems

<br>

This forms the data foundation layer for quantitative strategies such as:
- Derivatives pricing models
- Volatility trading systems
- Risk monitoring and hedging engines
- Execution simulation environments

##  Integration with Trading Systems
This pipeline is directly integrated with the [Delta-Hedging & Volatility Trading Engine](https://github.com/Briansim74/Delta-Hedging-Volatility-Trading-Engine), enabling:
- Automated ingestion of external market inputs
- Real-time updates of underlying market data feeds
- Continuous recalculation of hedging positions and PnL dynamics
- Simulation of execution-driven portfolio adjustments under evolving market conditions

<br>

This effectively connects market data → pricing → hedging → risk evaluation in a unified system architecture.

##  Core Engineering Components
### 1. Web-based Market Data Extraction
- Selenium + ChromeDriver used to navigate dynamic multi-page XML dataset
- Automated traversal across ~80+ pages of structured financial data
- Designed to handle non-static, interaction-dependent data structures

### 2. Data Transformation Layer
- Parsed raw XML content into structured Pandas DataFrames
- Normalization of financial variables for downstream quantitative usage
- Exported into CSV-based intermediate format for pipeline compatibility

### 3. Cloud Database Integration
- Azure SQL used as persistent storage layer for structured market data
- Python (pyodbc) used for programmatic database operations
- Full-table refresh logic implemented for data consistency

### 4. High-Throughput Data Loading
- BCP (Bulk Copy Program) used for efficient bulk ingestion into SQL database
- Optimized for fast overwrite of time-sensitive datasets

### 5. Automation & Scheduling Layer
- Linux Cron jobs used to schedule recurring execution
- Fully automated pipeline enabling periodic data refresh without manual intervention
- Simulates continuous market data feed updates

##  System Architecture
```
CCIL XML Market Dataset
        ↓
Selenium-based Extraction Layer
        ↓
Structured Data Parsing (Pandas)
        ↓
CSV Intermediate Storage
        ↓
Azure SQL (Data Warehouse Layer)
        ↓
BCP Bulk Load + Refresh Logic
        ↓
Automated Scheduling (Cron)
        ↓
Downstream Quant / Trading Systems
```

## Key Insights
### 1. Market data is fundamentally a pipeline problem
Real trading systems depend on reliable ingestion pipelines rather than raw data access.

### 2. Automation is critical for trading relevance
Scheduled execution simulates continuous market updates, a core requirement in live trading environments.

### 3. Data consistency matters more than raw speed
Full-table refresh logic ensures deterministic downstream behavior for pricing and risk systems.

### 4. ETL structure is the foundation of quant systems
Transforming unstructured market data into structured inputs is a prerequisite for any trading strategy.

## Technologies Used
- Python (data pipeline + automation)
- Selenium / ChromeDriver (web automation)
- Pandas (data transformation)
- SQL (data storage + querying)
- Azure SQL Database (cloud persistence layer)
- Bash / Linux (system automation)
- Cron (scheduled execution)
- BCP (bulk data ingestion utility)
- pyodbc (database connectivity)

## Key Outcome
This project demonstrates the ability to design and implement a fully automated market data pipeline, bridging the gap between raw external financial datasets and structured inputs usable in:
- Quantitative trading models
- Volatility and derivatives pricing systems
- Risk management frameworks
- Execution simulation engines

## Systems Role in Larger Trading Stack
This project serves as the data ingestion layer in a broader quantitative trading architecture:
- Market Data Layer → (this project)
- Pricing & Risk Layer → [Delta-Hedging & Volatility Trading Engine](https://github.com/Briansim74/Delta-Hedging-Volatility-Trading-Engine)
- Decision Layer → [Monte Carlo Decision Engine](https://github.com/Briansim74/Monte-Carlo-Decision-Engine)
- Execution Modeling Layer → [Order Matching Engine](https://github.com/Briansim74/Order-Matching-Engine)

</br></br></br></br>


<details>
<summary><strong>Implementation Details & Usage</strong></summary>

# Automated XML Web Scraping Financial Data Script

In this notebook, I will describe the processes of creating an Automated XML Financial Data Web Scraping Script.

<br/>

The financial data to be scraped would be the Security Wise Repo Market Summary, from The Clearing Corporation of India Limited.

https://www.ccilindia.com/web/ccil/security-wise-repo-market-summary

<br/>

The automation of the script can be seen in my personal portfolio:

https://briansim74-portfolio.webflow.io/projects/xml

<br/>

<br/><b>This script utilises the following programs & languages:</b>

<b>Languages:</b>
1. Python
2. Bash
3. SQL

<b>Programs:</b>
1. Google Colab - Developing the script
2. Selenium & ChromeDriver - Automation of XML Web Scraping
3. Ubuntu Linux - Running the script
4. Cron - Automation of script
5. pyodbc (Python Open Database Connectivity) - To delete all outdated data from SQL Azure database using SQL Query
6. BCP (Bulk Copy Program) Utility - Rapid bulk insert updated data into SQL Azure database
7. Microsoft Azure SQL Database - SQL Cloud database for updating financial data

<br/><b>The following files for reference for this script are:</b>
1. Security_Wise_Holdings_Script.ipynb
2. cron.txt
3. Security_Wise_Holdings.csv
4. Security_Wise_Holdings_Query.sql
5. Security_Wise_Holdings.mp4

<br/><b>Developing the script</b>

First, I installed Selenium and Chromium Driver onto my Google Colab as well as Ubuntu Virtual Machine. Selenium and ChromeDriver are plug-ins to automate the execution of parsing XML data from websites. Due to the dynamic nature of the table, a simple scraping of data into a dataframe was not possible. Here, I utilised the plug-ins to automate scraping each page of data, and also "clicking" onto each next page, all the way till the end of the ~84 pages. 

After that, I processed the relevant data into a Pandas DataFrame with relevant column names. I then exported the DataFrame into a CSV file to be stored in my Ubuntu Desktop.

Using the pyodbc driver, I then connected to the Microsoft Azure SQL cloud database where the Security Wise Holdings SQL Table exists, and parsed a query to delete all outdated data from the table.

In the same script, I added a command to execute the BCP utility to bulk copy the updated CSV file into the Security Wise Holdings SQL Table in the Microsoft Azure SQL database, whereby the database would then be updated with the most recent CSV file.

<br/><b>Running and Automation of the script</b>

I utilised Ubuntu Linux for the automation of the script. I started a new Cronjob on Crontab, an automatic task scheduler, whereby I set the Python script to run every minute, thus updating the Azure SQL database every minute with new data. 

Finally, the automation of the Web Scraping Script can be seen by the updating of the Azure SQL database every minute by quering the Security Wise Holdings SQL Table from the Microsoft Azure Portal.

Security_Wise_Holdings.mp4 shows the automation of the script.

</details>
</br></br>

</details>
</br></br>
