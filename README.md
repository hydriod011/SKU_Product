# SKU Product Generator

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-Web_Framework-000000?style=flat-square&logo=flask&logoColor=white)
![Gunicorn](https://img.shields.io/badge/Gunicorn-WSGI_Server-499848?style=flat-square&logo=gunicorn&logoColor=white)
![Render](https://img.shields.io/badge/Deployed_on-Render-46E3B7?style=flat-square&logo=render&logoColor=black)

A lightweight Flask web application for generating standardized **Stock Keeping Units (SKUs)** from product attributes, managing a live in-memory inventory table, and exporting product records as a downloadable CSV report.

🔗 **Live Application:** [https://sku-product.onrender.com/](https://sku-product.onrender.com/)

---

## 📖 Introduction

Managing product catalogs manually often leads to inconsistent naming conventions, duplicate codes, and tracking errors. **SKU Product Generator** solves this by providing a clean, browser-based interface where users input core product details—**Brand**, **Category**, **Item Type**, **Color**, and **Size**—to automatically generate structured, uppercase SKU identifiers.

Generated items are immediately displayed in a real-time inventory view where users can review entries, delete unwanted records, or export the entire catalog to a spreadsheet-ready CSV file (`sku_inventory_report.csv`).

---

## 🎯 Project Objectives

* **Standardize SKU Naming:** Automatically convert product attributes into a predictable, uppercase, hyphen-delimited format (`BRAND-CAT-TYPE-COLOR`).
* **Simplify Inventory Tracking:** Offer an instant web interface to view active SKUs alongside their full product metadata.
* **Enable Quick Record Management:** Allow one-click removal of outdated or incorrect SKU entries directly from the dashboard.
* **Support Portable Reporting:** Export active inventory records into a downloadable `.csv` file compatible with Microsoft Excel and Google Sheets.
* **Ensure Lightweight Deployment:** Keep the architecture minimal and production-ready for cloud hosting using Flask and Gunicorn.

---

## 🛠️ Technology Used

| Layer | Technology | Role in Project |
| :--- | :--- | :--- |
| **Backend** | Python & Flask | Handles routing, form processing, SKU generation, deletion, and CSV streaming |
| **Frontend** | HTML5 & Jinja2 (`templates/index.html`) | Renders the input form, dropdown menus, status alerts, and live inventory table |
| **WSGI Server** | Gunicorn | Serves the Flask application in production |
| **Hosting** | Render | Cloud platform hosting the live web app |

---

## ✨ Features

* **Automated SKU Formatting:** Generates unique SKU codes using the first 3 characters of the brand and the first 2 characters each of the category, product type, and color (e.g., `ACM-EL-CH-BL`).
* **Predefined Attribute Options:** Built-in dropdown selections for common **Categories** (`Electronics`, `Clothing`, `Footwear`, `Home Appliances`) and **Sizes** (`Small`, `Medium`, `Large`, `XL`, `N/A`).
* **Live Inventory Dashboard:** Displays newly created SKUs and their attributes in real time with instant confirmation messages.
* **One-Click Deletion:** Purge individual records cleanly via the `/delete/<sku>` endpoint.
* **CSV Report Export:** Download the complete active inventory as `sku_inventory_report.csv` via the `/export` endpoint.

---

## 🧩 How It Works

### SKU Naming Formula
```text
[BRAND (3 chars)] - [CATEGORY (2 chars)] - [ITEM TYPE (2 chars)] - [COLOR (2 chars)]
```

**Example Input:**
* **Brand:** `Nike`
* **Category:** `Footwear`
* **Item Type:** `Sneakers`
* **Color:** `White`
* **Size:** `Large`

**Generated SKU:** `NIK-FO-SN-WH`

### Application Routes

| Method | Route | Description |
| :--- | :--- | :--- |
| `GET`, `POST` | `/` | Renders the home page and processes form submissions to generate and store new SKUs |
| `GET` | `/delete/<sku>` | Removes the matching SKU entry from the active inventory and redirects to home |
| `GET` | `/export` | Streams all stored inventory records as a downloadable `sku_inventory_report.csv` file |

---

## 📁 Project Structure

```text
SKU_product/
│
├── app.py              # Main Flask application, SKU logic, delete route, and CSV export
├── requirements.txt    # Python dependencies (Flask, Gunicorn)
│
└── templates/
    └── index.html      # Frontend HTML template rendered with Jinja2
```

---

## 🚀 Installation & Local Setup

1. **Clone the repository**
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/SKU_product.git
   cd SKU_product
   ```

2. **Create and activate a virtual environment (optional but recommended)**
   ```bash
   python -m venv venv
   # On Windows:
   venv\Scripts\activate
   # On macOS/Linux:
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application**
   ```bash
   python app.py
   ```
   Visit `http://127.0.0.1:5000/` in your web browser.

---

## ⚠️ Current Limitations & Future Roadmap

* **In-Memory Storage:** Inventory data is currently stored in a Python dictionary in memory, meaning records reset when the server restarts or redeploys.
* **Collision Handling:** Two products sharing the same starting characters across brand, category, type, and color will generate identical SKU keys.

**Planned Improvements:**
* [ ] Integrate persistent database storage (SQLite or PostgreSQL).
* [ ] Add auto-incrementing numeric suffixes (e.g., `NIK-FO-SN-WH-001`) to prevent SKU collisions.
* [ ] Add search, filtering, and edit functionality for existing inventory items.

---

## 🙌 Credits & Acknowledgments

This project was created by **Shradha Chourasia**  GitHub: https://github.com/ShradhaChourasia
