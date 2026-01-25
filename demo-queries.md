## 1. Show the Entire Graph

```cypher
MATCH (n)-[r]->(m)
RETURN n, r, m;
```
## What to notice: This returns everything you loaded — no joins, no tables.

## 2. List All Characters and Their Groups
```cypher
MATCH (c:Character)
RETURN c.name AS character, c.group AS group
ORDER BY group;
```
## What to notice: Nodes can have properties that describe them.

## 3. Show the Entire Graph

```cypher
MATCH (n)-[r]->(m)
RETURN n, r, m;
```
## What to notice: This returns everything you loaded — no joins, no tables.

## 3. Who Is Friends With Whom?
```cypher
MATCH (a:Character)-[:FRIENDS_WITH]->(b:Character)
RETURN a.name AS person, collect(b.name) AS friends;
```
## What to notice: Relationships are first-class citizens in a graph.
