## 1. Show the Entire Graph

> **What to notice:** This returns everything you loaded — no joins, no tables.

```cypher
MATCH (n)-[r]->(m)
RETURN n, r, m;
---
