## 1. Show the Entire Graph ⭐ LIVE

```cypher
MATCH (n)-[r]->(m)
RETURN n, r, m;
What to notice: This returns everything you loaded — no tables, no joins.

2. List All Characters and Their Groups
MATCH (c:Character)
RETURN c.name AS character, c.group AS group
ORDER BY group;
What to notice: Nodes can have properties that describe them.

3. Who Is Friends With Whom? ⭐ LIVE
MATCH (a:Character)-[:FRIENDS_WITH]->(b:Character)
RETURN a.name AS person, collect(b.name) AS friends;
What to notice: Relationships are first-class citizens in a graph.

4. Who Protects Who?
MATCH (a:Character)-[:PROTECTS]->(b:Character)
RETURN a.name AS protector, b.name AS protected;
What to notice: Relationship types carry meaning — the connection itself tells the story.

5. Where Have Characters Been?
MATCH (c:Character)-[:VISITED]->(l:Location)
RETURN c.name AS character, collect(l.name) AS locations;
What to notice: Graphs make traversing different entity types easy.

6. Who Operates in the Upside Down?
MATCH (c:Character)-[:OPERATES_IN]->(l:Location {name:'Upside Down'})
RETURN c.name;
What to notice: You can filter by both relationships and node properties.

7. Who Is Connected to Eleven Within Two Hops ⭐ LIVE
MATCH (e:Character {name:'Eleven'})-[*1..2]-(others)
RETURN DISTINCT others.name;
What to notice: This is graph thinking — asking about paths, not joins.

8. Who Are Eleven’s Allies and Enemies?
MATCH (e:Character {name:'Eleven'})-[r]-(other)
RETURN type(r) AS relationship, other.name AS character;
What to notice: You can query by relationship type, not just data.

9. Which Characters Share Locations?
MATCH (c1:Character)-[:VISITED]->(l)<-[:VISITED]-(c2:Character)
WHERE c1 <> c2
RETURN l.name AS location, collect(DISTINCT c1.name) AS characters;
What to notice: Patterns across multiple hops are natural in graphs.

10. Recommendation-Style Query ⭐ LIVE
MATCH (e:Character {name:'Eleven'})
      -[:FRIENDS_WITH]->(:Character)
      -[:FRIENDS_WITH]->(rec)
WHERE NOT (e)-[:FRIENDS_WITH]->(rec)
RETURN DISTINCT rec.name AS recommended_friend;
What to notice: This is how recommendations begin — relationships first.

