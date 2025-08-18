# Introduction to Hadoop

### **Hadoop**

**Definition:**
Hadoop is an open-source framework for **distributed storage and processing of large datasets** across clusters of computers using simple programming models.

**Core Components:**

1. **HDFS (Hadoop Distributed File System)**

   * Stores data across multiple nodes in a **fault-tolerant** way.
   * Splits files into **blocks** (default 128 MB) and replicates them (default 3 copies).

2. **MapReduce**

   * Programming model for **parallel processing** of large datasets.
   * Steps:

     * **Map:** Processes input data into key-value pairs.
     * **Reduce:** Aggregates results by key.

3. **YARN (Yet Another Resource Negotiator)**

   * Resource management and job scheduling layer.
   * Manages cluster resources and runs multiple applications simultaneously.

4. **Hadoop Common**

   * Libraries and utilities needed by other Hadoop modules.

**Key Features:**

* **Scalable:** Handles petabytes of data by adding more nodes.
* **Fault-tolerant:** Data replication ensures no data loss.
* **Cost-effective:** Runs on commodity hardware.
* **Flexible:** Can process structured, semi-structured, and unstructured data.

**Use Cases:**

* Big data analytics
* Log processing
* Data warehousing
* Machine learning pipelines

---

### **Why Hadoop / Problems It Solves**

**1. Problem: Huge Data Volumes**

* Traditional databases can’t handle **petabytes or exabytes** efficiently.
* Hadoop splits data across nodes (HDFS), making **storage and processing scalable**.

**2. Problem: Expensive Storage & Hardware**

* High-performance servers are costly for big data.
* Hadoop runs on **commodity hardware**, lowering costs.

**3. Problem: Processing Large Data Sets**

* Single machines take too long to process huge data.
* Hadoop uses **parallel processing (MapReduce)** across nodes → faster computation.

**4. Problem: Fault Tolerance / Reliability**

* Hardware failures are common in large clusters.
* Hadoop **replicates data across multiple nodes**, ensuring no data loss.

**5. Problem: Variety of Data Types**

* Traditional systems struggle with unstructured/semi-structured data.
* Hadoop can store and process **structured, semi-structured, and unstructured data** (logs, videos, social media).

**6. Problem: Need for Cost-Effective Big Data Analytics**

* Organizations want insights from big data without huge infrastructure costs.
* Hadoop provides a **scalable, distributed, and cost-effective platform** for analytics.

**Summary:**
Hadoop solves **volume, variety, velocity, cost, and fault tolerance challenges** of big data.

---

### **Hadoop Pros and Cons**

**✅ Pros:**

1. **Scalable:** Easily add nodes to handle more data.
2. **Fault-tolerant:** Data replication prevents data loss.
3. **Cost-effective:** Runs on commodity hardware.
4. **Flexible:** Handles structured, semi-structured, and unstructured data.
5. **Parallel processing:** Processes massive datasets quickly with MapReduce.
6. **Open-source:** No licensing cost, large community support.

**❌ Cons:**

1. **Complex to manage:** Requires skilled administrators.
2. **High latency for small data:** Not ideal for low-latency/real-time tasks.
3. **Limited security:** Needs extra tools for authentication, encryption, and auditing.
4. **Inefficient for iterative processing:** MapReduce is slow for repeated computations (better alternatives exist like Spark).
5. **Storage overhead:** Data replication increases storage requirements (default 3x).

---

### **Hadoop Architecture Fundamentals**

#### **1. Hadoop Structure**

* Hadoop is a **master-slave architecture**.
* Core components: **HDFS**, **YARN**, **MapReduce**, **Common libraries**.
* Designed for **distributed storage and parallel processing**.

---

#### **2. HDFS (Hadoop Distributed File System)**

* **Purpose:** Stores huge data across multiple machines reliably.
* **Key Components:**

  * **NameNode (Master)**

    * Manages **metadata** (file structure, block locations).
    * Single point of management (HA NameNode setups exist for fault tolerance).
  * **DataNode (Slave)**

    * Stores actual **data blocks**.
    * Handles read/write requests from clients.
* **Features:**

  * **Data replication** (default 3 copies) → fault-tolerant.
  * **Block-based storage** (default 128 MB blocks).

---

#### **3. YARN (Yet Another Resource Negotiator)**

* **Purpose:** Resource management and job scheduling.
* **Key Components:**

  * **ResourceManager:** Allocates cluster resources.
  * **NodeManager:** Monitors and manages resources on each node.
  * **ApplicationMaster:** Manages execution of individual applications.

---

#### **4. Metastore**

* Stores **metadata for Hive or other data warehousing tools**.
* Contains **schema, table info, and data locations**.
* Optional for Hadoop core, mainly used in **data analytics layers**.

---

#### **5. Parallel Computing**

* Hadoop processes data in **parallel using MapReduce**:

  1. **Map:** Breaks tasks into key-value pairs.
  2. **Shuffle & Sort:** Organizes intermediate data.
  3. **Reduce:** Aggregates results.
* **Advantage:** Efficient processing of huge datasets across nodes.

---

#### **6. Hadoop vs HDFS vs Parallel Computing**

| Feature    | Hadoop                                      | HDFS                    | Parallel Computing             |
| ---------- | ------------------------------------------- | ----------------------- | ------------------------------ |
| Function   | Framework for big data storage & processing | Distributed file system | Processing model               |
| Scope      | Entire ecosystem                            | Storage layer           | Processing layer (MapReduce)   |
| Components | HDFS, YARN, MapReduce, Common               | NameNode, DataNode      | Map, Reduce, Shuffle           |
| Goal       | Store + process big data                    | Reliable data storage   | Fast computation on large data |

