# Introduction to BigData

## *What is Data Engineering*

Data engineering is the practice of **designing, building, and managing systems** that collect, store, and process data at scale. It focuses on creating **reliable, efficient, and scalable pipelines** to make data accessible for analytics, reporting, and machine learning. Data engineering ensures that **raw data is transformed into structured, high-quality, and usable formats** for decision-making.

---

## **Data Engineers’ Responsibilities**

### **Business Responsibilities**

* **Understanding business requirements:** Translate analytics and reporting needs into data specifications.
* **Data governance & compliance:** Ensure data security, privacy, and adherence to organizational policies.
* **Collaboration with stakeholders:** Work with analysts, data scientists, and business teams to ensure data availability.

### **Technical Responsibilities**

* **Data pipeline development:** Build ETL/ELT pipelines to ingest, clean, and transform data.
* **Data modeling & architecture:** Design schemas, data warehouses, and lakes for optimal storage and performance.
* **Data quality & monitoring:** Implement checks to maintain accuracy, consistency, and reliability.
* **Performance optimization:** Ensure data systems are scalable and queries run efficiently.
* **Tooling & automation:** Use platforms like Airflow, Spark, Kafka, Hadoop, and cloud services for workflow automation.

---

## **Role of a Data Engineer in Data Science**

* Provides **clean, structured, and accessible data** for data scientists.
* Ensures data pipelines are **reliable and reproducible** for experiments and models.
* Collaborates to **deploy ML models** by supplying feature stores, training datasets, and streaming data sources.
* Bridges the gap between **raw data and actionable insights**.

---

## **Data Engineers’ Interactions**

* **Data Scientists:** Supply processed data, design pipelines for ML models, and ensure data availability.
* **Data Analysts / BI Teams:** Provide curated datasets and maintain dashboards or reporting systems.
* **Software Engineers:** Integrate data pipelines into applications and production systems.
* **Business Stakeholders:** Gather requirements, explain data capabilities, and support decision-making.
* **DevOps / Cloud Engineers:** Deploy, monitor, and maintain data infrastructure in production.

---

## **The Data Engineering Lifecycle**

The data engineering lifecycle represents the **end-to-end process of managing data** from creation to consumption. It ensures that data is **reliable, accessible, and useful** for analytics, reporting, and machine learning. The key stages are:

---

### **1. Data Generation**

* Data is **created at the source**, which can include:

  * Applications, transactional databases, IoT devices, logs, APIs, or third-party sources.
* Both **structured and unstructured data** can be generated.

---

### **2. Data Storage**

* Raw or semi-processed data is **stored efficiently** for future use.
* Storage options include:

  * **Data Lakes:** For raw, unstructured, or semi-structured data (HDFS, S3).
  * **Data Warehouses:** For structured, analytics-ready data (Redshift, Snowflake).
  * **Databases:** Relational (PostgreSQL, MySQL) or NoSQL (MongoDB, Cassandra).

---

### **3. Data Ingestion**

* Moving data from **sources into storage or pipelines**.
* Can be **batch ingestion** (periodic uploads) or **streaming ingestion** (real-time events).
* Tools commonly used: Kafka, Kinesis, Apache NiFi, Airflow.

---

### **4. Data Transformation**

* Converts raw data into **clean, structured, and usable formats**.
* Includes:

  * Cleaning (removing duplicates, handling missing values)
  * Normalization or denormalization
  * Aggregation, filtering, and enrichment
* Usually done using **ETL/ELT pipelines** with Spark, SQL, or Python.

---

### **5. Serving Data**

* Making processed data **available to end-users, analysts, or ML models**.
* Can be provided via:

  * Data warehouses for analytics and dashboards
  * APIs or feature stores for machine learning
  * BI tools and reporting layers for business users

---

This lifecycle ensures that **data flows smoothly from generation to actionable insights**, maintaining **quality, reliability, and accessibility** throughout the process.

---

## **Undercurrents in the Data Engineering Lifecycle**

These are the **cross-cutting aspects** that ensure the data engineering lifecycle runs **securely, efficiently, and reliably**.

