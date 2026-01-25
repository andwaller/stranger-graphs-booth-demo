# Stranger Graphs – Cypher Demo & Challenge Queries

Welcome to the **Stranger Graph Thinking Challenge**.

These 10 Cypher queries are designed to:
- be approachable for first-time Neo4j users
- demonstrate core graph concepts
- build from simple visualization → real graph thinking

Run them **in order** for the best experience.

---

## 1️⃣ Show the Entire Graph

Start by visualizing everything you just loaded.

```cypher
MATCH (n)-[r]->(m)
RETURN n, r, m;
💡 No tables. No joins. This is the graph.

2️⃣ List All Characters and Their Groups
MATCH (c:Character)
RETURN c.name AS character, c.group AS group
ORDER BY group;
💡 Nodes can have properties that describe them.

3️⃣ Who Is Friends With Whom?
MATCH (a:Character)-[:FRIENDS_WITH]->(b:Character)
RETURN a.name AS person, collect(b.name) AS friends;
💡 Relationships are first-class citizens in a graph.

4️⃣ Who Protects Who?
MATCH (a:Character)-[:PROTECTS]->(b:Character)
RETURN a.name AS protector, b.name AS protected;
💡 Relationship types carry meaning.

5️⃣ Where Have Characters Been?
MATCH (c:Character)-[:VISITED]->(l:Location)
RETURN c.name AS character, collect(l.name) AS locations;
💡 Graphs make traversing different entity types easy.

6️⃣ Who Operates in the Upside Down?
MATCH (c:Character)-[:OPERATES_IN]->(l:Location {name:'Upside Down'})
RETURN c.name;
💡 Filter by both relationship and node properties.

7️⃣ Who Is Connected to Eleven Within Two Hops ⭐
MATCH (e:Character {name:'Eleven'})-[*1..2]-(others)
RETURN DISTINCT others.name;
💥 This is graph thinking.
Ask questions about paths, not joins.

8️⃣ Who Are Eleven’s Allies and Enemies?
MATCH (e:Character {name:'Eleven'})-[r]-(other)
RETURN type(r) AS relationship, other.name AS character;
💡 You can query by relationship type, not just data.

9️⃣ Which Characters Share Locations?
MATCH (c1:Character)-[:VISITED]->(l)<-[:VISITED]-(c2:Character)
WHERE c1 <> c2
RETURN l.name AS location, collect(DISTINCT c1.name) AS characters;
💡 Patterns across multiple hops are natural in graphs.

🔟 Recommendation-Style Query (Light “Wow” Moment)
MATCH (e:Character {name:'Eleven'})-[:FRIENDS_WITH]->(:Character)-[:FRIENDS_WITH]->(rec)
WHERE NOT (e)-[:FRIENDS_WITH]->(rec)
RETURN DISTINCT rec.name AS recommended_friend;