---

#### **7. Summary**

* Hadoop = **ecosystem** for **big data storage and processing**.
* HDFS = **reliable distributed storage**.
* YARN = **cluster resource manager**.
* MapReduce = **parallel computation framework**.
* Metastore = **metadata storage for analytics**.
* Advantage: Handles **volume, variety, and velocity** of big data efficiently.

---

### **FSImage & EditLog in HDFS**

HDFS **metadata** is managed by the **NameNode** and stored in two files:

#### **1. FSImage**

* **Definition:** Snapshot of the **entire file system metadata** at a point in time.
* **Contains:**

  * File names, directories
  * Permissions
  * Block locations
  * Ownership and replication info
* **Characteristics:**

  * Persistent on **NameNode storage**
  * Represents **the current state of HDFS**
  * Updated **only when a checkpoint happens** (e.g., via Secondary NameNode)

---

#### **2. EditLog**

* **Definition:** Log of **all changes/transactions** made to the HDFS metadata after the last FSImage snapshot.
* **Contains:**

  * File creation, deletion, renaming
  * Block allocation or replication changes
* **Characteristics:**

  * Append-only log
  * Keeps NameNode metadata **up-to-date in real time**
  * Periodically merged with FSImage during **checkpointing** to reduce size

---

#### **3. How They Work Together**

1. NameNode starts with **FSImage**.
2. Applies all changes from **EditLog** to get the current state.
3. **Checkpointing:** FSImage + EditLog → updated FSImage; EditLog is cleared.

**Analogy:**

* FSImage = full snapshot of your notebook
* EditLog = a running list of edits since the last snapshot

---

### **Hadoop 2.x vs 3.x**

| Feature                | Hadoop 2.x                              | Hadoop 3.x                                                                 |
| ---------------------- | --------------------------------------- | -------------------------------------------------------------------------- |
| **Release Year**       | 2013                                    | 2017                                                                       |
| **HDFS Storage**       | No support for erasure coding           | Supports **erasure coding** → reduces storage overhead                     |
| **YARN**               | Basic resource management               | Supports **GPU scheduling**, container-level resources, better scalability |
| **High Availability**  | Single Active NameNode, manual failover | Improved **HA** with multiple NameNodes and automatic failover             |
| **Scalability**        | Limited node support (\~4,000 nodes)    | Improved scalability (\~10,000+ nodes)                                     |
| **HDFS Federation**    | Supported but basic                     | Better **federation**, multi-namespace support                             |
| **Default Block Size** | 128 MB                                  | 128 MB (configurable)                                                      |
| **Other Features**     | No Docker/container support             | Supports **Docker containers** and **improved YARN features**              |
| **Storage Efficiency** | Replication only (3x)                   | Replication + **erasure coding** → 50% storage saving for cold data        |
| **MapReduce**          | Standard MR                             | MR improvements, better **fault tolerance** and efficiency                 |

---

#### **Summary**

* **Hadoop 3.x** is more **scalable, efficient, and fault-tolerant** than 2.x.
* Key improvements: **erasure coding**, **better YARN scheduling**, **multi-NameNode HA**, **container support**.

---

### **Hadoop Installation: On-Premises vs Cloud**

| Aspect                  | On-Premises                                                          | Cloud                                                                 |
| ----------------------- | -------------------------------------------------------------------- | --------------------------------------------------------------------- |
| **Infrastructure**      | Physical servers in your own data center                             | Virtualized infrastructure on cloud provider (AWS, Azure, GCP)        |
| **Setup Complexity**    | High → install OS, Java, Hadoop, configure HDFS, YARN, etc. manually | Low → managed services (e.g., EMR, Dataproc, HDInsight) available     |
| **Cost**                | High upfront CapEx (hardware, networking, maintenance)               | Pay-as-you-go OpEx → no upfront hardware cost                         |
| **Scalability**         | Limited by physical hardware; adding nodes requires new servers      | Highly scalable; add/remove nodes dynamically                         |
| **Maintenance**         | Managed in-house → upgrades, patching, monitoring, fault tolerance   | Managed by cloud provider → automatic scaling, updates, monitoring    |
| **Fault Tolerance**     | Depends on your own replication and backup strategies                | Cloud providers often provide built-in HA, replication, and backup    |
| **Deployment Speed**    | Slow → hours/days to provision cluster                               | Fast → minutes to launch a cluster via cloud console or APIs          |
| **Flexibility**         | Full control over configuration and hardware                         | Limited by provider’s configuration options, but flexible for scaling |
| **Use Case Preference** | Large, stable workloads with predictable traffic                     | Dynamic workloads, testing, analytics pipelines, temporary clusters   |

---

#### **Summary**

* **On-premises Hadoop**: More control, higher cost, slower to scale, good for stable, long-term workloads.
* **Cloud Hadoop**: Faster deployment, elastic scaling, lower upfront cost, easier maintenance.

---

### **Apache Ambari**

**Definition:**

* Ambari is an **open-source management and monitoring tool for Hadoop clusters**.
* Simplifies **deployment, configuration, monitoring, and maintenance** of Hadoop ecosystem components.

**Key Features:**

