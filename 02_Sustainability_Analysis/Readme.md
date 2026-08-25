# SQL Data Cleaning and Data Quality Validation

## Project Overview

This project was completed as part of the DACA (Data Analyst Career Accelerator) program.

The objective was to improve data quality by identifying and resolving common data issues in a retail database hosted in Supabase.

The project focused on four key areas:

- Sales data cleaning
- Customer data cleaning
- Product data cleaning
- Cross-table validation and data quality checks

---

## Tools Used

- SQL
- PostgreSQL / Supabase
- GitHub

---

## Dataset

The database contained three main business tables:

| Table | Description |
|---------|-------------|
| sales | Sales transactions |
| customers | Customer information |
| products | Product catalog |

---

## Sales Data Cleaning

### Checks Performed

- Duplicate invoice detection
- NULL value validation
- Future date validation
- Guest purchase identification

### Findings

| Issue | Count |
|---------|---------|
| Duplicate rows | 5116 |
| Duplicate invoice IDs | 4013 |
| NULL customer_id | 1487 |
| NULL sale_date | 0 |
| NULL total_price | 0 |
| Future dates | 0 |

### Business Conclusion

Duplicate sales records were the most critical issue because they directly impact revenue reporting and business analytics.

---

## Customer Data Cleaning

### Findings

| Issue | Count |
|---------|---------|
| Duplicate emails | 129 |
| Missing names | 0 |
| Missing contact information | 380 |
| City naming inconsistencies | 54 |

### Business Conclusion

Missing contact information presents the highest operational risk because customers cannot be contacted effectively.

---

## Product Data Cleaning

### Findings

| Issue | Count |
|---------|---------|
| Duplicate product names | 12 |
| NULL critical fields | 0 |
| Pricing errors | 0 |
| Category inconsistencies | 0 |

### Business Conclusion

Duplicate product names can distort product-level sales and profitability analysis.

---

## Cross-Table Validation

### Findings

| Issue | Count |
|---------|---------|
| Orphan customers | 0 |
| Orphan products | 0 |
| Price mismatches | 664 |
| Customers with no purchases | 592 |
| Unsold products | 12 |

### Business Conclusion

The most significant data quality concern was pricing inconsistency between sales transactions and product retail prices.

---

## Key Recommendations

1. Remove duplicate sales transactions.
2. Standardize customer contact information.
3. Enforce unique product identifiers.
4. Implement automated data quality monitoring.
5. Validate sales prices against product prices.

---

## Skills Demonstrated

- SQL Data Cleaning
- Data Quality Assessment
- Duplicate Detection
- NULL Value Analysis
- Data Validation
- Cross-Table Verification
- Business Insight Reporting

---

## Repository Structure

```text
portfolio/
└── week-2/
    ├── individual/
    │   ├── week2_sales_cleaning.sql
    │   ├── week2_customers_cleaning.sql
    │   ├── week2_products_cleaning.sql
    │   └── week2_cross_validation.sql
    ├── team/
    │   └── week2_team_cleaning_report.md
    └── README.md
