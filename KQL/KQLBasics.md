# KQL Basics

This file covers the basics of Kusto Query Language (KQL). 

Kusto Query Language (KQL) is the query language used to perform analysis on data to create Analytics, Workbooks, and perform Hunting in Microsoft Sentinel and Microsoft Defender XDR. Understanding basic KQL statement structure provides the foundation to build more complex statements.

You're a Security Operations Analyst working at a company that is implementing Microsoft Sentinel. You're responsible for performing log data analysis to search for malicious activity, display visualizations, and perform threat hunting. To query log data, you use the Kusto Query Language (KQL).

---

# 🎯 KQL Basics Cheat Sheet

## 🟢 What is KQL?

**Kusto Query Language (KQL)** is the query language used in:

- Azure Monitor Logs
- Log Analytics
- Microsoft Sentinel

It's **read-only** and optimized for:

- Searching logs
- Aggregating data
- Building charts

---

## 🟢 Basic Query Structure

A query looks like this:

```kql
TableName
| operator1
| operator2
| ...
```

✅ **Example:**

```kql
SigninLogs
| where ResultType == "50074"
| project UserPrincipalName, IPAddress, TimeGenerated
```

---

## 🟢 Most Common Operators

| Operator   | What it does                | Example                |
|------------|----------------------------|------------------------|
| `where`    | Filters rows                | | where EventID == 4625 |
| `project`  | Selects and renames columns | | project TimeGenerated, UserPrincipalName |
| `extend`   | Creates calculated columns  | | extend Hour = datetime_part("hour", TimeGenerated) |
| `summarize`| Groups rows and aggregates  | | summarize Count = count() by UserPrincipalName |
| `order by` | Sorts rows                  | | order by TimeGenerated desc |
| `top`      | Gets top N rows             | | top 10 by Count |
| `distinct` | Removes duplicates          | | distinct UserPrincipalName |
| `render`   | Creates charts              | | render timechart |

---

## 🟢 Filtering (`where`)
Filters rows by condition.

✅ **Example:**

```kql
SecurityEvent
| where EventID == 4625
| where AccountType == "User"
```

**Common operators:**

- `==` equal
- `!=` not equal
- `contains` substring match
- `startswith` / `endswith`
- `in` list membership
- `has` (fast substring match)

---

## 🟢 Selecting Columns (`project`)
Choose which columns to show (and rename them).

✅ **Example:**

```kql
SigninLogs
| project TimeGenerated, UserPrincipalName, IP = IPAddress
```

---

## 🟢 Creating New Columns (`extend`)
Adds calculated or extracted columns.

✅ **Example:**

```kql
SigninLogs
| extend Hour = datetime_part("hour", TimeGenerated)
```

---

## 🟢 Aggregating (`summarize`)
Groups rows and calculates aggregates.

✅ **Example:**

```kql
SigninLogs
| summarize Count = count() by UserPrincipalName
```

**Common aggregates:**

- `count()`
- `avg()`
- `sum()`
- `max()`
- `min()`

---

## 🟢 Sorting (`order by`)
Sorts your output.

✅ **Example:**

```kql
SigninLogs
| order by TimeGenerated desc
```

---

## 🟢 Removing Duplicates (`distinct`)

✅ **Example:**

```kql
SigninLogs
| distinct UserPrincipalName
```

---

## 🟢 Rendering Charts (`render`)
Visualizes your results.

✅ **Example:**

```kql
SigninLogs
| summarize count() by bin(TimeGenerated, 1h)
| render timechart
```

---

## 🟢 Time Filters
`TimeGenerated` is almost always used to filter time.

✅ **Last 7 days:**

```kql
| where TimeGenerated > ago(7d)
```

✅ **Last hour:**

```kql
| where TimeGenerated > ago(1h)
```

---

## 🟢 Tips for the Exam

- **Livestream queries:** ❌ No time filters (`ago()` not allowed).
- **Custom detection rules:** Must output:
  - `Timestamp`
  - `ReportId`
- Use `has` or `contains` for text searches.

---

## 🟢 Quick Memory Tip

| KQL Operator | What it does         |
|--------------|---------------------|
| `where`      | filter rows         |
| `project`    | select columns      |
| `extend`     | add columns         |
| `summarize`  | group and count     |
| `render`     | show charts         |
