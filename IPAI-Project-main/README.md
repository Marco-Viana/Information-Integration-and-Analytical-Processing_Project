# Pizza Sales Data Warehouse
Welcome to the Pizza Sales Data Warehouse project! This repository contains all the materials and code used to design, implement, and analyze a data warehouse for a fictional pizza restaurant called Plato’s Pizzeria. By modeling and processing this dataset, we aim to uncover insights regarding pizza sales trends, popular ingredients, peak demand times, and more.

## Table of Contents

1. Overview

2. Project Structure

3. Dataset

4. Dimensional Model

5. ETL Process

6. Analytical Questions

7. Setup & Usage

8. Contributing

## Overview

This project was developed as part of a university course on Integração e Processamento Analítico de Informação, focusing on building an end-to-end Business Intelligence pipeline (Extraction, Transformation, Loading, plus OLAP analysis). The main objectives are:

Analyze the pizza sales dataset (orders, pizzas, categories, ingredients) for data quality, outliers, missing values, and correlations.

Model a dimensional schema suitable for analytical queries.

Implement an ETL process in Python to load cleaned and transformed data into a PostgreSQL database.

Explore insights using a BI tool (e.g., Power BI), focusing on key business questions like most popular pizzas, busiest times, and capacity usage.

## Project Structure

A suggested directory layout:

bash
Copiar
Editar
.
├── data/
│   └── pizza_sales_original.xlsx        # Original dataset (if included)
├── etl/
│   ├── ipai-proj.ipynb                 # Jupyter Notebook with ETL code
│   └── scripts/                        # Any additional Python scripts
├── docs/
│   ├── IPAI_Relatorio_stage3.pdf       # Project report (analysis, modeling, etc.)
│   └── IPAI-DW-Modeling.drawio         # Dimensional modeling diagram
├── reports/
│   └── final_analysis.pbix             # Power BI report (example)
├── README.md                           # This README file
└── ...
Feel free to adjust folder names as needed.

## Dataset

Name: Pizza Sales Dataset

Source: The dataset was originally obtained from Maven Analytics and Kaggle, comprising roughly 48,600 rows of detailed pizza orders.

Data Fields (examples):

Order ID: Unique identifier for each order

Order Date / Time: Timestamp of each transaction

Pizza ID / Name / Category / Ingredients: Information about specific pizzas

Quantity: Number of pizzas in each transaction

Unit Price: Price per pizza

Total Price: Redundant (Quantity × Unit Price) but included for convenience

For a more detailed discussion of each field, including data types, see the project report (sections 2.1 and 2.2).

## Dimensional Model

We used a star schema design, separating descriptive attributes into dimensions and placing measurable metrics in a central fact table.

Fact Table: factOrderDetails

Grain: Each row represents a single transacted line item (e.g., one pizza type within an order).

Measures:

Quantity (# of pizzas in a transaction)

Total Price Transaction (price for that line item)

### Dimensions:

DimDate

Includes attributes such as Day, Month, Year, Hour, Minute, Second, Day of Week, etc.

DimPizza

Represents pizza details (Name, Category, Size, Unit Price, Ingredients).

DimCategory

An outrigger dimension storing high-level pizza categories (Classic, Veggie, Supreme, Chicken).

DimOrder

Summarizes the overall order (e.g., total price).

For a full graphical diagram, please refer to the docs/IPAI-DW-Modeling.drawio file or the star schema in the project report (see section 9).

## ETL Process
We employed Python to automate the Extraction, Transformation, and Loading of the pizza dataset into a PostgreSQL database.

### Extraction

Original data is pulled from pizza_sales_original.xlsx.

No severe data issues found (no duplicates or nulls).

### Transformation

Cleaning and reshaping steps (e.g., splitting timestamps, converting price fields to floats, generating surrogate keys).

Creating dimension tables (DimPizza, DimDate, DimCategory, DimOrder) and the fact table (factOrderDetails).

### Loading

Final structured data is inserted into a PostgreSQL schema on the server appserver-01.fc.di.ul.pt.

Power BI connects to PostgreSQL for analysis.

You can find the notebook containing all ETL logic at etl/ipai-proj.ipynb.

## Analytical Questions

Our core analytical questions, as defined in the project report (section 6), are:

How do pizza ingredients and categories impact popularity and average sales value?

Which days and times are busiest for the restaurant?

How is the pizzeria utilizing its seating capacity (tables and chairs)?

Answers and visualizations (including charts, funnel plots, and correlation matrices) can be found in the final Power BI report and the last sections of the project PDF (IPAI_Relatorio_stage3.pdf, sections 13.1, 13.2, 13.3).

## Setup & Usage

Clone or download this repository.

Install dependencies (within a Python 3 environment):

bash
Copiar
Editar
pip install -r requirements.txt
Make sure you also have PostgreSQL installed and a local or remote instance to connect to.

Configure database credentials in the etl/ipai-proj.ipynb notebook or in a .env file (if using environment variables).

Run the ETL:

Open etl/ipai-proj.ipynb in Jupyter or VSCode.

Execute cells to create dimensions and the fact table in the database.

Analyze in Power BI:

Open reports/final_analysis.pbix in Power BI Desktop.

Update the data source connection if needed (PostgreSQL server credentials).

Refresh to view the latest results.

## Contributing

Contributions are welcome! To propose changes:

Fork the repository.

Create a feature branch: git checkout -b feature/new-insight.

Commit changes: git commit -m "Add new insight for busiest hours analysis".

Push to your fork: git push origin feature/new-insight.

Open a Pull Request explaining your contribution.

## Team Members:
1. Afonso Gama
2. Eduardo Tanqueiro
3. Guilherme Rosário
4. Marco Viana
