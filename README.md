# Finance Management System

A desktop application built with Python that records income and expense transactions, stores them in a MySQL database, and runs an audit to determine whether a business is in profit, loss, or break-even.

![Finance Management System](screenshot.png)

## Features

- **Income entry:** adds an amount to the stored income total
- **Expense entry:** adds an amount to the stored expense total
- **Audit:** computes net balance (income − expenses), saves it to the database, and reports profit, loss, or break-even
- **Live table:** a scrollable Treeview displays Company, Income, Expense, and Balance, refreshing after every operation
- **Error handling:** input validation and database errors are shown through message boxes

## Tech Stack

| Component | Technology |
|-----------|------------|
| Language | Python 3 |
| GUI | Tkinter, ttk |
| Database | MySQL |
| Connector | PyMySQL |

## Project Structure

```
.
├── finance.py      # Application source code
├── screenshot.png  # UI preview
└── README.md
```

## Setup

### 1. Prerequisites

- Python 3.8+
- MySQL Server running locally

### 2. Install dependencies

```bash
pip install pymysql
```

Tkinter ships with most Python installations.

### 3. Create the database

Run the following in MySQL:

```sql
CREATE DATABASE finance;
USE finance;

CREATE TABLE finance (
    company VARCHAR(50) PRIMARY KEY,
    income  INT DEFAULT 0,
    expense INT DEFAULT 0,
    balance INT DEFAULT 0
);

INSERT INTO finance (company, income, expense, balance)
VALUES ('ABC', 0, 0, 0);
```

### 4. Configure the connection

In the `dbFun()` method of `finance.py`, update the connection details with your own MySQL credentials:

```python
self.con = pymysql.connect(
    host="localhost",
    user="root",
    password="your_password",
    database="finance"
)
```

> Do not commit real credentials to GitHub. Consider reading them from environment variables instead.

### 5. Run

```bash
python finance.py
```

## Usage

1. Enter the **Amount** and the **Type** (e.g. Salary, Rent).
2. Click **Income** or **Expenses** to update the corresponding total.
3. Click **Audit** to calculate the balance and view the profit/loss status.
4. The table on the right shows the latest figures.

## How It Works

- Each button triggers a handler (`incomeFun`, `expFun`, `audFun`) that opens a database connection, reads the current value, updates it, and commits the change.
- After each operation, the Treeview is cleared and repopulated with the latest record so the UI stays in sync with the database.
- Balance is calculated as `income − expense`, and the result decides the message shown (profit, loss, or no profit no loss).

## Future Improvements

- Transaction history table (store type, amount, and date for each entry)
- Support for multiple companies
- Input validation for non-numeric amounts
- Charts for income vs. expense trends
- Export reports to CSV or PDF

## Author

**Aryan Prakash Bhanage**
