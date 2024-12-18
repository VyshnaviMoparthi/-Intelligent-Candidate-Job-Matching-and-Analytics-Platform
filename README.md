**Intelligent Candidate-Job Matching and Analytics Platform**

This repository contains the implementation of an Intelligent Candidate-Job Matching and Analytics Platform. The project leverages advanced data engineering practices, PySpark, Google Cloud Platform (GCP) tools, and Looker Studio for comprehensive data analytics and visualization.

**1. Project Overview**

The goal of this platform is to streamline and optimize the process of matching candidates to job opportunities while providing insightful analytics through dashboards. Below is an overview of the project workflow:

**2. Overview**

This project aims to develop a comprehensive data engineering pipeline that processes candidate and job data to deliver actionable insights. Using Apache Spark and BigQuery on Google Cloud Platform (GCP), the platform enables advanced analytics and visualization via BI tools such as Google Looker Studio. The system’s primary objectives include matching candidates to jobs based on compatibility, analyzing hiring trends, and assessing company hiring efficiencies.

**3. Key Objectives**

Data Processing: Clean and transform raw data from multiple sources (e.g., candidates, job descriptions, education, work experience) into structured, analyzable formats.

Matching Algorithm: Build a robust candidate-job matching algorithm using job description (JD) and curriculum vitae (CV) data to compute compatibility scores.

BigQuery Integration: Store processed data in BigQuery for querying and analytics.

Visualization: Use BI tools to create interactive dashboards highlighting hiring trends, skills distribution, and job metrics.

**4.Technology Stack**

Data Storage: Google Cloud Storage (GCS), BigQuery

Data Processing: Apache Spark (PySpark)

BI Tools: Google Looker Studio

GCP Services: Cloud Storage, Cloud Dataproc, BigQuery

**5.Implementation Plan**

5.1. Data Collection and Storage

Upload raw datasets in CSV/JSON format to Google Cloud Storage (GCS).

Organize data using a clear schema:

raw/ for unprocessed data.

processed/ for cleaned and transformed data.

5.2. Data Cleaning and Preprocessing

Setup:

Deploy a Cloud Dataproc cluster for distributed data processing with Apache Spark.

Tasks:

Data Quality Checks: Address null values, duplicates, and inconsistencies.

Standardization: Normalize text fields (e.g., company names, job titles).

Dataset Joins: Merge datasets using foreign keys such as job_id.

Feature Engineering:

Extract skill keywords from non_technical_skills.

Calculate technical_skills and job tenure from candidate_id, start_date, and end_date in work experience records.

Parse and standardize notice_period fields into numeric values.

5.3. Data Transformation and Loading

Save Processed Data:

Load transformed datasets into BigQuery with schemas such as:

Candidates Table: Includes personal details, work/education history, and matched job scores.

Job Descriptions Table: Contains key JD attributes and computed metrics.

BigQuery Views:

Create aggregated views, e.g., average_matching_scores to calculate match scores by job.

5.4. Visualization with BI Tools

BI Integration:

Connect BigQuery to a BI tool like Google Looker Studio.

**6.Metrics and Deliverables**

6.1.Candidate-Level Metrics

Total Candidates Processed: Count of unique candidates (cid).

Distribution by Degree Level: Count of candidates grouped by degree and tier_level (e.g., Tier 1 colleges).

Skills Analysis:

Top 10 technical and non-technical skills from the technical_skills and non_technical_skills fields.

Skill popularity across candidates.

Notice Period Analysis:

Average notice period across candidates.

Count of candidates by notice period ranges (e.g., <30 days, 30–60 days, >60 days).

Experience Distribution:

Candidates grouped by total experience (total_exp from work experience table).

Count of freshers vs. experienced candidates.

Candidate Location Insights: Candidates grouped by location (from work experience).

6.2.Job-Level Metrics

Open vs. Filled JDs: Count of JDs with jd_status_value as open vs. filled.

Jobs by Location and Industry: Distribution of JDs by pref_location and company_name industry.

Job Designation and Skills Mapping: Top required skills for each designation extracted from technical_skills.

Notice Period Trends: Average required notice period across JDs.

Popular Job Roles: Count of JDs grouped by designation.

6.3.Matching Insights

Average Matching Score per JD: Aggregate jd_cv_matching_score by jd_id to compute average matching scores.

Top JDs by Candidate Interest: Top 10 JDs based on the count of candidates with is_interested as true.

Skills Match Trends: Average skill match percentage for JDs with higher matching scores.

Candidate-JD Overlap: Number of candidates interested in multiple JDs (grouped by cid).

Skill Gaps Analysis: Compare top skills required in JDs vs. candidate skills to identify gaps.

For example: Missing Skills = JD Technical Skills - Candidate Technical Skills

Candidate Performance: Ranking candidates based on their matching scores across multiple JDs.

Job Demand vs. Candidate Supply: Ratio of open JDs to total candidates for specific skills, locations, or industries.

6.4.Company Efficiency Metrics

Hiring Completion Rate:

Percentage of JDs filled vs. total JDs (jd_status_value).

Example: Hiring Completion Rate = (Filled JDs / Total JDs) * 100

Time to Fill Positions: Average time taken to fill a JD (updated_at - created_at for status change).

Industry Trends: Number of jobs posted by industry or company (company_name).

Data Aggregations for Metrics

Candidate Metrics: Use Spark aggregations (groupBy, count, avg) to compute counts and averages for candidate metrics.

Job Metrics: Extract and join jd_id and related fields from the JD table for aggregations.

Matching Metrics: Use filtering and grouping on jd_cv_matching_score and is_interested.

Efficiency Metrics: Compute time differences (updated_at - created_at) and group by company_name.