---

### **1. Security**

* Ensures **data privacy, integrity, and compliance** throughout the lifecycle.
* Includes authentication, authorization, encryption, and monitoring.
* Protects sensitive data from **unauthorized access and breaches**.

---

### **2. Data Management**

* Focuses on **organizing, storing, and maintaining data** effectively.
* Covers **metadata management, master data management, and data catalogs**.
* Ensures data is **consistent, discoverable, and trustworthy**.

---

### **3. DataOps**

* Brings **Agile and DevOps principles to data engineering**.
* Emphasizes **automation, collaboration, testing, and monitoring** of data pipelines.
* Improves **pipeline reliability, speed, and maintainability**.

---

### **4. Orchestration**

* Coordinates the **execution of data pipelines and workflows**.
* Handles dependencies, scheduling, and retries.
* Tools: Apache Airflow, Prefect, Luigi, Azure Data Factory.

---

### **5. Data Lifecycle Management (DLM)**

* Manages data **from creation to archiving or deletion**.
* Ensures proper **retention policies, compliance, and storage optimization**.
* Helps prevent **data sprawl and reduces costs**.

---

### **6. Automation**

* Reduces **manual intervention** in data pipelines and operations.
* Enables **scalable, repeatable, and error-free processes**.
* Examples: automated ingestion, transformation, monitoring, and alerting.

---

## *What is Big Data*

Big Data refers to **extremely large and complex datasets** that traditional database systems cannot efficiently store, process, or analyze. It is characterized by **volume, velocity, and variety**, often requiring distributed storage and parallel processing to extract insights.

---

## **Large-Scale Data Storage**

* Big Data requires storage systems that can **handle massive volumes of structured, semi-structured, and unstructured data**.
* Examples: HDFS, cloud object storage (AWS S3, Azure Data Lake), NoSQL databases.
* Storage systems are often **distributed and fault-tolerant**.

---

## **Large-Scale Data Analysis**

* Involves **processing and analyzing massive datasets** to extract insights.
* Techniques include **batch processing, real-time streaming, machine learning, and advanced analytics**.
* Frameworks: Apache Spark, Flink, Hive, Presto.

---

## **Cost Effectiveness**

* Big Data platforms leverage **commodity hardware, cloud storage, and distributed computing** to reduce costs.
* Using **scalable storage and processing solutions** avoids expensive centralized systems.

---

## **Data Sources Evolution**

* Traditional sources: relational databases, spreadsheets, ERP/CRM systems.
* Modern sources: social media, IoT devices, clickstreams, logs, APIs, sensor data.
* Data has become **more diverse, high-volume, and real-time**.

---

## **Big Data Families**

* **Hadoop Ecosystem:** Distributed storage and batch processing (HDFS, MapReduce, YARN, Hive, Spark).
* **NoSQL Databases:** Flexible, schema-less storage for high-velocity and unstructured data (MongoDB, Cassandra, Redis).
* **NewSQL Databases:** Combines **scalability of NoSQL** with **ACID compliance** of SQL (CockroachDB, Google Spanner).

---

## **How Data Engineering Workflow Looks Like**

1. **Ingest** – Collect data from multiple sources, both batch and streaming.
2. **Persist** – Store data in scalable storage systems (data lake, warehouse, or NoSQL).
3. **Data Product** – Transform and structure data into **curated datasets, reports, or ML-ready features**.
4. **Prepare Data** – Clean, enrich, and aggregate data for **analytics, BI dashboards, or machine learning pipelines**.

---

## **Why Do You Use Big Data Tools?**

Big Data tools are used to efficiently **store, process, and analyze massive datasets** that traditional systems cannot handle. The main reasons include:

* **Resource Pooling** – Big Data frameworks like Hadoop or Spark use **clusters of commodity hardware** to pool storage and compute resources, enabling distributed processing of large datasets.

* **Availability** – These tools are designed to be **fault-tolerant and highly available**, ensuring that data remains accessible even if some nodes fail.

