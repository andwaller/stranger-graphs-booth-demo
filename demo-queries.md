## 1. Show the Entire Graph

```cypher
MATCH (n)-[r]->(m)
RETURN n, r, m;
### The critical line is:
