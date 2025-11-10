<p align="center">
  <img src="https://img.shields.io/badge/Built%20With-Databricks-orange?style=for-the-badge&logo=databricks" alt="Built with Databricks"/>
  <img src="https://img.shields.io/badge/Cloud-AWS_S3-blue?style=for-the-badge&logo=amazonaws" alt="AWS S3"/>
  <img src="https://img.shields.io/badge/Security-IAM%20Troubleshooting-success?style=for-the-badge&logo=amazonaws" alt="IAM Troubleshooting"/>
  <img src="https://img.shields.io/badge/Architecture-Medallion%20(Bronze%2Fsilver%2Fgold)-yellow?style=for-the-badge" alt="Medallion Architecture"/>
  <img src="https://img.shields.io/github/stars/albe290/healthcare-data-engineering-troubleshooting?style=for-the-badge&logo=github" alt="GitHub stars"/>
</p>

<h1 align="center">🏥 Troubleshooting AWS IAM “Permission Denied” in Databricks</h1>

<p align="center">
  <i>Real-world debugging of a Databricks + AWS S3 integration issue during my Healthcare Wait Time Data Engineering Project</i>
</p>

---

This repository documents how I resolved a **PERMISSION_DENIED** error between **Databricks** and **AWS S3** while building my **Healthcare Wait Time Data Engineering Project**.  

The issue occurred while creating **external locations (Bronze, Silver, and Gold layers)** in Databricks using **Unity Catalog**.  
The fix involved tracing IAM roles, updating AWS inline policies, and validating connectivity between Databricks and S3.

---

## 🚨 Problem Overview

When I attempted to create external locations in Databricks, I received the following error:

```bash
PERMISSION_DENIED: AWS IAM role does not have READ permissions on s3://hospital-wait-times-bucket-usw2/bronze
