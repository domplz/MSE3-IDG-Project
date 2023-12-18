### execute command for newfile_01.csv (x10 for every file)
LOAD CSV WITH HEADERS FROM "file:///newfile_01.csv" AS row
MERGE (u:User {userId: substring(row.userID, 2)}) WITH *
MATCH (m:Movie {imdbId: row.imdbID})
MERGE (u)-[:RATED {rating: toFloat(row.rating), timestamp: apoc.date.parse(row.review_date, "s", "dd MMMMM yyyy")}]->(m)

## we need a "User" for ratings
Create (n:User {userId:'99999999999', name: 'Dominik Pilz'})

## select the new user 
match (n:User)
where n.name = 'Dominik Pilz'
return n
## or
MATCH (u:User)
where u.userId = '99999999999'
RETURN u

## create ratings
## titanic(1721) 5* 
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '1721'})
CREATE (u)-[:RATED {rating: 5.0, timestamp: timestamp()}]->(m)

## home alone (586) 5*
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '586'})
CREATE (u)-[:RATED {rating: 5.0, timestamp: timestamp()}]->(m)

## deadpool (122904) 4*
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '122904'})
CREATE (u)-[:RATED {rating: 4.0, timestamp: timestamp()}]->(m)

## beerfest (47640) 4*
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '47640'})
CREATE (u)-[:RATED {rating: 4.0, timestamp: timestamp()}]->(m)

## scary movie (3785) 4* 
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '3785'})
CREATE (u)-[:RATED {rating: 4.0, timestamp: timestamp()}]->(m)

## Fast and the Furious (46335) 4*
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '46335'})
CREATE (u)-[:RATED {rating: 4.0, timestamp: timestamp()}]->(m)


##  get rated movies of user
MATCH (u:User {userId: '99999999999'})-[:RATED]->(m:Movie)
RETURN u, m