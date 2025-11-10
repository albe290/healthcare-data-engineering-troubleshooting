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

> ⚡ *Diagnosed and resolved a Databricks–AWS S3 permission issue by updating IAM policies, enabling secure external locations for Delta Lake integration.*

---

## 🩺 Project Overview
This troubleshooting effort is part of my larger **Healthcare Wait Time Data Engineering Project**, where I’m building a scalable **data lakehouse** using **Databricks**, **Delta Lake**, and **AWS S3**.  
The goal is to ingest real-time hospital wait time data, transform it through **Bronze → Silver → Gold** layers, and prepare it for downstream analytics and machine learning.

---

## 🚨 Problem Overview

While creating external locations in Databricks (Unity Catalog), I encountered the following error:

```bash
PERMISSION_DENIED: AWS IAM role does not have READ permissions on s3://hospital-wait-times-bucket-usw2/bronze
````

This indicated that my Databricks workspace’s IAM role did not have the proper **read/list** permissions on the target S3 bucket.

---

### ❌ Initial Error Message

Databricks displayed this error when attempting to create external locations for the **Bronze/Silver/Gold** data layers:

![IAM Permission Error](images/Permission%20IAM%20Error%20message.png)

This message confirmed the workspace’s IAM role was missing `s3:GetObject` and `s3:ListBucket` access on the **hospital-wait-times-bucket-usw2**.

---

## 🧭 Root Cause

After inspecting the storage credential in Databricks using:

```sql
DESCRIBE STORAGE CREDENTIAL workspace;
```

I discovered that the IAM role linked to my Unity Catalog storage credential didn’t include the required S3 permissions.

---

## 🧩 Solution Steps

After diagnosing the issue, I followed these key steps to resolve it 👇🏾

| 🧭 Step 1 — Identify the IAM Role                                      | 🔐 Step 2 — Update IAM Policy                            | ✅ Step 3 — Validate in Databricks                                        |
| ---------------------------------------------------------------------- | -------------------------------------------------------- | ------------------------------------------------------------------------ |
| ![Describe Storage Credential](images/step1-describe-storage-role.png) | ![IAM Policy Update](images/step2-iam-policy-update.png) | ![External Location Success](images/step3-external-location-success.png) |

**Step 1:** Ran `DESCRIBE STORAGE CREDENTIAL workspace;` to confirm the IAM role Databricks was assuming.
**Step 2:** Updated the IAM policy in AWS to include `s3:ListBucket`, `s3:GetObject`, and `s3:PutObject` for the hospital wait time bucket.
**Step 3:** Re-ran the SQL commands to create the **Bronze, Silver, and Gold** locations all executed successfully ✅

---

## ⚙️ Tech Stack

| Layer      | Tool              | Purpose                                  |
| ---------- | ----------------- | ---------------------------------------- |
| Cloud      | **AWS (S3, IAM)** | Data lake storage + permissions          |
| Platform   | **Databricks**    | ETL, Delta Lake, and catalog management  |
| Governance | **Unity Catalog** | Access control and security              |
| Format     | **Delta Lake**    | ACID table format for scalable analytics |
| Language   | **SQL / PySpark** | Data transformations and validation      |

---

## 🧠 Lessons Learned

* Always verify **which IAM role** your Databricks storage credential uses.
* Cross-check **S3 region** and **Databricks metastore region** for compatibility.
* Keep IAM policies **bucket-specific and least-privileged**.
* Test permissions using **`DESCRIBE STORAGE CREDENTIAL`** and **external location creation**.
* Proper IAM configuration avoids hours of unnecessary debugging!

---

## 🔗 Resources

* [Databricks: External Locations Documentation](https://docs.databricks.com/en/data-governance/unity-catalog/external-locations.html)
* [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)
* [Delta Lake Overview](https://docs.databricks.com/en/delta/index.html)

---

## 🩺 Next Steps

* Build the **Healthcare** catalog and `er_wait_times` schema.
* Ingest data via **Auto Loader** into Bronze → Silver → Gold layers.
* Implement **Delta Live Tables** for incremental updates.
* Use **MLflow** to predict emergency wait times.

---

⭐ **If you found this helpful, feel free to star the repo and connect with me on [LinkedIn](www.linkedin.com/in/aalbertglenn)!**

🧠 *Next up: Integrating Delta Live Tables + Auto Loader for a full production pipeline.*

