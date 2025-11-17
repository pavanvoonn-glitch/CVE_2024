# CVE-2024 Data Processing Project

This project is about processing the CVE-2024 dataset using a simple Bronze → Silver → EDA workflow in Databricks Community Edition. I worked with the official CVE JSON files, cleaned them into a proper structure, and ran basic analysis to understand patterns in the 2024 vulnerabilities.

## 1. Bronze Layer

In the Bronze layer, I downloaded the CVE GitHub repository and loaded only the JSON files from the cves/2024 folder. I did not modify anything here. I only:

- Read each JSON file
- Kept all nested fields as raw JSON strings
- Added ingestion timestamp, year, and record ID
- Saved everything as a Delta table

This Bronze table is just the raw data stored in a clean format for the next steps.
<img width="693" height="93" alt="Screenshot 2025-11-16 at 9 04 57 PM" src="https://github.com/user-attachments/assets/20897142-64b1-4304-a046-99a2c041b2ae" />
<img width="535" height="396" alt="Screenshot 2025-11-16 at 9 05 29 PM" src="https://github.com/user-attachments/assets/b3435057-34dc-4f41-ba6e-bc9b1c81cf4a" />
<img width="665" height="88" alt="Screenshot 2025-11-16 at 9 06 14 PM" src="https://github.com/user-attachments/assets/a13e5094-4772-48af-9e1a-f97aa5dfccc7" />
<img width="1047" height="406" alt="Screenshot 2025-11-16 at 9 03 42 PM" src="https://github.com/user-attachments/assets/24e2baf3-1785-409a-aa65-1447e9d58028" />




## 2. Silver Layer

In the Silver layer, I cleaned and structured the data. I parsed the raw JSON fields into columns and extracted useful information such as:

- CVE ID
- Description
- Publish and update dates
- CVSS metrics
- Affected vendors and products

I also added a few helper fields:

- reference_count
- affected_product_count
- has_description
- has_cvss
- cve_number

I filtered only CVE-2024 records and created a clean analysis-ready Silver view.
<img width="1032" height="567" alt="Screenshot 2025-11-16 at 9 08 04 PM" src="https://github.com/user-attachments/assets/b53e1082-1b02-4c44-aaf4-f9854772854b" />
<img width="720" height="235" alt="Screenshot 2025-11-16 at 9 08 58 PM" src="https://github.com/user-attachments/assets/1a19d7f8-491b-4ab6-9ed2-b90d23a157af" />



## 3. EDA

After preparing the Silver layer, I used Spark SQL to perform simple exploratory data analysis (EDA). The analysis includes:

### Monthly CVE counts
How many vulnerabilities were published each month in 2024.
<img width="505" height="326" alt="Screenshot 2025-11-16 at 9 10 15 PM" src="https://github.com/user-attachments/assets/a69f23f0-aa70-495b-aa33-c5d452c7c81c" />


### Severity distribution
Most CVEs showed “Unknown” because many 2024 entries do not yet have CVSS scores.
<img width="301" height="161" alt="Screenshot 2025-11-16 at 9 11 45 PM" src="https://github.com/user-attachments/assets/f14eda0e-c1ec-4644-9f99-9d05ad603f6e" />


### Top vendors
Shows which vendors appeared most often (Linux, Microsoft, Red Hat, Siemens, Apple, Adobe, etc.).
<img width="1020" height="417" alt="Screenshot 2025-11-16 at 9 12 24 PM" src="https://github.com/user-attachments/assets/8d372b82-28fc-49a4-aff4-1d33e90ff51a" />
<img width="1023" height="390" alt="Screenshot 2025-11-16 at 9 13 03 PM" src="https://github.com/user-attachments/assets/a606e03a-4ac2-4aee-8c73-362a1dcd799c" />
<img width="1024" height="379" alt="Screenshot 2025-11-16 at 9 13 27 PM" src="https://github.com/user-attachments/assets/195c20b5-bd82-44a3-8026-1926f55b9139" />


## 4. Conclusion

This project helped me understand how to:
- Load raw JSON files into a Bronze table
- Parse and flatten nested CVE fields
- Build a clean Silver table
- Use Spark SQL to explore trends and vendor patterns

Even though many CVSS scores were missing for 2024, the pipeline worked correctly and the structure can be reused for future CVE datasets.