1. **Cluster Installation & Setup**

   * Install Hadoop components (HDFS, YARN, Hive, HBase, etc.) on multiple nodes automatically.
2. **Configuration Management**

   * Centralized UI to **configure services and nodes** easily.
3. **Monitoring & Alerts**

   * Tracks cluster health, performance metrics, and triggers alerts for failures.
4. **Service Management**

   * Start, stop, or restart Hadoop services from the dashboard.
5. **REST APIs**

   * Provides APIs for **automation and integration** with other tools.

**Advantages:**

* Simplifies **cluster management** for admins.
* **Reduces manual errors** in setup and configuration.
* Provides **real-time metrics** for proactive monitoring.

**Use Cases:**

* Hadoop cluster deployment and maintenance
* Performance monitoring and alerting
* Managing multiple Hadoop services efficiently

---

### **CDH (Cloudera Distribution for Hadoop) Benefits**

**Definition:**

* CDH is a **commercial Hadoop distribution** by Cloudera that bundles Hadoop ecosystem components with **enterprise-grade features**.

**Key Benefits:**

1. **Pre-integrated Ecosystem**

   * Combines Hadoop core (HDFS, YARN, MapReduce) with tools like **Hive, Impala, HBase, Spark**.
   * Reduces time and effort to assemble components manually.

2. **Enterprise Support & Stability**

   * Professional support from Cloudera.
   * Tested and stable releases suitable for **production workloads**.

3. **Management Tools**

   * Includes **Cloudera Manager** for easy deployment, monitoring, and maintenance of clusters.

4. **Security & Governance**

   * Integrates **Kerberos, Sentry, encryption**, and auditing features.
   * Supports **data governance and compliance** requirements.

5. **Performance Optimizations**

   * Pre-tuned configurations for better **query performance** (Impala, Hive) and **data processing efficiency**.

6. **Scalability & Flexibility**

   * Handles **petabyte-scale datasets**.
   * Supports **hybrid deployments** (on-premises + cloud).

7. **Monitoring & Troubleshooting**

   * Provides **metrics, alerts, and logs** for proactive cluster management.

**Summary:**

* CDH = **enterprise-ready Hadoop distribution** → easier setup, better support, security, performance, and manageability compared to open-source vanilla Hadoop.

---

### **Running Hadoop with Docker**

**Definition:**

* Using **Docker containers** to deploy Hadoop clusters instead of installing directly on physical or virtual machines.

**Key Benefits:**

1. **Easy Deployment**

   * Prebuilt Docker images allow **quick setup of Hadoop clusters**.
   * No need for complex manual installation of HDFS, YARN, or ecosystem components.

2. **Easy Backup**

   * Containers are **portable and self-contained**, making snapshots and backups simpler.
   * Volume mapping allows **persistent storage** outside the container.

3. **Elasticity**

   * Scale up/down by **spinning up or removing containers**.
   * Useful for **testing, development, or temporary clusters** without hardware constraints.

4. **Burstability**

   * Temporary increase in cluster capacity is easy by **adding more containers** on demand.
   * Ideal for **high-demand workloads** without permanent resource allocation.

**Summary:**

* Docker + Hadoop = **fast deployment, easy management, scalable & flexible clusters**.
* Particularly useful for **development, testing, or elastic big data environments**.

---

### **Hadoop in the Cloud: AWS EMR**

**Definition:**

* **Amazon EMR (Elastic MapReduce)** is a **fully managed Hadoop framework** on AWS.
* Allows you to **process vast amounts of data** using Hadoop, Spark, HBase, Presto, Hive, and other ecosystem tools.
* Handles **cluster provisioning, configuration, and management automatically**.

---

### **1. EMR Overview**

* Purpose: Run **big data frameworks** in the cloud without manual setup of Hadoop clusters.
* Managed services features:

  * Automatic **cluster provisioning** and configuration
  * Integration with **S3, DynamoDB, RDS** for storage
  * Supports **elastic scaling** → adjust cluster size dynamically
* Pay for **compute and storage used**, reducing upfront costs.

---

### **2. EMR Architecture**

**High-level components:**

1. **Master Node**

   * Runs **NameNode (HDFS)**, **ResourceManager (YARN)**, and **JobTracker** components.
   * Manages **cluster metadata and job scheduling**.

2. **Core Nodes**

   * Run **DataNode (HDFS)** and **NodeManager (YARN)**.
   * Store **data locally** and execute processing tasks.

3. **Task Nodes (Optional)**

   * Run **NodeManager (YARN)** only; do **not store HDFS data**.
   * Used for **elastic scaling and burst processing**.

4. **Storage Integration**

   * **Amazon S3** acts as persistent storage (HDFS can be ephemeral).
   * Can also connect to **RDS, DynamoDB, or EBS** volumes.

5. **Cluster Management**

   * EMR automatically handles **software installation, patching, monitoring, and logging**.

---

### **3. EMR AWS Integration**

* **S3 Integration** → Read/write datasets directly from S3 instead of HDFS.
* **IAM Roles** → Fine-grained **access control** for EMR clusters.
* **CloudWatch** → Monitor cluster performance and receive alerts.
* **SNS (Simple Notification Service)** → Job completion/failure notifications.
* **VPC** → Launch EMR clusters in a **secure, isolated network**.

---

### **4. What You Give Up With EMR**

1. **Full Control Over Hardware**

   * EMR abstracts nodes; you don’t choose exact machine hardware.