* **Easily Scalable** – Big Data platforms can **scale horizontally** by adding more nodes to the cluster, allowing them to handle increasing volumes of data without significant downtime or re-architecture.

---

## *Data Characteristics*

* **Structured Data** – Data that is organized in **rows and columns** and stored in relational databases. Easy to query using SQL.

  * Examples: Customer tables, sales records, inventory data.

* **Unstructured Data** – Data that has **no predefined schema** and does not fit neatly into rows and columns.

  * Examples: Text files, images, videos, social media posts, sensor logs.

---

## **Schema on Read vs Schema on Write**

* **Schema on Write** – Data is **structured before storing** in the database. Schema must be defined upfront.

  * Example: Relational databases (PostgreSQL, MySQL).
  * Pros: Data integrity, faster reads.
  * Cons: Less flexible for unknown or evolving data.

* **Schema on Read** – Data is **stored in raw form** and structured **when reading or querying**.

  * Example: Data lakes (HDFS, S3) with Spark or Hive.
  * Pros: Flexible, can handle changing data formats.
  * Cons: Query performance can be slower.

---

## **Speed of Data – Real-Time to Batch Processing**

* **Real-Time / Streaming** – Processes data **immediately** as it arrives.

  * Example: Kafka, Spark Streaming, Flink.

* **Micro-Batch** – Processes **small batches of data at short intervals**.

  * Example: Spark Structured Streaming.

* **Batch** – Processes **large volumes of data periodically** (hours, days).

  * Example: Daily sales aggregation using Hadoop MapReduce or Spark batch jobs.

---

## **Storage & Formats of Data**

* **File Storage** – Raw files stored in HDFS, S3, or local file systems.
* **NoSQL** – Stores semi-structured or unstructured data (MongoDB, Cassandra).
* **Traditional DB** – Relational databases with structured data (PostgreSQL, MySQL).

---

## **Raw File Formats vs Processed File Formats**

* **Raw File Formats** – Original data captured from sources, often uncleaned and unstructured.

  * Examples: CSV logs, JSON events, sensor readings.

* **Processed File Formats** – Data that has been **cleaned, transformed, and optimized** for analytics.

  * Examples: Parquet, ORC, Avro.

---

## **Formats of Data**

* **Row-Oriented** – Stores data **row by row**. Efficient for **transactional operations**.

  * Examples: CSV, traditional RDBMS tables.

* **Column-Oriented** – Stores data **column by column**. Efficient for **analytical queries** and aggregations.

  * Examples: Parquet, ORC.

* **Data Compression** – Reduces **storage footprint** and can improve **read performance**.

  * Examples: Snappy, Gzip, ZSTD for columnar formats.

---

## *Big Data Solutions*

* Efficient Big Data solutions **integrate storage, processing, analytics, and access** to deliver actionable insights at scale.
* Key characteristics include:

  * **Scalability:** Can handle growing volumes of structured and unstructured data.
  * **Reliability & Availability:** Fault-tolerant and highly available systems.
  * **Flexibility:** Supports batch, micro-batch, and streaming processing.
  * **Cost-effectiveness:** Optimizes storage and compute resources.
  * **Security & Governance:** Ensures compliance and data integrity.

---

## **General Big Data Architecture**

1. **Edge / Ingestion Layer**

   * Captures data from **IoT devices, logs, applications, APIs, and external sources**.
   * Handles **streaming and batch ingestion** using tools like Kafka, Kinesis, NiFi, or Flume.

2. **Data Storage Layer**

   * Stores raw and processed data for analytics and ML.
   * Includes:

     * **Data Lakes:** HDFS, S3 for raw/unstructured data.
     * **Data Warehouses:** Redshift, Snowflake for curated structured data.
     * **NoSQL Databases:** MongoDB, Cassandra for high-velocity semi-structured data.

3. **Analytics Production Pipelines**

   * ETL/ELT pipelines transform raw data into **analytics-ready datasets**.
   * Supports **real-time streaming and batch processing**.
   * Tools: Spark, Flink, Airflow, Databricks.

