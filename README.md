# 🏥 Troubleshooting AWS IAM "Permission Denied" in Databricks

This repository documents how I resolved a **PERMISSION_DENIED** error between **Databricks** and **AWS S3** while building my **Healthcare Wait Time Data Engineering Project**.  

The issue occurred while creating **external locations (Bronze, Silver, Gold layers)** in Databricks using **Unity Catalog**.

---

## 🚨 Problem Overview

When I attempted to create external locations in Databricks, I kept seeing the following error:

bash
PERMISSION_DENIED: AWS IAM role does not have READ permissions on s3://hospital-wait-times-bucket-usw2/bronze
