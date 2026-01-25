# Stranger Graph Thinking Challenge — Demo Queries

Use this page to run Cypher queries **live** during the Stranger Graph Thinking Challenge.

**How it works**
- The facilitator calls out a query number
- Copy that query from this page
- Paste it into **Neo4j Browser**
- Run it together as a group

---

## 1. Show the Entire Graph ⭐ LIVE

> **What to notice:** This returns everything you loaded — no tables, no joins.

```cypher
MATCH (n)-[r]->(m)
RETURN n, r, m;

## 2. List All Characters and Their Groups

> **What to notice:** Nodes can have properties that describe them.

```cypher
MATCH (c:Character)
RETURN c.name AS character, c.group AS group
ORDER BY group;

## 3. Who Is Friends With Whom? ⭐ LIVE

> **What to notice:** Relationships are first-class citizens in a graph.

```cypher
MATCH (a:Character)-[:FRIENDS_WITH]->(b:Character)
RETURN a.name AS person, collect(b.name) AS friends

## 4. Who Protects Who?

> **What to notice:** Relationship types carry meaning — the connection itself tells the story.

```cypher
MATCH (a:Character)-[:PROTECTS]->(b:Character)
RETURN a.name AS protector, b.name AS protected;;
