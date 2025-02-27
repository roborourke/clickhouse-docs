---
sidebar_label: Performance Tips
sidebar_position: 5
keywords: [clickhouse, go, client, high-level, api, database, sql, performance]
slug: /en/integrations/go/clickhouse-go/performance-tips
description: Performance Tips
---

# Performance Tips

* Utilize the ClickHouse API where possible, especially for primitive types. This avoids significant reflection and indirection.
* Be specific with your types when inserting data. While the client aims to be flexible, e.g., allowing strings to be parsed for UUIDs or IPs, this requires data validation and incurs a cost at insert time.
* Use column-oriented inserts where possible. Again these should be strongly typed, avoiding the need for the client to convert your values.
* If using the JSON type, encoding of structs and maps to a columnar format is done on the client. This requires reflection, which can be expensive and more work for the client. Conversely, it requires less computation by ClickHouse at insert time. To shift computation to ClickHouse, insert data as a string. Where this work is performed is a design decision but ClickHouse will be more performant if you have cluster resource capacity.
* Follow ClickHouse [recommendations](https://clickhouse.com/docs/en/sql-reference/statements/insert-into/#performance-considerations) for optimal insert performance.
