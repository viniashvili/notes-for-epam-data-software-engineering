# DevOps

## *DevOps Basics*

### **What is DevOps**

* DevOps is a cultural and technical movement that combines software development (Dev) and IT operations (Ops) to shorten the development lifecycle and deliver high-quality software continuously.
* It emphasizes collaboration, automation, continuous integration, continuous delivery, and monitoring.
* The goal is to improve deployment frequency, reliability, and faster time to market.

---

### **Implementing DevOps**

* Break down silos between development, operations, QA, and security teams.
* Adopt automation tools for building, testing, and deploying software.
* Use continuous integration/continuous delivery (CI/CD) pipelines to automate code integration and deployment.
* Embrace a culture of shared responsibility and continuous improvement.

---

### **DevOps Practices**

* **Continuous Integration (CI)** – Developers frequently merge code changes into a central repository, triggering automated builds and tests.
* **Continuous Delivery (CD)** – Automated release processes that make software deployments reliable and repeatable.
* **Infrastructure as Code (IaC)** – Managing and provisioning infrastructure through machine-readable configuration files rather than manual processes.
* **Monitoring and Logging** – Collect and analyze metrics and logs to detect issues proactively.
* **Collaboration and Communication** – Foster transparency and cross-team cooperation.

---

### **Infrastructure as Code (IaC)**

* IaC is the practice of managing infrastructure (servers, networks, storage) using code and automation tools.
* Enables version control, repeatability, and faster provisioning of environments.
* Common tools include Terraform, AWS CloudFormation, Ansible, and Puppet.
* Helps achieve consistent environments across development, testing, and production.

---

## *CI & CD (Continuous Integration & Continuous Delivery/Deployment)*

### **Introduction**

* CI/CD is a set of practices aimed at automating the software delivery process to improve code quality and speed up releases.
* Continuous Integration (CI) focuses on integrating code changes frequently and automatically testing them.
* Continuous Delivery (CD) automates preparing code for release, ensuring it can be deployed reliably at any time.
* Continuous Deployment extends CD by automatically deploying code to production after passing tests.

---

### **Continuous Integration (CI)**

* Continuous Integration (CI) is a development practice where developers regularly merge their code changes into a shared repository.
* Each integration triggers an automated process that builds the software and runs tests to detect integration issues early.
* CI helps maintain a healthy codebase, reduces integration problems, and speeds up development.

#### **Version Control Systems and Branching Workflows**

* Use version control systems (e.g., Git) to manage code changes collaboratively.
* Branching workflows (e.g., GitFlow, feature branches, trunk-based development) organize how developers isolate and merge code.
* CI systems automatically build and test code when changes are pushed to branches.

#### **Continuous Inspection**

* Automated tools analyze code for bugs, vulnerabilities, and code smells during the CI process.
* Improves code quality by catching issues early before integration.

#### **Improving Code Quality**

* Incorporates unit tests, integration tests, and static code analysis in CI.
* Encourages test-driven development (TDD) and code reviews.

#### **Artifact**

* Successful builds produce artifacts—versioned packages or binaries ready for deployment.
* Artifacts are stored in repositories (e.g., Nexus, Artifactory) for reuse in later stages.

---

### **Continuous Delivery (CD)**

* Automates the release process so that code is always in a deployable state.
* Includes additional testing stages like performance, security, and user acceptance tests.
* Deployment to production is a manual step but can be triggered quickly and reliably.

---

### **Continuous Deployment**

* Extends Continuous Delivery by automating deployment to production without manual intervention.
* Requires high confidence in automated testing and monitoring to detect and roll back failures quickly.

---

### **CI/CD Pipelines**

* A sequence of automated steps including building, testing, packaging, and deploying code.
* Pipelines define workflows and dependencies between stages.
* Tools include Jenkins, GitLab CI/CD, CircleCI, Travis CI, Azure DevOps.

---

### **CI/CD Pros and Cons**

#### **Pros**

* Faster feedback cycles leading to early bug detection.
* Improved code quality and consistency.
* Reduced manual errors in deployment.
* Faster release cycles and ability to deploy frequently.

#### **Cons**

* Requires investment in automation and tooling.
* Initial setup complexity can be high.
* Risk of deploying faulty code if tests are insufficient.
* Cultural change needed for teams to adapt to continuous practices.

---

## *Jenkins Pipeline Fundamentals*

