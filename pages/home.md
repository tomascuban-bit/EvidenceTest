---
name: Home
assetId: 1e234aba-a10d-4070-9e60-64cd3d47b4bc
type: page
---

# Welcome

Testing a simple dashboard

```sql clean_sales
SELECT
  "Employee Name" as employee_name,
  "Role" as role,
  "Region" as region,
  "Reporting Manager" as reporting_manager,
  "Opportunities Created" as opportunities_created,
  "Deals Closed" as deals_closed,
  "Total Sales ($)" as total_sales,
  "Win Rate (%)" as win_rate
FROM sales_org_dummy_data
ORDER BY total_sales DESC
```

{% dropdown
    id="role_filter"
    data="clean_sales"
    value_column="role"
    title="Role"
/%}

{% dropdown
    id="region_filter"
    data="clean_sales"
    value_column="region"
    title="Region"
/%}

{% dropdown
    id="manager_filter"
    data="clean_sales"
    value_column="reporting_manager"
    title="Reporting Manager"
/%}

```sql sales_data
SELECT employee_name, total_sales
FROM {{clean_sales}}
WHERE {{role_filter.filter}}
  AND {{region_filter.filter}}
  AND {{manager_filter.filter}}
ORDER BY total_sales DESC
```

{% bar_chart
    data="sales_data"
    x="employee_name"
    y="total_sales"
/%}
{% combo_chart
    data="demo.daily_orders"
    x="category"
%}
    {% bar
        y="sum(total_sales)"
    /%}
    {% line
        y="sum(transactions)"
        axis="y2"
    /%}
{% /combo_chart %}
