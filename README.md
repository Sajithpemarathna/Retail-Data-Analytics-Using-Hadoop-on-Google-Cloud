# Retail-Data-Analytics-Using-Hadoop-on-Google-Cloud
Processed 1M+ records using Hadoop and Google Cloud tools to detect purchasing trends and enhance inventory planning.
# 🛒 Retail Data Analytics Using Hadoop on Google Cloud

This project demonstrates how to use Hadoop and Hive on Google Cloud Dataproc to perform big data analysis on a large retail dataset. The goal was to identify trends and patterns in customer demographics and salary distribution across different countries and genders.

## 🎯 Objective

To process and analyze over **1 million+ retail records** using Hadoop and Hive to extract meaningful insights about customer salary and demographics using distributed computing on Google Cloud.

---

## 🔧 Tools & Technologies

- **Google Cloud Platform (GCP)**
  - Dataproc (Managed Hadoop & Spark)
  - SSH-in-Browser (VM Shell)
- **Hadoop Distributed File System (HDFS)**
- **Apache Hive** (SQL-like interface on Hadoop)
- **Bash Shell Scripts**
- **Linux CLI**

---

## 📁 Dataset Details

- **Source**: Retail dataset with ~200 CSV files, each representing 5-minute data
- **Size**: ~20 GB
- **Fields**:
  - `custId`, `age`, `salary`, `gender`, `country`

---

## 🧱 Cluster Setup

- **Cluster Name**: `sajithbigdata`
- **Region**: `europe-west4-b`
- **Master Node**: `n1-standard-2` (200GB disk)
- **Workers**: 2 nodes (`n1-standard-2`, 100GB each)
- **Monitoring**: Enabled for CPU, memory, and YARN stats

📷 _Cluster Configuration Screenshot_  
![Cluster Info](Cluster%20Details%201.png)  
📷 _Worker & Master Instances_  
![Cluster VMs](Cluster%20details%202.png)

---

## 📦 Data Upload & Preprocessing

- Dataset zipped and extracted via command line:
  ```bash
  wget https://github.com/futurexskill/bigdata/raw/master/retailstore_5mn.zip
  unzip retailstore_5mn.zip
## Data duplicated across 200+ files for parallel processing:

for i in {1..200}; do cp retailstore_5mn.csv "retailstore_5mn_$i.csv"; done
## Hive Table creation

CREATE TABLE retailcust (
  custId INT, 
  age INT, 
  salary FLOAT, 
  gender STRING, 
  country STRING
)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ',' 
LOCATION '/user/sajithsandaruwa17/retail/'
TBLPROPERTIES ("skip.header.line.count"="1");


## Average Salary by Gender and Country

SELECT country, gender, AVG(salary) 
FROM retailcust 
GROUP BY gender, country;
