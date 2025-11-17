# CVE_2024
CVE-2024 Data Processing Project

In this project, I worked on processing the CVE-2024 dataset using a simple Bronze → Silver → EDA flow. My goal was to load the raw JSON files, clean them into a proper structure, and run some basic analysis to understand the data.

1. Bronze Layer
In the Bronze layer, I took all the raw JSON files from the cves/2024 folder and loaded them into Databricks. I did not change anything here. I kept the JSON fields as they are, added an ingestion timestamp and year column, and saved everything in Delta format. This layer is just the raw data.

(Add your Bronze screenshots here)
![Bronze Sample](images/bronze_sample.png)
![Bronze Schema](images/bronze_schema.png)

2. Silver Layer
In the Silver layer, I cleaned and structured the data. I parsed the JSON fields and extracted the main information like CVE ID, description, dates, CVSS metrics, and affected vendors/products. I also flattened the affected products using explode and added some helper columns like reference_count and affected_product_count. This gave me a clean table for analysis.

(Add your Silver screenshots here)
![Silver Sample](images/silver_sample.png)
![Silver Schema](images/silver_schema.png)

3. EDA
After preparing the Silver table, I used Spark SQL to explore the data. I checked how many CVEs were published each month, looked at severity distribution, found the top vendors, and checked severity for those vendors. Most severity values showed as Unknown because many CVSS scores for 2024 are still not available.

(Add your EDA screenshots here)
![Monthly](images/monthly.png)
![Severity](images/severity.png)
![Vendors](images/vendors.png)
![Vendor Severity](images/vendor_severity.png)

Conclusion
This project helped me understand how to load raw JSON data, parse and clean nested fields, build a structured table, and run simple analysis using Spark SQL. Even though the 2024 dataset had missing CVSS scores, the pipeline works correctly and can be reused for other years.

Place all screenshots inside the /images folder in the repository.
