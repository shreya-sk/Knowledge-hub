# [[Expense-Tracker]] Template 

## Overview

This is a simple expense tracking template for Obsidian that requires minimal manual input but provides comprehensive financial insights. It uses the Dataview plugin to automatically calculate totals, categorize expenses, and generate reports.

## Getting Started

### Prerequisites

1. [Obsidian](https://obsidian.md/) - A knowledge base app that works on local markdown files
2. [Dataview Plugin](https://github.com/blacksmithgu/obsidian-dataview) - Install this from Obsidian's Community Plugins

### Setup Instructions

1. Create a new note in Obsidian
2. Copy and paste the entire [[Expense-Tracker]] into your note
3. Install and enable the Dataview plugin
4. Make sure "JavaScript Queries" are enabled in Dataview settings

## How to Use

### Adding Transactions

Add your expenses at the top of the file in the "Transaction List" section:

```
- 15th Jan: $120 [Rent]
```

The format is:

- Date: Always include the month (Jan, Feb, etc.)
- Amount: Always use $ symbol
- Category: [Optional] Add in square brackets

Examples:

```
- 1st Jan: $10 [Coffee]
- 15th Jan: $100 [Groceries]
- 20th Jan: $15.50 [Subscription]
```

### Understanding the Auto-Generated Reports

The template automatically generates:

1. **Monthly Summary** - Total spending by month
2. **Category Breakdown** - Overall spending by category
3. **Transaction Log** - All transactions with a running total
4. **Monthly Category Breakdown** - Category spending for each month

### Customization

You can customize the template by:

- Adding your own categories
- Modifying the report sections in the dataviewjs code block
- Adding income items by using negative values (e.g., `- 15th Jan: -$1000 [Salary]`)

## Alternative Budgeting Approaches

### For Comprehensive Tracking (Australia)

- **Frollo** - Connects to 170+ Australian financial institutions
- **Pocketbook** - Australian-made finance tracker
- **Money Brilliant** - Comprehensive Australian finance app
- **Up Bank** - Neobank with built-in tracking features

## Troubleshooting

- **Dataview Errors** - Make sure you have the latest version of the Dataview plugin
- **Missing Transactions** - Ensure proper formatting (date format, $ symbol)
- **Category Issues** - Check that all categories use square brackets [Category]