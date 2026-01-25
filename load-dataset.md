## Stranger Graphs Booth Demo Dataset

This dataset is designed for live Neo4j Aura Free demos.

```cypher
// Stranger Graphs Booth Demo Dataset
// Safe to run in a fresh Aura Free database

CREATE CONSTRAINT character_name IF NOT EXISTS
FOR (c:Character)
REQUIRE c.name IS UNIQUE;

CREATE CONSTRAINT location_name IF NOT EXISTS
FOR (l:Location)
REQUIRE l.name IS UNIQUE;

WITH [
  {name:'Eleven', group:'Hawkins Kids'},
  {name:'Mike', group:'Hawkins Kids'},
  {name:'Dustin', group:'Hawkins Kids'},
  {name:'Lucas', group:'Hawkins Kids'},
  {name:'Max', group:'Hawkins Kids'},
  {name:'Will', group:'Hawkins Kids'},
  {name:'Hopper', group:'Adults'},
  {name:'Joyce', group:'Adults'},
  {name:'Vecna', group:'Upside Down'}
] AS characters
UNWIND characters AS c
MERGE (:Character {name:c.name, group:c.group});

WITH ['Hawkins', 'Starcourt Mall', 'Upside Down'] AS locations
UNWIND locations AS l
MERGE (:Location {name:l});

MATCH
  (eleven:Character {name:'Eleven'}),
  (mike:Character {name:'Mike'}),
  (dustin:Character {name:'Dustin'}),
  (lucas:Character {name:'Lucas'}),
  (max:Character {name:'Max'}),
  (will:Character {name:'Will'}),
  (hopper:Character {name:'Hopper'}),
  (joyce:Character {name:'Joyce'}),
  (vecna:Character {name:'Vecna'}),
  (hawkins:Location {name:'Hawkins'}),
  (mall:Location {name:'Starcourt Mall'}),
  (upside:Location {name:'Upside Down'})

MERGE (eleven)-[:FRIENDS_WITH]->(mike)
MERGE (eleven)-[:FRIENDS_WITH]->(dustin)
MERGE (eleven)-[:FRIENDS_WITH]->(lucas)
MERGE (eleven)-[:FRIENDS_WITH]->(max)
MERGE (mike)-[:FRIENDS_WITH]->(will)

MERGE (hopper)-[:PROTECTS]->(eleven)
MERGE (joyce)-[:PROTECTS]->(will)

MERGE (vecna)-[:ENEMY_OF]->(eleven)
MERGE (vecna)-[:OPERATES_IN]->(upside)

MERGE (eleven)-[:VISITED]->(hawkins)
MERGE (eleven)-[:VISITED]->(mall)
MERGE (vecna)-[:VISITED]->(upside);
