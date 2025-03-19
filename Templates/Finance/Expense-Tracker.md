# Simple Expense Tracker Template

## Transaction List

<!-- Add your transactions here in this format -->

- 15th Jan: $120 [Rent]
- 18th Jan: $45 [Groceries]
- 20th Jan: $15 [Subscription]
- 1st Feb: $120 [Rent]
- 5th Feb: $50 [Utilities]
- 12th Feb: $40 [Groceries]

## Auto Calculation

```dataviewjs
// Get the current page
const page = dv.current();

// Extract the transfers from the list
const transferList = page.file.lists
  .filter(item => item.text.includes("$"))
  .map(item => {
    const text = item.text;
    
    // Extract date
    let date = "Unknown";
    if (text.includes(":")) {
      date = text.split(":")[0].trim();
    }
    
    // Extract amount
    const amountMatch = text.match(/\$(\d+(\.\d+)?)/);
    const amount = amountMatch ? parseFloat(amountMatch[1]) : 0;
    
    // Extract category if present
    let category = "Uncategorized";
    const categoryMatch = text.match(/\[(.*?)\]/);
    if (categoryMatch) {
      category = categoryMatch[1];
    }
    
    // Determine month
    let month = "Unknown";
    if (date.includes("Jan")) month = "January";
    if (date.includes("Feb")) month = "February";
    if (date.includes("Mar")) month = "March";
    if (date.includes("Apr")) month = "April";
    if (date.includes("May")) month = "May";
    if (date.includes("Jun")) month = "June";
    if (date.includes("Jul")) month = "July";
    if (date.includes("Aug")) month = "August";
    if (date.includes("Sep")) month = "September";
    if (date.includes("Oct")) month = "October";
    if (date.includes("Nov")) month = "November";
    if (date.includes("Dec")) month = "December";
    
    return {
      date: date,
      amount: amount,
      month: month,
      category: category
    };
  });

// Calculate monthly totals
const monthlyTotals = {};
let grandTotal = 0;

transferList.forEach(transfer => {
  if (transfer.month === "Unknown") return;
  
  grandTotal += transfer.amount;
  
  if (!monthlyTotals[transfer.month]) {
    monthlyTotals[transfer.month] = {
      total: 0,
      count: 0,
      categories: {}
    };
  }
  
  monthlyTotals[transfer.month].total += transfer.amount;
  monthlyTotals[transfer.month].count += 1;
  
  // Track category spending
  if (!monthlyTotals[transfer.month].categories[transfer.category]) {
    monthlyTotals[transfer.month].categories[transfer.category] = 0;
  }
  monthlyTotals[transfer.month].categories[transfer.category] += transfer.amount;
});

// Display monthly summary
dv.paragraph("### Monthly Summary");

const monthRows = [];
for (const [month, data] of Object.entries(monthlyTotals)) {
  monthRows.push([
    month,
    `$${data.total.toFixed(2)}`,
    `${data.count} transactions`
  ]);
}

// Add total row
monthRows.push([
  "**Total**",
  `**$${grandTotal.toFixed(2)}**`,
  `**${transferList.length} transactions**`
]);

dv.table(["Month", "Amount", "Count"], monthRows);

// Display category breakdown
dv.paragraph("### Category Breakdown");

const categoryTotals = {};
transferList.forEach(transfer => {
  if (!categoryTotals[transfer.category]) {
    categoryTotals[transfer.category] = 0;
  }
  categoryTotals[transfer.category] += transfer.amount;
});

const categoryRows = [];
for (const [category, total] of Object.entries(categoryTotals)) {
  categoryRows.push([
    category,
    `$${total.toFixed(2)}`,
    `${((total / grandTotal) * 100).toFixed(1)}%`
  ]);
}

dv.table(["Category", "Total", "Percentage"], categoryRows);

// Display all transfers with running total
dv.paragraph("### Transaction Log");
let runningTotal = 0;
const transferRows = [];

transferList.forEach(transfer => {
  runningTotal += transfer.amount;
  transferRows.push([
    transfer.date,
    `$${transfer.amount.toFixed(2)}`,
    transfer.category,
    `$${runningTotal.toFixed(2)}`
  ]);
});

dv.table(["Date", "Amount", "Category", "Running Total"], transferRows);

// Monthly category breakdown
dv.paragraph("### Monthly Category Breakdown");
for (const [month, data] of Object.entries(monthlyTotals)) {
  dv.paragraph(`#### ${month}`);
  
  const monthlyCategoryRows = [];
  for (const [category, amount] of Object.entries(data.categories)) {
    monthlyCategoryRows.push([
      category,
      `$${amount.toFixed(2)}`,
      `${((amount / data.total) * 100).toFixed(1)}%`
    ]);
  }
  
  dv.table(["Category", "Amount", "Percentage"], monthlyCategoryRows);
}
```