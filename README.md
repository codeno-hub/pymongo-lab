# pymongo-lab
# PyMongo: MongoDB & Python Engineering Lab

A structured repository of hands-on notebooks, data modeling experiments, and backend mini-projects built with **Python** and **PyMongo**.

## About This Repository

This repository serves as a central workspace for mastering document-oriented databases—progressing from core CRUD operations and multi-stage aggregation pipelines to query optimization, schema validation, and API integration. Each folder is self-contained with its own dataset, runnable code, and documentation.

---

## Repository Index

| # | Folder / Module | Focus Areas |
|---|---|---|
| 01 | [01-aggregation-and-indexing](./01-aggregation-and-indexing) | `$unwind`, `$group`, `$match`, `$project`, `$lookup` joins, `COLLSCAN` vs. `IXSCAN` optimization |
| 02 | `02-schema-validation` *(Planned)* | JSON Schema validation rules, data integrity constraints |
| 03 | `03-fastapi-mongodb-crud` *(Planned)* | Async Motor/PyMongo integration with REST APIs |

---

## Tech Stack

* **Database:** MongoDB / MongoDB Atlas
* **Language & Driver:** Python 3, PyMongo (`dnspython`)
* **Environment:** Google Colab, Jupyter Notebook

## Getting Started

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/pymongo.git
   cd pymongo