### **What is Jenkins?**

* **Jenkins** is an open-source automation server designed to help automate parts of software development, especially building, testing, and deploying code.
* It enables **Continuous Integration (CI)** and **Continuous Delivery/Deployment (CD)** workflows by automating repetitive tasks.
* Highly extensible through plugins.

---

### **Advantages of Jenkins**

* **Open-source** and free with a large community.
* Supports **hundreds of plugins** for integration with various tools and services.
* Easy to configure through **web UI** or code.
* Enables **automation** of building, testing, and deployment processes.
* Supports distributed builds across multiple nodes/slaves.
* Works with almost any language or source code repository.

### **Disadvantages of Jenkins**

* UI can feel outdated or complex for beginners.
* Setup and plugin management can be cumbersome.
* Maintenance overhead, especially in large environments.
* Pipelines can become complex and hard to maintain if not well-structured.
* Scaling and security require additional configuration.

---

### **What is Jenkins Pipeline?**

* A **Pipeline** is a suite of plugins that supports **defining build processes as code**.
* It allows defining a **CI/CD workflow** as a series of stages and steps in a **Jenkinsfile** (written in Groovy DSL).
* Pipelines provide **more flexibility and robustness** compared to freestyle jobs.
* Enables **code review, version control, and easier collaboration** since pipeline code is stored alongside the source code.

---

### **Motivation for Using Jenkins Pipeline**

* **Automation as code:** pipelines are scripted, stored in SCM, and version controlled.
* **Complex workflows:** allows multiple stages (build, test, deploy) with parallelism, conditional execution, and error handling.
* **Better maintainability:** code is easier to review, reuse, and extend.
* **Resilience:** pipelines can survive Jenkins restarts, checkpointing progress.
* **Integration:** pipelines can integrate tightly with SCM, testing tools, notifications, and deployment systems.

---

### **Freestyle Jobs vs Pipelines**

| Aspect            | Freestyle Jobs                              | Pipelines                                                 |
| ----------------- | ------------------------------------------- | --------------------------------------------------------- |
| Definition        | Configured mostly through UI, step-by-step. | Defined as code in a Jenkinsfile (Groovy).                |
| Flexibility       | Limited, linear, simpler workflows.         | Highly flexible; supports parallelism, loops, conditions. |
| Version Control   | No native version control for config.       | Pipeline scripts stored in source control.                |
| Complex Workflows | Difficult to manage complex flows.          | Designed for complex, multi-stage workflows.              |
| Restart & Resume  | No checkpointing support.                   | Can resume after Jenkins restart.                         |

---

### **Pipeline Concepts**

* **Node:** A machine where Jenkins executes pipeline steps (master or agent).
* **Stage:** Logical phase of the pipeline (e.g., Build, Test, Deploy).
* **Step:** Single task or command inside a stage (e.g., shell command).
* **Agent:** Defines where the pipeline or stage runs (any node, specific label, docker container, etc.).
* **Scripted vs Declarative Pipeline:**

  * *Declarative:* Simplified and opinionated syntax for most use cases.
  * *Scripted:* More flexible Groovy-based code for advanced logic.

---

### **Pipeline Syntax Overview**

**Declarative Pipeline example:**

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'make build'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'make test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sh 'make deploy'
            }
        }
    }
}
```

---

### **Defining a Pipeline**

* Create a **Jenkinsfile** at the root of your repository.
* Write pipeline code in declarative or scripted syntax.
* Commit the Jenkinsfile to SCM (Git, SVN, etc.).
* In Jenkins UI, create a pipeline job that points to the repository containing the Jenkinsfile.

---

### **Blue Ocean vs Classic UI**

* **Classic UI:** The traditional Jenkins interface, powerful but can be cluttered and less user-friendly.
* **Blue Ocean:** A modern, streamlined Jenkins UI focused on visualization of pipelines.

  * Shows pipeline stages graphically.
  * Easier navigation, visualization, and debugging.
  * Built to improve usability for DevOps teams.

---

### **SCM (Source Code Management) Integration**

* Jenkins pipelines typically pull code and Jenkinsfile from SCM.
* Supports Git, SVN, Mercurial, Perforce, and others via plugins.
* Enables **pipeline-as-code** by keeping Jenkinsfile alongside the app code in SCM.
* Pipelines can be triggered by SCM events (e.g., commits, pull requests).

---