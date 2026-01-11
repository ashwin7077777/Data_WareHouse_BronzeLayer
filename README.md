
# 🥉 Bronze Layer ETL Pipeline — SQL Server

---

## 📌 Project Overview

This project implements a **Bronze Layer ETL pipeline** for a modern data warehouse using **SQL Server stored procedures**.
The implementation is inspired by the concepts taught in **Data With Baraa**, focusing on building strong fundamentals in:

* **Data warehousing architecture**
* **ETL best practices**
* **Production-grade SQL coding standards**

The pipeline ingests **raw data from CRM and ERP CSV files** into the **Bronze layer**, ensuring the data is stored in its **purest, unchanged form** for downstream processing.

---

## 🥉 What is the Bronze Layer?

In a modern data warehouse, data flows through multiple layers:

| **Layer**  | **Purpose**                          |
| ---------- | ------------------------------------ |
| **Bronze** | Raw, untransformed data              |
| **Silver** | Cleaned, standardized data           |
| **Gold**   | Business-ready, analytics-ready data |

The **Bronze layer** acts as the **single source of truth**.
It stores data **exactly as it comes from the source systems** —
**no joins, no transformations, no business logic**.

---

## ⭐ Why the Bronze Layer is Important

* **Preserves original data** for audit and debugging
* **Enables reprocessing** if transformation logic changes
* **Creates a clear separation** between ingestion and transformation
* **Improves data reliability and traceability**
* **Supports enterprise-grade data governance**

---

## 🔁 ETL Concept Used in This Project

This project follows the **classic ETL pattern**.

---

### 1️⃣ Extract

Data is extracted from:

* **CRM CSV files**
* **ERP CSV files**

---

### 2️⃣ Load (Bronze Stage)

Data is loaded into SQL Server using:

* **BULK INSERT**
* **Table-level truncation** for fresh loads
* **Batch processing logic**

> ⚠️ **No transformation is performed in the Bronze layer.**
> This strictly follows **industry best practices** as taught by **Data With Baraa**.

---

### 3️⃣ Transform

Transformation is **not part of this layer**.
It will be implemented later in:

* **Silver Layer** — cleaning & standardization
* **Gold Layer** — business logic & analytics modeling

---

## 🏗 Architecture Used

```
Source Files (CSV)
        |
        v
+------------------+
|  Bronze Layer    |
|  (Raw Tables)    |
+------------------+
        |
     Future
        |
+------------------+
|  Silver Layer    |
+------------------+
        |
+------------------+
|  Gold Layer      |
+------------------+
```

---

## ⚙️ What This Pipeline Does

The stored procedure **`bronze.load_bronze`** performs the following operations:

---

### ✅ Data Ingestion

Loads data into Bronze tables from:

#### CRM Tables

* **crm_cust_info**
* **crm_prd_info**
* **crm_sales_details**

#### ERP Tables

* **erp_cust_az12**
* **erp_loc_a101**
* **erp_px_cat_g1v2**

---

### ✅ Logging & Monitoring

For **every table load**, the pipeline:

* Prints **start messages**
* Prints **truncation status**
* Prints **load completion status**
* Captures and prints **table-level load duration**

---

### ✅ Batch-Level Tracking

At the pipeline level, it:

* Tracks **batch start time**
* Tracks **batch end time**
* Calculates and prints:

  * **Total pipeline execution time**
  * **Overall batch duration**

---

### ✅ Error Handling

Implements **production-grade error handling** using a centralized:

```
BEGIN TRY
...
END TRY
BEGIN CATCH
...
END CATCH
```

The pipeline logs:

* **Error Number**
* **Error Severity**
* **Error State**
* **Error Line Number**
* **Full Error Message**

The error is **re-thrown using `THROW`** so that:

* **SQL Agent jobs fail correctly**
* **Monitoring tools can detect failures**
* **Alerts and retries can be triggered**
* **No silent failures occur**

---

## 🧠 Design Principles Followed

This project strictly follows **modern data engineering principles**:

* **Separation of concerns**
* **Layered architecture**
* **Schema-on-read philosophy**
* **Auditability and traceability**
* **Reproducible pipelines**
* **Enterprise-grade error handling**

---

## 🎯 Learning Outcomes

By building this project, you gain hands-on experience in:

* Designing a **real-world data warehouse ingestion layer**
* Writing **production-ready SQL stored procedures**
* Implementing **robust logging and monitoring**
* Applying **best-practice ETL architecture**
* Understanding how **Bronze → Silver → Gold** pipelines scale in enterprises

---

## 🙏 Credits

This project is inspired by the teachings of **Data With Baraa**, whose content emphasizes:

* Strong **data engineering fundamentals**
* **Industry-aligned best practices**
* Real-world **data warehouse architecture patterns**


