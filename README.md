Data Analysis of Zepto Inventory dataset using MySQL

# Zepto Data Analysis — SQL Project

A structured SQL-based data analysis project on Zepto's product catalog, covering data exploration, cleaning, and business insight queries.

---

## Project Structure

```
zepto-data-analysis/
│
├── Zepto_Data_Analysis_SQL.sql   # Main SQL script (exploration + cleaning + analysis)
└── README.md
```

---

## Database Setup

The project uses a MySQL database named `zepto_database` with a table called `zepto`.

**Schema modifications applied:**
- Added a `sku_id` column as a `SERIAL PRIMARY KEY`
- Renamed the malformed column `ï»¿Category` to `category` (BOM encoding fix)

---

##  Data Exploration

Before analysis, the following exploratory steps were performed:

- Total row count
- Sample data preview (first 10 rows)
- Null value check across all key columns
- Distinct product categories
- In-stock vs. out-of-stock product distribution
- Products appearing under multiple SKUs

---

## Data Cleaning

| Issue | Fix Applied |
|---|---|
| Products with `mrp = 0` | Deleted from table |
| Prices stored in paise | Converted to ₹ by dividing by `100.0` |

---

## Business Analysis Queries

| # | Question | Technique Used |
|---|---|---|
| Q1 | Top 10 best-value products by discount % | `ORDER BY discountPercent DESC` |
| Q2 | High MRP (>₹300) products that are out of stock | Filter on `outOfStock` + `mrp` |
| Q3 | Estimated revenue per category | `SUM(discountedSellingPrice × availableQuantity)` |
| Q4 | Premium products (MRP > ₹500) with low discount (<10%) | Compound `WHERE` filter |
| Q5 | Top 5 categories by average discount % | `AVG` + `GROUP BY` + `LIMIT` |
| Q6 | Price per gram for products ≥ 100g | Derived column: `discountedSellingPrice / weightInGms` |
| Q7 | Weight-based product segmentation (Low / Medium / Bulk) | `CASE WHEN` |
| Q8 | Total inventory weight per category | `SUM(weightInGms × availableQuantity)` |

---

## Tech Stack

- **Database:** MySQL
- **Language:** SQL (DDL + DML + DQL)
- **Concepts:** Aggregations, filtering, `CASE` expressions, derived metrics, data cleaning

---

## Getting Started

1. Clone this repository:
   ```bash
   git clone https://github.com/ManasSriv10/zepto-data-analysis.git
   ```

2. Import the dataset into MySQL and create the `zepto_database` schema.

3. Run the SQL script:
   ```sql
   SOURCE Zepto_Data_Analysis_SQL.sql;
   ```

---

## Key Insights (Sample)

- Several high-MRP products remain out of stock, indicating potential demand worth restocking.
- Estimated revenue varies significantly across categories, with certain categories dominating due to high availability.
- Price-per-gram analysis helps surface the best-value products for weight-sensitive categories like groceries and snacks.

---

## Notes

- Prices in the raw dataset were stored in **paise**; all monetary values have been normalized to **Indian Rupees (₹)**.
- The `outOfStock` column is stored as a string (`'true'`/`'false'`), not a boolean — queries account for this.

---

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

---

## License

This project is open source and available under the [MIT License](LICENSE).