2. **HDFS Permanence**

   * By default, EMR uses **ephemeral HDFS**, so data must be saved in S3 for persistence.
3. **Version/Configuration Control**

   * EMR handles software installation; custom setups may be limited.
4. **Cost Management Complexity**

   * Pay-as-you-go model requires careful **cluster sizing and auto-termination** to avoid surprises.

---

### **5. EMR Use Cases**

1. **Big Data Processing**

   * Process **large datasets** in parallel using Hadoop or Spark.
2. **ETL Pipelines**

   * Extract, transform, and load data from S3, RDS, DynamoDB into analytics platforms.
3. **Machine Learning**

   * Run **ML workloads** with Spark MLlib or integrate with SageMaker.
4. **Data Analytics & Reporting**

   * Use Hive, Presto, or Spark SQL for **interactive queries** on large datasets.
5. **Temporary/Elastic Clusters**

   * Ideal for **batch jobs** or experiments that do not require permanent infrastructure.

---

### **Summary**

* AWS EMR = **Hadoop in the cloud without infrastructure headaches**.
* **Pros:** Easy deployment, scaling, integration with AWS ecosystem, managed services.
* **Cons / Trade-offs:** Less hardware control, ephemeral HDFS, potential cost if not managed carefully.

---

### **Hadoop: Basic Components (Cloud Focus)**

Hadoop in the cloud can be broken into **three main components**: **Processing, Storage, On-Cluster Storage**.

---

### **1. Processing**

* **Definition:** Frameworks/tools that **perform computation** on large datasets in a distributed manner.
* **Components in Hadoop Ecosystem:**

  1. **MapReduce** – Traditional batch-processing engine.

     * Splits tasks across multiple nodes → parallel processing.
  2. **Apache Spark** – Faster, in-memory processing engine.

     * Supports **batch, streaming, ML, and graph processing**.
  3. **Hive/Impala** – SQL-like query engines for analytics.
  4. **HBase** – NoSQL database for real-time read/write workloads.
* **Cloud Integration:**

  * Cloud Hadoop services (like **AWS EMR, GCP Dataproc, Azure HDInsight**) automatically configure processing engines.
  * Processing can directly read/write **S3, Blob Storage, or object storage**.

---

### **2. Storage**

* **Definition:** Persistent storage for large datasets, usually **distributed** across nodes.
* **Traditional HDFS:** Distributed across cluster nodes (blocks, replication).
* **Cloud Storage Options:**

  * **Amazon S3 (AWS)** – Object storage, persistent, scalable.
  * **Google Cloud Storage (GCP)** – Same purpose, integrates with Dataproc/Spark.
  * **Azure Blob Storage** – Supports Hadoop-compatible APIs.
* **Advantage of cloud storage:**

  * Decouples storage from compute → cluster can be ephemeral.
  * Eliminates HDFS replication overhead → storage-efficient.

---

### **3. On-Cluster Storage**

* **Definition:** Temporary storage **within the compute cluster** (ephemeral).
* **Role:**

  * Used for intermediate data processing (e.g., MapReduce shuffle, Spark RDD caching).
  * Provides **fast local I/O** during computation.
* **Cloud Considerations:**

  * On-cluster storage is usually **ephemeral EBS, local SSD, or instance storage**.
  * Data must be persisted to **S3, Blob, or other persistent storage** to survive cluster termination.
* **Example:** EMR uses **HDFS on core nodes** for temporary storage, then moves results to S3.

---

### **Summary**

| Component              | Purpose                       | Cloud Implementation                                                       |
| ---------------------- | ----------------------------- | -------------------------------------------------------------------------- |
| **Processing**         | Compute/analytics             | MapReduce, Spark, Hive, HBase via EMR, Dataproc, HDInsight                 |
| **Storage**            | Persistent data storage       | S3, GCS, Azure Blob (object storage)                                       |
| **On-Cluster Storage** | Temporary computation storage | Ephemeral HDFS, instance storage, local SSD, used for intermediate results |

**Key Concept:** In cloud Hadoop: **storage and compute are often decoupled**, allowing **elastic clusters, easier backups, and better cost management**.

---

### **Advantages of Hadoop on Amazon EMR**

1. **Fully Managed Service**

   * AWS handles **provisioning, configuration, patching, and maintenance** of Hadoop clusters.
   * Reduces administrative overhead significantly.

2. **Elastic Scaling**

   * Add or remove nodes dynamically based on workload.
   * Supports **burst workloads** without permanent infrastructure.

3. **Cost Efficiency**

   * Pay-as-you-go model → only pay for resources used.
   * Use **spot instances** for further cost savings.

4. **Integration with AWS Ecosystem**

   * Direct access to **S3 (storage), RDS/DynamoDB (databases), Redshift (data warehouse), CloudWatch (monitoring)**.
   * Simplifies **data ingestion, analytics, and ML workflows**.

5. **High Availability & Fault Tolerance**

   * Supports **multi-AZ deployment**, automatic failure recovery.
   * HDFS data can be stored in **S3 for persistence**, reducing dependency on cluster nodes.

6. **Flexible Framework Support**

   * Supports **Hadoop, Spark, Hive, HBase, Presto, Flink, MLlib**, etc.
   * Allows choosing the right tool for each workload.

7. **Security & Compliance**

   * Integrates with **IAM, KMS, encryption, VPC**, and audit logging.
   * Helps meet **enterprise security and compliance requirements**.

