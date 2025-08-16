# Data Modelling and Data Architecture

## *Approaching Data Modeling*

### **Database Modeling**

Database modeling is the process of creating a structured representation of the data and its relationships within a database. It involves defining how data will be stored, organized, and accessed to ensure consistency, efficiency, and integrity. The purpose of database modeling is to visualize the entities, their attributes, and the relationships between them, which helps in designing a database that supports the requirements of applications and users while minimizing redundancy and potential errors.

---

### **Data vs Information**

Data refers to raw, unprocessed facts, figures, or symbols that by themselves **have no meaning**, such as numbers, words, or measurements. Information, on the other hand, is what you get when data is **processed, organized, or interpreted** in a way that makes it meaningful and useful for decision-making. In short, data is the raw input, and information is the meaningful output derived from that data.

---

### **Why Is Data Modeling Important?**

Data modeling is important because it provides a clear blueprint for how data will be stored, organized, and accessed in a database. It ensures that the database supports business requirements, reduces redundancy, maintains data integrity, and makes it easier to manage and scale as the system grows. Essentially, it lays the foundation for efficient, reliable, and meaningful use of data.

---

### **Benefits of Data Modeling**

* **Improved Data Quality** – By defining entities, attributes, and relationships clearly, data modeling reduces errors, inconsistencies, and duplication.

* **Better Communication** – Visual representations like ER diagrams help developers, analysts, and stakeholders understand the database structure and business rules.

* **Increased Efficiency** – Proper modeling leads to optimized queries and faster performance, as data is organized logically and storage is used effectively.

* **Easier Maintenance and Scalability** – A well-structured model simplifies updates, schema changes, and expansion of the database as business needs evolve.

* **Supports Business Decision-Making** – By organizing data effectively, it becomes easier to generate meaningful reports and insights for strategic decisions.

* **Cost Reduction** – Preventing redundancy and errors early in the design reduces the time and resources needed for fixing issues later.

---

## *Data Modeling Levels*

### **Types of Relationships in Database Modeling**

Relationships define how **entities are connected** in a database. There are three main types:

1. **One-to-One (1:1)**

   * Each record in one entity corresponds to **exactly one record** in another entity.
   * Example: Each person has one passport, and each passport belongs to one person.

2. **One-to-Many (1\:N)**

   * A record in one entity can relate to **multiple records** in another entity, but each record in the second entity relates to **only one record** in the first.
   * Example: A department has many employees, but each employee belongs to only one department.

3. **Many-to-Many (M\:N)**

   * Records in one entity can relate to **multiple records** in another entity and vice versa.
   * Requires a **junction (or bridge) table** to implement in relational databases.
   * Example: Students can enroll in multiple courses, and each course can have multiple students.

---

### **IE (Information Engineering) Notation**

* Also called **Crow’s Foot Notation**.
* **Entities** are represented as rectangles.
* **Relationships** are lines connecting entities, with symbols at the ends showing **cardinality**:

  * Single line = one
  * Crow’s foot = many
  * Circle = zero (optional)
* Popular for **relational database design** and easy to read for developers.

---

### **IDEF1X (Integration Definition for Information Modeling) Notation**

* Standardized by the U.S. Air Force for **complex database modeling**.
* **Entities** are rectangles with **primary keys** underlined.
* **Relationships** use lines with **symbols indicating mandatory/optional and identifying/non-identifying relationships**.

  * Solid line = identifying (child depends on parent)
  * Dashed line = non-identifying (child can exist without parent)
* Focuses on **rigorous, precise modeling** for large enterprise systems.

---

## *Data Modeling Techniques Overview*

* Data modeling techniques define how data is structured and stored for different purposes.
* Choosing the right technique depends on **use case, type of analysis, and performance needs**.

---

### **1. ER Modeling (Entity-Relationship Modeling)**

* Focuses on **entities, attributes, and relationships**.
* Helps design a **conceptual and logical schema**.
* **When to use:**

  * At the **beginning of database design** to visualize data requirements.
  * Suitable for **transactional systems** where relationships and constraints are important.

---

### **2. 3NF Modeling (Third Normal Form)**

* Organizes data to **eliminate redundancy** and ensure **data integrity**.
* Tables are **normalized** so that each non-key attribute depends only on the primary key.
* **When to use:**

  * OLTP systems requiring **frequent inserts, updates, and deletes**.
  * Ensures **efficient storage and consistency**.

---

### **3. Dimensional Modeling**

* Optimized for **analytics and reporting** in data warehouses.
* Organizes data into **facts and dimensions** for easy querying.
* **When to use:**

  * OLAP systems requiring **fast aggregations, trends, and reports**.

---

### **Star Schema**

* Central **fact table** linked to **dimension tables**.
* **Fact table:** stores **measurable data** like sales, revenue, counts.
* **Dimension tables:** store **descriptive attributes** like customer, product, time.
* **Advantages:** simple, fast for queries.

### **Snowflake Schema**

* A **normalized version** of the star schema.
* Dimensions can be **split into multiple related tables**.
* **Advantages:** reduces data redundancy but queries are slightly more complex.

---

