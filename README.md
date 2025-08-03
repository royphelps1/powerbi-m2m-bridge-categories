# Power BI: Many-to-Many Bridge Table with Category Filtering

This Power BI project demonstrates how to handle many-to-many relationships using a bridge table, especially when a single product can belong to multiple categories. The solution avoids double-counting and includes dynamic DAX to accurately allocate revenue per category.

## 🔧 Features

- Bridge table: `Bridge_ProductCategory`
- Category dimension: `DimCategory`
- Product dimension: `DimProduct`
- Fact table: `FactSales`
- Date table: `DimDate`
- Custom DAX to handle non-additive metrics by category

## 📊 Key Measures

```DAX
Total Revenue = SUM(FactSales[Revenue])

Total Revenue by Category = 
SUMX(
    FILTER(
        Bridge_ProductCategory,
        Bridge_ProductCategory[CategoryName] IN VALUES(DimCategory[CategoryName])
    ),
    CALCULATE([Total Revenue])
)
