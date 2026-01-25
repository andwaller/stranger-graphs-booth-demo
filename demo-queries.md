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
2. List All Characters and Their Groups
What to notice: Nodes can have properties that describe them.

MATCH (c:Character)
RETURN c.name AS character, c.group AS group
ORDER BY group;
3. Who Is Friends With Whom? ⭐ LIVE
What to notice: Relationships are first-class citizens in a graph.

MATCH (a:Character)-[:FRIENDS_WITH]->(b:Character)
RETURN a.name AS person, collect(b.name) AS friends;
4. Who Protects Who?
What to notice: Relationship types carry meaning.

MATCH (a:Character)-[:PROTECTS]->(b:Character)
RETURN a.name AS protector, b.name AS protected;
5. Where Have Characters Been?
What to notice: Graphs make traversing different entity types easy.

MATCH (c:Character)-[:VISITED]->(l:Location)
RETURN c.name AS character, collect(l.name) AS locations;
6. Who Operates in the Upside Down?
What to notice: You can filter by both relationships and node properties.

MATCH (c:Character)-[:OPERATES_IN]->(l:Location {name:'Upside Down'})
RETURN c.name;
7. Who Is Connected to Eleven Within Two Hops ⭐ LIVE
What to notice: This is graph thinking — asking about paths, not joins.

MATCH (e:Character {name:'Eleven'})-[*1..2]-(others)
RETURN DISTINCT others.name;
8. Who Are Eleven’s Allies and Enemies?
What to notice: You can query by relationship type, not just data.

MATCH (e:Character {name:'Eleven'})-[r]-(other)
RETURN type(r) AS relationship, other.name AS character;
9. Which Characters Share Locations?
What to notice: Patterns across multiple hops are natural in graphs.

MATCH (c1:Character)-[:VISITED]->(l)<-[:VISITED]-(c2:Character)
WHERE c1 <> c2
RETURN l.name AS location, collect(DISTINCT c1.name) AS characters;
10. Recommendation-Style Query ⭐ LIVE
What to notice: This is how recommendations begin — relationships first.

MATCH (e:Character {name:'Eleven'})
      -[:FRIENDS_WITH]->(:Character)
      -[:FRIENDS_WITH]->(rec)
WHERE NOT (e)-[:FRIENDS_WITH]->(rec)
RETURN DISTINCT rec.name AS recommended_friend;
