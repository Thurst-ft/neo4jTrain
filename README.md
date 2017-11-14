# neo4jTrain
repo for neo4j recommendations training stuff

## Details:
http://bit.ly/polycon-neo4j

## Resource
Using data from this api
https://www.meetup.com/meetup_api/

Useful for complex queries
https://github.com/neo4j-contrib/neo4j-apoc-procedures

##
:play https://guides.neo4j.com/reco

### Interesting cypers

```
LOAD CSV WITH HEADERS
 FROM $url + "/groups.csv"
 AS row
 RETURN row
 LIMIT 10
 ```

The $url is the paramter we created in the first step where we set the params/

### Example basic queries

match groups and return count:
```
MATCH (g:Group) RETURN count(*)
```

return tabel of id, name and url name
```
MATCH (g:Group)
 RETURN g.id, g.name, g.urlname
 ```

 Add in constrains

 ```
 CREATE CONSTRAINT ON (t:Topic) ASSERT t.id IS UNIQUE
 ```

 Get constraints
 ```
 CALL db.constraints()
 ```
 Get indexes

 ```
 CALL db.indexes()
 ```

 ```
MERGE (topc:topic )
ON CREATE SET topic.name = "A name" //  Only sets the value if the node does not already exists
ON MATCH SET // will effectively update
SET // will update

```
Exclude really common stuff
ie
```
WHERE size((topic)<-[:HAS_TOPIC]-()) < 100
```
Test where a predicat exist or `NOT`
```
WHERE EXISTS((Group)-[:HAS_REL]->(Topic)))

WHERE NOT EXISTS((Group)-[:HAS_REL]->(Topic)))
```

Don't forget `PROFILE` for analysis

 ## Useful commands

Outputs the schema so you can see the constrains applied etc.
 ```
 :schema
```


Indexes have constraints but constraints don't necessrsary have an index.

Indexes are design to be used to find the starting point.

## Using periodic commits
Can only be used with `LOAD CSV`
flushes after n amount of rows to avoid outOfMemory issues

### Limits
35kb node
15kb rel
65k rel per node
2 to the power of 50 is the limit on nodes
2 ^ 50

### Notes on WITH
sub queryish

Used to capture the query and do some aggregation

- limit number of entries ton to the othe rmatch clause

- filter on agrigate
- separate reading ..


### OPTIONAL MATCH
similar to left join in RDB

## Functions

#### Distance:
Check this but it roughly like this

```
WITH point(longitude: '' latitude '') AS here
WITH point(longitude: '' latitude '') AS there

distance(here, there)
```

#### Time
```
timestamp()
```

##Other examples

Java based example:
https://github.com/graphaware/neo4j-reco