### **Facts and Fact Tables**

* **Facts:** Quantitative data points (e.g., sales amount, order quantity).
* **Fact tables:** Store **facts along with foreign keys** to dimension tables.

---

### **Dimensional Models**

* Designed for **OLAP and reporting**.
* Focus on **user-friendly query performance**.
* Include **facts, dimensions, hierarchies, and measures** for analysis.

---

### **Hadoop and Big Data**

* Big Data requires **scalable storage and processing** for massive datasets.
* **Hadoop** uses a **distributed file system (HDFS)** and **MapReduce or Spark** for computation.
* Dimensional modeling is often used **on top of Big Data platforms** for analytics.

---

### **3NF vs Dimensional Modeling**

| Feature           | 3NF Modeling                         | Dimensional Modeling                 |
| ----------------- | ------------------------------------ | ------------------------------------ |
| Purpose           | OLTP, transactional systems          | OLAP, analytics & reporting          |
| Data Organization | Normalized to reduce redundancy      | Denormalized for fast querying       |
| Tables            | Many small tables with relationships | Fact and dimension tables            |
| Performance       | Optimized for inserts/updates        | Optimized for read/query performance |
| Use Case          | Banking, e-commerce, operational DB  | Data warehouse, BI, dashboards       |

---

## **Data Factory Basic Concepts**

* A **data factory** is a cloud-based or on-premises platform used to **orchestrate, move, and transform data** from multiple sources into analytics-ready formats.
* Supports **ETL (Extract, Transform, Load)** and **ELT (Extract, Load, Transform)** pipelines.
* Helps integrate **structured, semi-structured, and unstructured data** for analytics and machine learning.

---

## **Data Analytics Platform**

* Provides tools and infrastructure for **storing, processing, analyzing, and visualizing data**.
* Typically includes:

  * **Data ingestion & integration** (batch and streaming)
  * **Data storage** (data lake, warehouse, databases)
  * **Analytics & reporting** (BI dashboards, visualizations)
  * **Machine learning & AI pipelines**

---

## **Lambda and Kappa Architectures**

* **Lambda Architecture:**

  * Combines **batch processing** and **streaming processing**.
  * Batch layer stores **master dataset**, computes **batch views**.
  * Speed layer processes **real-time data** for immediate insights.
  * Serving layer merges both for analytics.

* **Kappa Architecture:**

  * Simplifies Lambda by using **only a streaming pipeline**.
  * Stores **raw event streams** and reprocesses them as needed.
  * Avoids maintaining separate batch and speed layers.

### **Key Differences**

| Feature      | Lambda                                   | Kappa                              |
| ------------ | ---------------------------------------- | ---------------------------------- |
| Processing   | Batch + Streaming                        | Streaming only                     |
| Complexity   | Higher                                   | Lower                              |
| Use Case     | When both batch and real-time are needed | When real-time suffices            |
| Reprocessing | Batch layer handles reprocessing         | Stream replay handles reprocessing |

---

## **Streaming / Batch Data Sources**

* **Streaming sources:** IoT sensors, Kafka topics, event logs, API events.
* **Batch sources:** Databases, CSV/Excel files, data lakes, legacy systems.

---

## **Edge / Ingestion**

* **Edge:** Data generated at the source (devices, sensors) or near-source processing.
* **Ingestion:** Moving data from **edge or sources** into storage or pipelines. Can be **real-time (streaming)** or **scheduled (batch)**.

---

## **Data Storage**

* **Data Lake:** Stores **raw, unstructured, or semi-structured data** at scale.
* **Data Warehouse:** Stores **structured, curated, analytics-ready data**.
* **Databases / NoSQL:** For operational and transactional data.

---

## **Analytics Production Pipelines**

* **ETL/ELT Pipelines:** Move and transform data for analytics.
* **Streaming Pipelines:** Process real-time events with frameworks like Spark Streaming, Flink, or Kafka Streams.
* **Batch Pipelines:** Process large datasets periodically (e.g., daily sales aggregation).

---

## **Management Components**

* **Orchestration & Scheduling:** Automates pipeline execution (Airflow, Data Factory).
* **Monitoring & Logging:** Tracks pipeline health, performance, and errors.
* **Data Quality & Governance:** Validates data accuracy, consistency, and compliance.

---

## **Data and ML Exploratory Environment**

* Tools and environments for **data exploration, feature engineering, and model prototyping**.
* Examples: Jupyter Notebooks, Databricks, SageMaker, or local Python/R environments.

---

## **Products / Tools**

* **Data Ingestion & Orchestration:** Apache NiFi, Apache Airflow, Azure Data Factory, Talend
* **Data Storage & Processing:** Hadoop, Spark, BigQuery, Snowflake, AWS S3
* **Streaming:** Kafka, Kinesis, Flink
* **Analytics / BI:** Power BI, Tableau, Looker
* **ML:** Databricks, SageMaker, MLflow

---

## **Access Layer**

* Provides **data to users, applications, or ML models**.
* Can include:

  * **APIs / Data Services** for applications
  * **BI dashboards** for business users
  * **ML feature stores** for data scientists