8. **Fast Deployment & Experimentation**

   * Launch clusters in **minutes**, ideal for temporary, test, or development clusters.
   * Reduces time-to-insight for **big data analytics**.

9. **Monitoring & Automation**

   * Integration with **CloudWatch, CloudTrail, and SNS** for metrics, logging, and alerts.
   * Supports **auto-termination** to prevent unnecessary costs.

---

**Summary:**

* **Hadoop on EMR = fast deployment + elastic scaling + AWS integration + cost efficiency + managed maintenance**.
* Ideal for **big data analytics, ETL pipelines, machine learning, and temporary workloads**.

---

### **Hadoop in the Cloud: GCP vs AWS vs Azure**

| Cloud     | Service                     | Strengths / Arguments                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **AWS**   | **EMR (Elastic MapReduce)** | - **Fully managed Hadoop cluster** → no manual setup. <br> - **Elastic scaling**: add/remove nodes easily, supports burst workloads. <br> - **Integration with AWS ecosystem**: S3, Redshift, RDS, DynamoDB, CloudWatch. <br> - **Flexible frameworks**: Hadoop, Spark, Hive, HBase, Presto, Flink. <br> - **Cost control**: pay-as-you-go, spot instances. <br> - **High availability**: multi-AZ deployment, persistent storage in S3.                                                    |
| **Azure** | **HDInsight**               | - **Managed Hadoop and big data services** on Azure. <br> - Supports **Hadoop, Spark, Hive, HBase, Kafka, Storm**. <br> - **Blob Storage / Data Lake Storage** as persistent storage → decouples compute & storage. <br> - **Enterprise security**: Azure AD, encryption, RBAC, network isolation. <br> - **Elasticity**: scale clusters up/down for temporary workloads. <br> - **Integrated with Azure ecosystem** → Power BI, ML services, SQL Data Warehouse.                           |
| **GCP**   | **Dataproc**                | - **Managed Hadoop/Spark service** with **fast cluster creation (\~90 sec)**. <br> - **Pay-per-second billing** → cost-efficient for short workloads. <br> - **Deep integration with Google Cloud Storage, BigQuery, Bigtable, Pub/Sub**. <br> - **Elastic & ephemeral clusters** → ideal for temporary or burst workloads. <br> - Supports **open-source Hadoop/Spark tools** → easy migration from on-premises Hadoop. <br> - **Simpler pricing & scaling** than EMR for ad-hoc clusters. |

---

### **Arguments Summary**

**AWS EMR:**

* Best if you are already in **AWS ecosystem**.
* Good for **large-scale, production-grade clusters** with enterprise support and multiple framework options.

**Azure HDInsight:**

* Best for **Microsoft-centric environments**.
* Strong **enterprise security and governance**, good integration with **Power BI & Azure ML**.

**GCP Dataproc:**

* Best for **fast, short-lived clusters** and **data analytics pipelines**.
* **Cost-efficient** for ephemeral workloads and integrates well with **BigQuery** for analytics.

---

**Quick Takeaway:**

* **AWS:** Production-scale, flexible, widely used.
* **Azure:** Enterprise security & Microsoft ecosystem.
* **GCP:** Fast, elastic, cost-efficient, analytics-focused.

---

### **Databricks**

**Definition:**

* **Databricks** is a **unified data analytics platform** built on **Apache Spark**.
* Provides a **cloud-based environment** for big data processing, machine learning, and AI workflows.
* Designed to simplify **data engineering, data science, and analytics** in one platform.

---

### **Key Features**

1. **Unified Analytics Platform**

   * Combines **data engineering, ETL, BI, ML, and AI workflows**.
   * Supports **batch and real-time processing**.

2. **Apache Spark Powered**

   * Leverages **Spark’s distributed processing** for large-scale data.
   * Supports **Python, R, SQL, Scala, and Java** APIs.

3. **Cloud-Native & Managed**

   * Runs on **AWS, Azure, or GCP**.
   * Handles **cluster provisioning, scaling, and maintenance** automatically.

4. **Collaborative Workspace**

   * Interactive **notebooks** for data exploration, visualization, and coding.
   * Supports **multi-user collaboration** for data teams.

5. **Machine Learning & AI Integration**

   * Provides **MLflow** for model tracking and deployment.
   * Integrates with **TensorFlow, PyTorch, Scikit-learn**.

6. **Data Lake & Warehouse Integration**

   * Works with **Delta Lake** for ACID-compliant data storage.
   * Integrates with **S3, Azure Data Lake, GCS, Snowflake**, and other data sources.

---

### **Advantages**

* **Unified platform** → data engineering + analytics + ML in one place.
* **Scalable & elastic** → automatic cluster scaling.
* **Simplifies Spark** → no need to manage clusters manually.
* **Collaboration** → notebooks and shared workflows for teams.
* **Delta Lake support** → reliable, transactional big data storage.

---

**Summary:**

* **Databricks = Managed Spark + Collaborative Data Platform + ML/AI Workflows**.
* Ideal for **big data analytics, ETL pipelines, machine learning, and AI in the cloud**.

---

### **Databricks Benefits**

1. **Performance**

   * Optimized **Apache Spark engine** for fast distributed processing.
   * **Delta Lake** ensures **ACID transactions** → avoids errors and improves query speed.
   * Supports **in-memory computing** for faster analytics and ML workflows.