4. **Management Components**

   * **Orchestration:** Automates pipeline scheduling and execution.
   * **Monitoring & Logging:** Tracks pipeline health and performance.
   * **Data Governance:** Ensures quality, compliance, and cataloging.

5. **Exploratory / Data Science Environment**

   * Supports **feature engineering, model prototyping, and experimentation**.
   * Tools: Jupyter Notebooks, Databricks, SageMaker.

6. **CI/CD Pipelines**

   * Automates **deployment of data pipelines, ML models, and analytics workflows**.
   * Ensures reproducibility, version control, and continuous delivery.

7. **ML Training / AI Services**

   * Uses curated datasets to **train machine learning models**.
   * Supports **inference and AI service deployment** for applications.

8. **Data Product Storage**

   * Stores **processed datasets, features, and model outputs** for consumption.
   * Can be a **feature store, data warehouse, or object storage**.

9. **Data Access Layer**

   * Provides **secure access to data products** for analytics, BI, and ML.
   * Tools: APIs, dashboards, SQL queries, or feature stores.

10. **AI Products & AI Access**

    * Deploys **ML/AI models as applications or services**.
    * End-users or downstream systems access predictions via APIs or dashboards.

---

This architecture ensures that data **flows from source to insight**, supports **analytics and AI at scale**, and maintains **reliability, governance, and performance**.

---

## **Data Modeling Methodologies**

Data modeling methodologies define how **data is structured, stored, and accessed** to support analytics, reporting, and operational systems. Different approaches are used depending on the **use case, volume, and type of data**.

---

### **1. Data Lakes**

* **Purpose:** Store **raw, unstructured, semi-structured, and structured data** at scale.
* **Characteristics:** Schema-on-read, highly scalable, cost-effective storage.
* **Use Cases:** Big Data analytics, machine learning, exploratory data analysis.
* **Example Tools:** HDFS, AWS S3, Azure Data Lake.

---

### **2. Data Warehouse**

* **Purpose:** Store **structured, cleaned, and curated data** optimized for analytics and reporting.
* **Characteristics:** Schema-on-write, high query performance, integrates data from multiple sources.
* **Use Cases:** OLAP, business intelligence, dashboards, reporting.
* **Example Tools:** Snowflake, Amazon Redshift, Google BigQuery.

---

### **3. Data Mart**

* **Purpose:** Subset of a data warehouse focused on a **specific business line, department, or use case**.
* **Characteristics:** Simplified structure, faster access for targeted analytics.
* **Use Cases:** Sales analysis, finance reporting, marketing insights.
* **Example:** A sales data mart aggregating only sales and customer data from the enterprise warehouse.

---

### **4. Data Vault**

* **Purpose:** Provide a **flexible, scalable, and auditable data modeling approach** for enterprise data warehouses.
* **Characteristics:** Combines **hubs (entities), links (relationships), and satellites (descriptive attributes)**.
* **Use Cases:** Historical tracking, complex enterprise integrations, compliance-heavy environments.
* **Advantages:** Handles **change over time**, integrates multiple sources, supports agility in modeling.

---

## *What is Databricks*

Databricks is a **cloud-based data platform** that provides a **unified environment for big data processing, analytics, and machine learning**. It is built on **Apache Spark**, enabling **distributed data processing at scale**.

### **Key Features**

* **Unified Analytics:** Combines **data engineering, data science, and business analytics** in a single platform.
* **Scalable Processing:** Handles **large-scale batch and streaming data** efficiently.
* **Collaborative Workspace:** Provides notebooks and collaborative tools for **data scientists, analysts, and engineers**.
* **Machine Learning & AI:** Supports **training, deployment, and monitoring of ML models**.
* **Integration:** Connects to **data lakes, warehouses, cloud storage, and BI tools** seamlessly.
* **Managed Service:** Fully managed in the cloud (AWS, Azure, GCP), reducing infrastructure management overhead.

### **Use Cases**

* Building **ETL/ELT pipelines** for analytics.
* Running **big data processing jobs**.
* Developing and deploying **machine learning models**.
* Performing **exploratory data analysis and BI reporting**.

---
