# Use Case: Cloud-Based Patient Intake and Triage Analytics for a Community Clinic

## **Problem Statement**

Paper forms or disorganized spreadsheets are commonly used by community health centers and small outpatient clinics to record patient intake data, including demographics, symptoms, vital signs, and reasons for visits. As a result, medical professionals find it challenging to quickly recognize high-risk patients, monitor visit patterns, or track daily workload. The lack of centralized, structured data also limits basic analytics that could help with operational planning and triage.

The cloud-based patient intake and triage analytics system proposed in this project enables clinicians to upload patient intake data, securely store it, and generate straightforward summaries for administrative and clinical decision-making.

Primary users include:
* Front desk or intake employees uploading intake data
* Clinicians examining the summarized triage signs
* Clinic administrators keeping an eye on visit patterns

This solution does not store actual PHI and is meant only for demonstration and educational purposes.

## **Data Sources**
Simple structured data is taken in by the system, including:
* CSV files with patient intake information (such as visit date, age range, chief complaint, basic vitals, and triage level)
* JSON payloads (optional extension) submitted through a web form

## **Basic Workflow**
1. Clinic staff uploads a CSV intake file through a Flask web application.
2. The file is stored in Google Cloud Storage as raw input data.
3. A backend process parses and cleans the data.
4. Cleaned records are written to a Cloud SQL (MySQL) database.
5. Simple analytics (e.g., visit counts, common symptoms, triage distribution) are generated.
6. Summary statistics are displayed through the Flask app for staff review.