2. **Cost-Effective**

   * **Auto-scaling clusters** → only pay for resources used.
   * **Spot/preemptible instance support** reduces cloud costs.
   * Combines **storage + compute optimization** (Delta Lake, caching) → efficient resource usage.

3. **Simplicity**

   * Fully **managed cloud platform** → no manual cluster management.
   * **Unified workspace** for ETL, analytics, and ML → reduces complexity.
   * **Collaborative notebooks** → easier teamwork and faster development cycles.

---

**Summary:**

* **Databricks = high performance + cost efficiency + simple, collaborative cloud platform**.
* Ideal for **big data processing, machine learning, and analytics**.

---

### **Databricks Key Features**

1. **Caching**

   * Stores **intermediate results in memory** to speed up repeated queries.
   * Reduces I/O operations and improves **query performance**.

2. **Z-Order Clustering**

   * Optimizes **data layout in storage** for faster queries.
   * Reduces **scan times** by clustering related data together.

3. **Join Optimization**

   * Automatic optimization for **data joins** in Spark queries.
   * Supports **broadcast joins, shuffle optimizations**, and query plan tuning.

4. **High Availability (HA)**

   * **Managed clusters** with automatic failover.
   * Ensures **continuous availability** of compute and storage.

5. **Notifications & Alerts**

   * Integration with **email, Slack, or monitoring tools**.
   * Alerts on **job success/failure, cluster health, and performance issues**.

6. **Flexible Job Types**

   * Supports **batch jobs, streaming jobs, ML workflows, and interactive queries**.
   * Jobs can be scheduled or triggered programmatically.

7. **Optimized Data Sources**

   * Works efficiently with **Delta Lake, Parquet, Avro, ORC, JSON, and CSV**.
   * Delta Lake enables **ACID transactions and time travel** for reliable analytics.

8. **Delta Lake**

   * Provides **reliable, transactional storage** for big data.
   * Supports **schema enforcement, versioning, and rollback**.

9. **Collaborative Notebooks**

   * Supports **Python, R, SQL, Scala, Java** in the same environment.
   * Multi-user collaboration for **data engineering, analytics, and ML**.

10. **Auto-scaling & Elasticity**

    * Clusters automatically scale **up or down** based on workload.
    * Supports **cost-efficient burst processing**.

11. **Security & Governance**

    * Integrates with **IAM, role-based access control, encryption**, and audit logging.
    * Supports enterprise **compliance and governance requirements**.

12. **Machine Learning & AI Integration**

    * Supports ML frameworks like **TensorFlow, PyTorch, Scikit-learn**.
    * MLflow integration for **tracking experiments and deploying models**.

---

**Summary:**

* Databricks provides a **high-performance, scalable, and collaborative platform** for big data analytics, ETL, and machine learning.
* Key advantages come from **optimized storage (Delta Lake, Z-order), query performance (caching, join optimization), flexibility (job types, scaling), and enterprise features (HA, security, notifications)**.

---

### **Hadoop Overview: Open-Source, Distributions, and Cloud**

#### **1. Hadoop Open-Source**

* **Definition:** Vanilla Hadoop released under **Apache License**, free to use and modify.
* **Components:** HDFS, YARN, MapReduce, Hadoop Common libraries.
* **Pros:**

  * Free and fully open-source.
  * Large community support.
  * Can be customized for specific needs.
* **Cons:**

  * Manual setup and configuration required.
  * No enterprise support.
  * Harder to manage for large clusters.

---

#### **2. Pre-Built Hadoop Distributions**

* **Definition:** Enterprise-ready Hadoop bundles with additional tools and management features.
* **Examples:**

  * **CDH (Cloudera Distribution for Hadoop)**
  * **HDP (Hortonworks Data Platform)** → now merged with Cloudera
  * **MapR (now HPE Ezmeral Data Platform)**
* **Features:**

  * Pre-integrated ecosystem: Hive, Spark, HBase, Impala, Kafka.
  * Enterprise-grade support, security, monitoring.
  * Simplifies deployment and maintenance with management tools (e.g., Cloudera Manager).
* **Pros:**

  * Faster setup, less operational complexity.
  * Optimized performance and security.
  * Supported in production environments.

---

#### **3. Hadoop in the Cloud**

* **Definition:** Hadoop clusters running on **cloud platforms** instead of on-premises hardware.
* **Key Services:**

  * **AWS EMR** → managed Hadoop, Spark, Hive, integration with S3, Redshift.
  * **Azure HDInsight** → managed Hadoop/Spark clusters, integration with Azure Blob Storage and Data Lake.
  * **GCP Dataproc** → fast, ephemeral Hadoop/Spark clusters, integrated with GCS and BigQuery.
* **Benefits:**

  * No manual cluster management → cloud handles provisioning, patching, monitoring.
  * Elastic scaling → add/remove nodes on demand.
  * Cost-effective → pay-as-you-go, ephemeral clusters for short workloads.
  * Integrates with cloud ecosystem → storage, ML, analytics tools.
* **Considerations:**

  * Less direct hardware control.
  * Storage and compute may be separate → requires S3/Blob/GCS for persistence.

---

### **Summary**

| Type                       | Pros                                          | Cons                                               | Use Case                                                         |
| -------------------------- | --------------------------------------------- | -------------------------------------------------- | ---------------------------------------------------------------- |
| **Open-Source**            | Free, customizable, community support         | Manual setup, no enterprise support                | Learning, small clusters, experimentation                        |
| **Pre-Built Distribution** | Enterprise support, optimized, pre-integrated | Licensing cost, less flexible than raw open-source | Production workloads, enterprises                                |
| **Cloud Hadoop**           | Managed service, scalable, cost-efficient     | Less hardware control, ephemeral storage           | Big data pipelines, analytics, ML, temporary or elastic clusters |

