# KQL (Kusto Query Language) Notes

## 📌 Introduction
Kusto Query Language (KQL) is a powerful query language used for analyzing large data sets in **Azure Monitor, Log Analytics, Azure Sentinel, and Application Insights**. It is a **read-only** query language that enables interactive data exploration.

---

## 🔹 Basic Query Structure
KQL queries are structured as a sequence of commands separated by pipes (`|`).

```kql
TableName
| where Condition
| project Column1, Column2
| order by Column1 desc
```

---

## 🔍 Filtering Data
Use `where` to filter data based on conditions.

```kql
SecurityEvent
| where TimeGenerated > ago(7d)
| where EventID == 4625
```
- **`ago(7d)`** → Retrieves data from the last 7 days.
- **`EventID == 4625`** → Filters failed login attempts.

---

## 📑 Selecting Specific Columns
Use `project` to select the columns you need.

```kql
SecurityEvent
| project TimeGenerated, Computer, EventID
```

---

## 🔄 Sorting Data
Use `order by` to sort results.

```kql
SecurityEvent
| order by TimeGenerated desc
```

---

## 🔢 Counting Records
Use `summarize count()` to count occurrences.

```kql
SecurityEvent
| where EventID == 4624
| summarize count()
```

---

## 📊 Grouping Data
Use `summarize` to group results.

```kql
SecurityEvent
| summarize count() by EventID
```

---

## 🔗 Joining Tables
Join two tables on a common column.

```kql
Table1
| join kind=inner (Table2) on CommonColumn
```

> **Types of Joins:**
> - `inner` → Returns matching records in both tables.
> - `leftouter` → Returns all records from the left table and matching records from the right.
> - `rightouter` → Returns all records from the right table and matching records from the left.

---

## 🆕 Creating New Columns
Use `extend` to create a new column.

```kql
SecurityEvent
| extend LoginType = iff(EventID == 4624, "Success", "Failure")
```

---

## 📌 Parsing JSON Data
Use `todynamic()` to parse JSON fields.

```kql
Table
| extend ParsedField = todynamic(JsonColumn).FieldName
```

---

## 🔍 Advanced Filtering with Regex
Use `matches regex` for advanced pattern matching.

```kql
SecurityEvent
| where Account contains "admin"
| where CommandLine matches regex ".*powershell.*"
```

---

## ⏳ Time-Based Aggregation
Use `bin()` to group data into time intervals.

```kql
SecurityEvent
| summarize count() by bin(TimeGenerated, 1h)
```

---

## 🎯 Conclusion
KQL is an efficient way to analyze logs and detect security incidents. Mastering KQL can enhance your ability to work in **SOC (Security Operations Center)** roles and improve threat detection in **Microsoft Sentinel**.

🚀 Want to practice more? Try running these queries in **Azure Log Analytics**!

---

