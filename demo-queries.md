## 1. Show the Entire Graph

```cypher
MATCH (n)-[r]->(m)
RETURN n, r, m;
```
## What to notice: This returns everything you loaded — no joins, no tables.

## 2. List All Characters and Their Groups
MATCH (c:Character)
RETURN c.name AS character, c.group AS group
ORDER BY group;
```
## What to notice: Nodes can have properties that describe them.