---

### **Hadoop HDFS Architecture**

HDFS follows a **Master-Slave architecture** with three main components: **NameNode, Secondary NameNode, and DataNode**.

---

#### **1. NameNode (Master Node)**

* **Role:** Central **metadata manager** of HDFS.
* **Responsibilities:**

  * Stores metadata: file names, directories, permissions, and block locations.
  * Manages **namespace operations**: create, delete, rename files/directories.
  * Coordinates client read/write operations with DataNodes.
* **Characteristics:**

  * Single point of failure in Hadoop 1.x (HA NameNode added in Hadoop 2.x+).
  * Does **not store actual file data**, only metadata.

---

#### **2. Secondary NameNode**

* **Role:** Assists NameNode by **checkpointing metadata**.
* **Responsibilities:**

  * Periodically merges **FSImage + EditLog** to create a new FSImage.
  * Reduces NameNode recovery time after failure.
* **Important Note:**

  * Does **not act as a failover NameNode**.
  * Only maintains metadata checkpoints for faster recovery.

---

#### **3. DataNode (Slave Node)**

* **Role:** Stores **actual data blocks** of HDFS files.
* **Responsibilities:**

  * Handles **read/write requests** from clients.
  * Reports **block information** to NameNode periodically via heartbeat.
  * Performs **block replication** based on NameNode instructions.
* **Characteristics:**

  * Multiple DataNodes per cluster → scalable storage.
  * Failure of a DataNode triggers automatic replication to other nodes.

---

### **How They Work Together**

1. **Client wants to write a file:**

   * Contact NameNode → get block allocation → write blocks to DataNodes.
2. **Client wants to read a file:**

   * Contact NameNode → get block locations → read from DataNodes.
3. **Metadata maintenance:**

   * NameNode updates EditLog → Secondary NameNode periodically merges to FSImage.
4. **Fault tolerance:**

   * DataNodes replicate blocks → NameNode monitors replication.

---

### **Summary Table**

| Component          | Role   | Stores              | Key Function                                            |
| ------------------ | ------ | ------------------- | ------------------------------------------------------- |
| NameNode           | Master | Metadata            | File system namespace, block locations                  |
| Secondary NameNode | Helper | FSImage checkpoints | Merges FSImage + EditLog, assists recovery              |
| DataNode           | Slave  | Actual data blocks  | Read/write blocks, report to NameNode, replicate blocks |

---

### **Hadoop High Availability (HA)**

**Definition:**

* High Availability ensures that **HDFS and NameNode services continue working** even if a NameNode fails.
* Eliminates the **single point of failure (SPOF)** problem of traditional Hadoop 1.x clusters.

---

### **1. HA Overview**

* Traditional Hadoop: **Single NameNode → SPOF**.
* HA Hadoop: **Two NameNodes** (Active + Standby) with **shared storage or quorum-based coordination**.
* **Goal:** Continuous availability of HDFS metadata.

---

### **2. Manual Failover**

* **Definition:** Administrator manually switches from **failed Active NameNode to Standby NameNode**.
* **Process:**

  1. Detect Active NameNode failure.
  2. Manually start Standby NameNode as Active.
* **Pros:** Simple to implement.
* **Cons:** Requires human intervention → downtime until failover.

---

### **3. Automatic Failover**

* **Definition:** Hadoop automatically switches from **Active to Standby NameNode** using **ZooKeeper**.
* **Components:**

  * **ZooKeeper Quorum** → monitors Active NameNode heartbeat.
  * **Failover Controllers** → coordinate switching to Standby.
* **Advantages:**

  * No manual intervention → **minimal downtime**.
  * Continuous HDFS availability even if Active NameNode fails.

---

### **HA Architecture**

1. **Active NameNode** → serves client requests.
2. **Standby NameNode** → keeps metadata in sync via **EditLog replication or shared storage**.
3. **ZooKeeper** → monitors NameNodes and triggers automatic failover.
4. **Shared Storage or Quorum Journal Manager (QJM)** → ensures both NameNodes have consistent metadata.

---

### **Summary Table**

| HA Type      | Failover Method                 | Pros                        | Cons                         |
| ------------ | ------------------------------- | --------------------------- | ---------------------------- |
| Manual HA    | Admin switches Active → Standby | Simple                      | Downtime, human intervention |
| Automatic HA | ZooKeeper + Failover Controller | Minimal downtime, automatic | More complex setup           |

---

**Key Concept:**

* **Hadoop HA = two NameNodes (Active + Standby) + failover mechanism (manual or automatic)** → ensures reliable HDFS service and avoids SPOF.

---

### **Hadoop HA Metadata Storage Options**

Hadoop HA requires **metadata consistency between Active and Standby NameNodes**. Two common approaches:

---

### **1. Shared Storage (Traditional Approach)**

* **Definition:** Both NameNodes (Active & Standby) access a **single shared storage** for HDFS metadata (FSImage + EditLog).
* **How it works:**

  1. Active NameNode writes changes (EditLog) to shared storage.
  2. Standby NameNode reads from shared storage → stays in sync.
