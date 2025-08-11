# Cloud Overview

## *Cloud Core Concepts*

### **What is the Cloud**

* The cloud is the delivery of computing services — such as servers, storage, databases, networking, software, analytics, and intelligence — over the internet (“the cloud”) instead of on local infrastructure.
* It enables on-demand access to shared computing resources without direct management of the physical hardware.
* Services are typically provided by cloud vendors through data centers located worldwide.

---

### **Benefits of Cloud Computing**

* **Cost Efficiency** – Reduces capital expenditure by replacing physical infrastructure with pay-as-you-go or subscription models.
* **Scalability** – Allows resources to scale up or down automatically or manually based on demand.
* **Elasticity** – Quickly adapts to workload changes, adding or releasing resources in real time.
* **Service Variety** – Offers a wide range of services including compute, storage, AI/ML, IoT, analytics, and developer tools.
* **Reliability** – Provides high availability, disaster recovery, and global redundancy to ensure minimal downtime.
* **Security** – Implements advanced security controls, compliance standards, and encryption to protect data and workloads.

---

### **Cloud Types**

* **Private Cloud** – Cloud infrastructure dedicated to a single organization, offering greater control, security, and customization. Hosted either on-premises or by a third-party provider.
* **Public Cloud** – Cloud resources owned and operated by a third-party provider and shared across multiple customers, accessible via the internet.
* **Hybrid Cloud** – Combination of private and public clouds, allowing data and applications to be shared between them for flexibility and workload optimization.
* **Multi-Cloud** – Use of multiple public cloud providers simultaneously to avoid vendor lock-in, improve resilience, and optimize service selection.

---

## *Cloud Service Models*

### **Infrastructure as a Service (IaaS)**

* Provides virtualized computing resources over the internet, including servers, storage, networking, and virtualization layers.
* Users manage the operating system, applications, and data, while the provider manages the hardware and virtualization.
* **Examples** – Amazon EC2, Google Compute Engine, Microsoft Azure Virtual Machines.
* **When to Use** – When you need full control over the OS and environment, want to run custom applications, or need to migrate legacy systems to the cloud.
* **When Not to Use** – When you want to focus only on application development without managing infrastructure or OS-level tasks.

---

### **Platform as a Service (PaaS)**

* Offers a platform with hardware, OS, runtime, and development tools so developers can build, test, and deploy applications without managing the underlying infrastructure.
* Provider manages infrastructure, OS, runtime, and scaling; user manages code and data.
* **Examples** – Google App Engine, Azure App Service, AWS Elastic Beanstalk.
* **When to Use** – When you want to accelerate development, focus on coding without worrying about servers, and deploy quickly.
* **When Not to Use** – When you need deep customization of the OS, runtime, or hardware resources.

---

### **Software as a Service (SaaS)**

* Delivers fully functional software applications over the internet, accessible via web browsers or APIs.
* Provider manages everything, including application updates, scaling, and security.
* **Examples** – Google Workspace, Microsoft 365, Salesforce, Zoom.
* **When to Use** – When you want ready-to-use software without installation or maintenance, and when scalability and remote accessibility are priorities.
* **When Not to Use** – When you require full control over the application’s source code or need extensive customization beyond what the SaaS provider allows.

---

## *Containers and Serverless*

### **Containers**

* Containers are lightweight, portable units that package an application with all its dependencies, ensuring it runs consistently across environments.
* They share the host OS kernel but are isolated from other containers, improving resource efficiency compared to virtual machines.
* Containers support fast deployment, scaling, and rollback.

---

### **Docker**

* Docker is a platform for developing, shipping, and running applications inside containers.
* It standardizes how containers are built and run, making them easy to use in development, testing, and production environments.

---

### **Docker Engine**

* **Docker Daemon** – The background service that builds, runs, and manages Docker containers.
* **REST API** – Interface that allows programs to communicate with the Docker Daemon.
* **Docker CLI** – Command-line tool to interact with Docker (e.g., `docker run`, `docker build`).

---

### **Kubernetes**

* Kubernetes is an open-source container orchestration platform that automates deployment, scaling, and management of containerized applications.
* It manages clusters of nodes and ensures high availability, load balancing, and self-healing of workloads.
* Supports rolling updates, service discovery, and secret/config management.

---

### **Serverless Computing**

* Serverless allows developers to run code without managing servers or infrastructure.
* Cloud provider handles provisioning, scaling, and availability; users only pay for execution time.
* Best for event-driven workloads like APIs, background jobs, and real-time processing.
* Examples: AWS Lambda, Azure Functions, Google Cloud Functions.

---

### **12-Factor App**

* A methodology for building cloud-ready applications that are portable, scalable, and maintainable.
* Principles include codebase tracking in version control, dependency isolation, configuration in environment variables, stateless processes, and automated build/deploy pipelines.

---

### **Cloud-Native Applications**

* Applications designed specifically for cloud environments, leveraging containerization, microservices, serverless, and DevOps practices.
* They are resilient, scalable, and optimized for distributed cloud infrastructure.
* Often built following the 12-Factor App principles.

---

## *Cloud Ownership*

### **Cloud Ownership Models**

* **Public Cloud** – Infrastructure owned and operated by a third-party provider and shared among multiple customers.
* **Private Cloud** – Infrastructure dedicated to a single organization, offering greater control and security. Hosted on-premises or by a third party.
* **Hybrid Cloud** – Combination of public and private clouds, enabling workload portability and flexibility.
* **Multi-Cloud** – Use of multiple public cloud providers to improve resilience, avoid vendor lock-in, and optimize services.

---

## **Adopting a Cloud Solution**

### **1. Assessment**

* Evaluate existing infrastructure, workloads, and business needs to determine cloud readiness.
* **Cloud Economics** – Analyze total cost of ownership (TCO), potential cost savings, and return on investment (ROI).
* Identify compliance, security, and performance requirements before choosing a provider.

---

### **2. Preparation**

* Develop a **Cloud Migration Strategy** outlining objectives, timelines, and risk management plans.
* Decide on a target architecture (public, private, hybrid, or multi-cloud).
* Select migration tools and providers based on workload needs and cost considerations.

---

### **3. Migration**

#### **Approaches**

* **Rehosting (“Lift and Shift”)** – Move applications with minimal changes.
* **Replatforming** – Make small optimizations for cloud efficiency without full redesign.
* **Refactoring/Re-architecting** – Redesign applications to take full advantage of cloud-native features.
* **Repurchasing** – Move to SaaS alternatives.
* **Retiring** – Decommission obsolete applications.
* **Retaining** – Keep certain workloads on-premises for compliance or performance reasons.

#### **Process**

* Plan migration sequence and prioritize workloads.
* Perform testing in a staging environment before production cutover.
* Execute migration in phases to reduce downtime and risk.

---

### **4. Cloud Operations**

* Post-migration activities include monitoring performance, managing costs, ensuring security, and scaling resources.
* Use cloud-native monitoring and automation tools for visibility and efficiency.

---

### **CloudOps Best Practices**

* Implement cost management policies and resource tagging for transparency.
* Automate provisioning, scaling, and backups.
* Maintain strong identity and access management (IAM) controls.
* Continuously monitor performance, security, and compliance.
* Adopt DevOps practices for faster, reliable deployments.

---