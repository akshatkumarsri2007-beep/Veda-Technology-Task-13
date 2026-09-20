# Duplicate Record Check - Retail Sales Data

**Task 13 of the Data Analytics Track (Level 1, Day 13) at Veda Technology.**

**This project finds duplicate records in a retail sales dataset using Python and Pandas, documents them in a report, and produces a cleaned copy of the data along with an audit note.**

# Objective

Understand how duplicate detection works and how duplicate records affect data quality and business numbers such as total revenue and order counts.

# Tools Used

- Python 3
- Pandas
- OpenPyXL (for writing the Excel report)
- Google Colab
- Excel

# Dataset

`retail_sales_dataset.csv` contains 1,060 records and 10 columns. It is a sample retail sales dataset in which duplicate records were inserted on purpose for practice.

| Column | Description |
|---|---|
| Order_ID | Order identifier (key column) |
| Order_Date | Date of the order |
| Customer_ID | Customer identifier |
| Category | Product category |
| Product | Product name |
| Quantity | Units sold |
| Unit_Price | Price per unit |
| Total_Amount | Quantity x Unit_Price |
| City | City of the sale |
| Payment_Mode | Cash, UPI or Card |

## Project Structure

```
.
|-- retail_sales_dataset.csv         # Input data (with duplicates)
|-- duplicate_check.py               # Script for detection and cleaning
|-- duplicate_report.xlsx            # Output: all duplicate records
|-- cleaned_retail_sales.csv         # Output: dataset after cleaning
|-- audit_note.txt                   # Output: summary of the process
|-- Task13_Duplicate_Record_Check_Report.pdf
`-- README.md
```

## How to Run

**1. Clone the repository:**

   ```bash
   git clone <your-repository-url>
   cd <repository-folder>
   ```

**2. Install the requirements:**

   ```bash
   pip install pandas openpyxl
   ```

**3. Run the script:**

   ```bash
   python duplicate_check.py
   ```

The script creates `duplicate_report.xlsx`, `duplicate_report.csv`, `cleaned_retail_sales.csv` and `audit_note.txt` in the same folder.

The steps can also be run cell by cell in Google Colab after uploading the CSV file.

# Methodology

1. Load the CSV file and inspect its shape and data types.
2. Find full-row duplicates using `df.duplicated()`.
3. Find key-column duplicates using `df.duplicated(subset=["Order_ID"], keep=False)`, which shows every copy so they can be compared.
4. Save all duplicate records to the duplicate report.
5. Remove exact duplicates with `drop_duplicates()`, then remove repeated Order_IDs keeping the first record.
6. Save the cleaned dataset and write the audit note.

# Results

| Check | Result |
|---|---|
| Total records in original file | 1,060 |
| Full-row (exact) duplicates | 40 |
| Total repeated Order_ID records | 60 |
| Conflicting duplicates (same Order_ID, different values) | 20 |
| Records after cleaning | 1,000 |

The 60 repeated Order_ID records include the 40 exact duplicates plus 20 conflicting records where the Order_ID is the same but values such as City or Payment_Mode differ.

Total_Amount was 2,872,371 before cleaning and 2,729,249 after cleaning, a difference of about 5 percent that would have been counted as false revenue.

# Conclusion

Two types of duplicates were found. Exact copies were removed safely, while conflicting records sharing an Order_ID were documented and only the first occurrence was kept. Checking duplicates on both full rows and key columns is important because each method catches problems the other can miss. Recording every step in an audit note keeps the cleaning process transparent and repeatable.

## What I Learned

- How `duplicated()` and `drop_duplicates()` work
- How the `keep` and `subset` parameters change the result
- Why data should be cleaned and documented before any analysis

## By
Akshat Srivastava
Data Analytics Intern, Veda Technology
