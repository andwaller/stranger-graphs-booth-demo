## 1. Show the Entire Graph

```cypher
MATCH (n)-[r]->(m)
RETURN n, r, m;
```
## What to notice: This returns everything you loaded — no joins, no tables.