* **Pros:**

  * Simple to implement.
  * Works with manual failover.
* **Cons:**

  * **Single point of failure** → if shared storage fails, metadata is lost.
  * Not fully scalable or fault-tolerant.

---

### **2. Quorum Journal Nodes (QJM)**

* **Definition:** Distributed journal nodes that maintain **EditLogs in a replicated, fault-tolerant manner**.
* **Components:**

  * 3 or 5 JournalNodes → maintain replicated EditLogs.
  * Both Active and Standby NameNodes write to QJM.
* **How it works:**

  1. Active NameNode writes EditLogs to **all JournalNodes**.
  2. Standby NameNode reads EditLogs from QJM → stays synchronized.
  3. Automatic failover possible using **ZooKeeper + Failover Controller**.
* **Pros:**

  * No single point of failure → highly available.
  * Supports **automatic failover**.
  * Scalable and distributed → suitable for large clusters.
* **Cons:**

  * Slightly more complex setup than shared storage.
  * Requires multiple nodes for quorum.

---

### **Comparison Table**

| Feature          | Shared Storage           | Quorum Journal Nodes (QJM)               |
| ---------------- | ------------------------ | ---------------------------------------- |
| Storage Type     | Single shared disk       | Distributed across multiple JournalNodes |
| Fault Tolerance  | Low                      | High (replicated, fault-tolerant)        |
| Failover         | Manual or semi-automatic | Automatic via ZooKeeper                  |
| Scalability      | Limited                  | High (distributed)                       |
| Setup Complexity | Simple                   | Moderate                                 |

---

**Key Concept:**

* **Shared Storage:** simple but SPOF risk.
* **QJM:** recommended for **production HA clusters** → supports automatic failover and distributed fault tolerance.

---

### **Hadoop Real-World Use Cases**

Hadoop is widely used in **big data processing, analytics, and storage** across industries.

---

### **1. Data Warehousing & Analytics**

* **Problem:** Massive structured/unstructured data that traditional RDBMS cannot handle.
* **Hadoop Use:** Store and process terabytes/petabytes of data.
* **Example:**

  * **Yahoo, Facebook:** Log analytics to understand user behavior.
  * **Netflix:** Analyze viewing patterns to optimize recommendations.

---

### **2. ETL (Extract, Transform, Load)**

* **Problem:** Need to process diverse, large datasets from multiple sources.
* **Hadoop Use:**

  * Ingest data from databases, logs, APIs.
  * Transform using Spark or MapReduce.
  * Load into HDFS, Hive, or cloud data warehouses.
* **Example:**

  * **Financial institutions:** Process transaction logs for fraud detection.
  * **Retail:** Aggregate sales and inventory data.

---

### **3. Machine Learning & AI**

* **Problem:** Training ML models on huge datasets is slow or impossible on single machines.
* **Hadoop Use:**

  * Store training data in HDFS.
  * Use Spark MLlib or Hadoop MapReduce for distributed ML.
* **Example:**

  * **Uber:** Predict demand and optimize pricing.
  * **Amazon:** Recommendation systems.

---

### **4. Log & Event Processing**

* **Problem:** Huge volumes of logs from servers, applications, and IoT devices.
* **Hadoop Use:**

  * Collect, store, and analyze logs.
  * Detect anomalies, errors, or patterns.
* **Example:**

  * **LinkedIn:** Analyze server logs to monitor system health.
  * **Telecom companies:** Monitor network traffic and outages.

---

### **5. Social Media & Sentiment Analysis**

* **Problem:** Analyze unstructured text, images, videos at massive scale.
* **Hadoop Use:**

  * Store unstructured social media data.
  * Analyze sentiment, trends, and user engagement using Spark or Hive.
* **Example:**

  * **Twitter:** Real-time sentiment analysis and trend detection.
  * **Marketing companies:** Customer sentiment analysis across platforms.

---

### **6. Fraud Detection & Security Analytics**

* **Problem:** Detect fraudulent activities across millions of transactions or events.
* **Hadoop Use:**

  * Process large transaction datasets.
  * Apply pattern detection and ML models.
* **Example:**

  * **Banks/credit card companies:** Detect unusual spending patterns.
  * **Insurance companies:** Identify fraudulent claims.

---

### **7. Genomics & Healthcare**

* **Problem:** Analyze genome sequences, medical records, imaging data.
* **Hadoop Use:**

  * Store and process massive bioinformatics datasets.
  * Parallel processing for pattern recognition and disease prediction.
* **Example:**

  * **Healthcare research:** Genome sequencing analysis.
  * **Pharmaceuticals:** Drug discovery using large datasets.

---

### **Summary Table**

| Use Case              | Industry           | Hadoop Role                                 |
| --------------------- | ------------------ | ------------------------------------------- |
| Data Analytics        | Tech, Media        | Log processing, recommendations             |
| ETL                   | Finance, Retail    | Large-scale data ingestion & transformation |
| ML & AI               | Tech, Ride-hailing | Distributed model training                  |
| Log/Event Processing  | Telecom, Web       | Monitoring & anomaly detection              |
| Social Media Analysis | Marketing, Media   | Sentiment & trend detection                 |
| Fraud Detection       | Banking, Insurance | Pattern recognition, anomaly detection      |
| Genomics/Healthcare   | Healthcare, Pharma | Big data processing for research            |

---

**Key Concept:** Hadoop excels when **data volume is massive, data types are diverse, and distributed processing is required**.

---

