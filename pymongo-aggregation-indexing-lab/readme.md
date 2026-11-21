# PyMongo Aggregation Pipelines & Indexing Practice

A hands-on Google Colab notebook demonstrating core MongoDB operations, aggregation pipelines, and query optimization in Python using **PyMongo**.

## Overview

Using a sample e-commerce dataset (`techgear_db`) consisting of `orders` and `customers` collections, this notebook walks through transforming, joining, and optimizing queries on document-based data.

## Concepts Covered

* **Database & Collection Setup:** Connecting via `MongoClient` and seeding sample relational-style documents (`orders` and `customers`).
* **Array Deconstruction (`$unwind`):** Flattening the `items` array inside order documents to analyze individual product occurrences.
* **Data Aggregation (`$group` & `$sort`):** Calculating item sales frequency (`times_sold`) and ranking products by popularity.
* **Filtering & Shaping (`$match` & `$project`):** Filtering for `shipped` orders and dynamically computing post-tax totals (`18%` GST/tax) while excluding internal `_id` fields.
* **Collection Joins (`$lookup`):** Performing a left outer join between `orders` and `customers` on `customer_id` to enrich order records with customer metadata.
* **Query Optimization (`COLLSCAN` vs. `IXSCAN`):** Measuring execution stats via `.explain()` to compare total documents examined before and after creating a single-field index on `customer_id` (reducing scanned documents from `5` to `2`).

## Prerequisites & Setup

1. **Dependencies:**
   ```bash
   pip install pymongo dnspython
