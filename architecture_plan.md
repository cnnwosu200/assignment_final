# Architecture and Implementation Plan 

| Layer              | Service (GCP)                     | Role in Solution                                           | Related Assignment/Module      |
|------------------- |---------------------------------  |------------------------------------------------------------|---------------------------     |
| Frontend/ API      | Flask(Python)                     | Web interfaces for uploads and viewing summaries           | Assignment 2                   |
| Compute            | Cloud Run(containerized Flask app)| Runs the Flask application serverlessly                    | Module 5/Assignment 3          |
| Storage            | Cloud Storage                     | Stores raw uploaded CSV intake files                       | Module 6                       |
| Database/SQL       | Cloud SQL(MySQL)                  | Store cleaned intake records and aggregates                | Assignment 4                   |
| Analytics          | Vertex AI Notebook                | Runs exploratory queries and visual summaries              | Module 7                       |


## **Data Flow Narrative**
* **Step 1**: A clinic staff member accesses the Flask web app hosted on Cloud Run.
* **Step 2**: The user uploads a CSV file containing patient intake data.*
* **Step 3**:The Flask app stores the raw file in a Cloud Storage bucket for durability and traceability.
* **Step 4**: The application parses and validates the data, then inserts cleaned records into Cloud SQL.
* **Step 5**: SQL queries generate summary tables (e.g., visits per day, triage level counts).
* **Step 6**: The Flask app displays these summaries to users.

## Security, Identity, and Governance Basics
Instead of using hard-coded keys, environment variables, and service accounts are used to manage credentials for Cloud SQL and Cloud Storage. A dedicated service account with minimal IAM permissions runs the Flask application.
Only authorized services can access databases and storage due to access controls. Using synthetic or de-identified data instead of actual PHI reduces the risk of noncompliance. HIPAA-aligned controls, audit logging, and encryption at rest would be necessary in a production setting.

## Cost and Operational Considerations
Database and compute use would be the most significant cost drivers. To keep expenses under control:
* Cloud Run, which scales to zero while not in use, is used in place of an always-on virtual machine.
* For low-volume workloads, Cloud SQL runs on a small instance.
* Because CSV files are small, storage costs are kept to a minimum.

This architecture can grow in the future if necessary and fits under free tiers or student credits.
