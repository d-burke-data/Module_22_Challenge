# Module_22_Challenge : *Spark SQL*

This analysis is a demonstration of [Apache Spark SQL](https://spark.apache.org/sql/). The Jupyter Notebook *Home_Sales_colab.ipynb*, located in the root of the repository, was executed in Google Colab.

# Overview
The analysis used Spark SQL to answer four questions about a home sales dataset and calculates query times for uncached, cached, and partitioned Parquet tables.

## Data
The dataset is 33,287 records in CSV format retrieved from an AWS S3 bucket. The data has the following columns:

|Column|Type|Description|
|---|---|---|
|id|string|Transaction identification string|
|date|date (YYYY-MM-DD)|Date of home sale|
|date_built|date (YYYY)|Year home was built|
|price|integer|Sale price|
|bedrooms|integer|Number of bedrooms|
|bathrooms|integer|Number of bathrooms|
|sqft_living|integer|Square footage of the living space|
|sqft_lot|integer|Square footage of the lot|
|floors|integer|Number of floors|
|waterfront|integer boolean|Is this waterfront property? (1=true, 0=false)|
|view|integer|View rating (0-100)|

# Results
## Questions
1. What is the average price for a four-bedroom house sold for each year?  
![image](https://github.com/user-attachments/assets/3e1fe9f1-37f9-493c-ae16-84cd8ba8358c)

2. What is the average price of a home for each year the home was built, that has three bedrooms and three bathrooms?  
![image](https://github.com/user-attachments/assets/bf890727-2f7e-4d05-85de-28b9ddf64e73)

3. What is the average price of a home for each year the home was built, that has three bedrooms, three bathrooms, two floors, and is greater than or equal to 2,000 square feet?  
![image](https://github.com/user-attachments/assets/0a733b98-b2b3-4ad0-94f4-860ccf63e83b)
  
4. What is the average price of a home per "view" rating having an average home price greater than or equal to $350,000?  
![image](https://github.com/user-attachments/assets/b22e3532-396e-479c-82e5-d9325f194217)

## Query Times
The last question was queried under three different conditions to compare the query execution times, as follows:

|Conditions|Run Time|% of Original Time|
|---|---|---|
|Original table|1.5578 sec|100.0%|
|Cached table|1.3286 sec|85.3%|
|Parquet table, partitioned by *date_built*|0.6026 sec|38.7%|

Thus, the cached table performed slightly better than the original table, and the partitioned parquet table performed considerably better than both of those, completing the query in only 38.7% of the original time. Though the dataset is small, the speed increase for the partitioned data is interesting because the query does not take advantage of the partition criterion *date_built*.
