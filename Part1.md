# Part 1
Dump file link
https://cloud.technikum-wien.at/s/cr2e8mKFQxHEyrr

## Preparation

### Execute import command for newfile_01.csv (x10, once for each file)
```
LOAD CSV WITH HEADERS FROM "file:///newfile_01.csv" AS row
MERGE (u:User {userId: substring(row.userID, 2)}) WITH *
MATCH (m:Movie {imdbId: row.imdbID})
MERGE (u)-[:RATED {rating: toFloat(row.rating), timestamp: apoc.date.parse(row.review_date, "s", "dd MMMMM yyyy")}]->(m)
```

## Tasks

### We need a "User" for ratings
```CREATE (n:User {userId:'99999999999', name: 'Dominik & Ruben'})```

### Select the new user
```
MATCH (n:User)
WHERE n.name = 'Dominik & Ruben'
RETURN n
```
#### or
```
MATCH (u:User)
WHERE u.userId = '99999999999'
RETURN u
```

### Create ratings
#### Titanic(1721) 5* 
```
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '1721'})
CREATE (u)-[:RATED {rating: 5.0, timestamp: timestamp()}]->(m)
```

#### Home Alone (586) 5*
```
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '586'})
CREATE (u)-[:RATED {rating: 5.0, timestamp: timestamp()}]->(m)
```

#### Deadpool (122904) 4*
```
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '122904'})
CREATE (u)-[:RATED {rating: 4.0, timestamp: timestamp()}]->(m)
```

#### Beerfest (47640) 4*
```
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '47640'})
CREATE (u)-[:RATED {rating: 4.0, timestamp: timestamp()}]->(m)
```

#### Scary Movie (3785) 4* 
```
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '3785'})
CREATE (u)-[:RATED {rating: 4.0, timestamp: timestamp()}]->(m)
```

#### Fast and the Furious (46335) 6.8*
```
MATCH (u:User {userId: '99999999999'})
MATCH (m:Movie {movieId: '46335'})
CREATE (u)-[:RATED {rating: 6.8, timestamp: timestamp()}]->(m)
```

###  Get rated movies of user
```
MATCH (u:User {userId: '99999999999'})-[:RATED]->(m:Movie)
RETURN u, m
```

### Get users which also rated a movie similar to me using EUCLIDEAN DISTANCE
```
MATCH (me:User {userId: '99999999999'})-[myRating:RATED]->(m:Movie)<-[otherRating:RATED]-(other:User)
WITH me, other, COLLECT(myRating.rating) AS myRatings,COLLECT(otherRating.rating) AS othersRating, COLLECT(m) AS movies
WHERE other <> me
WITH me, other, gds.similarity.euclideanDistance(myRatings, othersRating) AS similarity,myRatings, othersRating, movies
ORDER BY similarity ASC
LIMIT 5
RETURN other, movies, similarity, myRatings, othersRating
```

### Get users which also rated a movie similar to me using EUCLIDEAN <br/> Desc in that case
```
MATCH (me:User {userId: '99999999999'})-[myRating:RATED]->(m:Movie)<-[otherRating:RATED]-(other:User)
WITH me, other, COLLECT(myRating.rating) AS myRatings,COLLECT(otherRating.rating) AS othersRating, COLLECT(m) AS movies
WHERE other <> me
WITH me, other, gds.similarity.euclidean(myRatings, othersRating) AS similarity,myRatings, othersRating, movies
ORDER BY similarity DESC
LIMIT 5
RETURN other, movies, similarity, myRatings, othersRating
```

### Get users which also rated a movie similar to me using PEARSON <br/> Desc in that case
```
MATCH (me:User {userId: '99999999999'})-[myRating:RATED]->(m:Movie)<-[otherRating:RATED]-(other:User)
WITH me, other, COLLECT(myRating.rating) AS myRatings,COLLECT(otherRating.rating) AS othersRating, COLLECT(m) AS movies
WHERE other <> me
WITH me, other, gds.similarity.pearson(myRatings, othersRating) AS similarity,myRatings, othersRating, movies
ORDER BY similarity DESC
LIMIT 5
RETURN other, movies, similarity, myRatings, othersRating
```

### Get users which also rated a movie similar to me using OVERLAP <br/> Desc in that case
```
MATCH (me:User {userId: '99999999999'})-[myRating:RATED]->(m:Movie)<-[otherRating:RATED]-(other:User)
WITH me, other, COLLECT(myRating.rating) AS myRatings,COLLECT(otherRating.rating) AS othersRating, COLLECT(m) AS movies
WHERE other <> me
WITH me, other, gds.similarity.overlap(myRatings, othersRating) AS similarity,myRatings, othersRating, movies
ORDER BY similarity DESC
LIMIT 5
RETURN other, movies, similarity, myRatings, othersRating
```

### Get users which also rated a movie similar to me using JACCARD <br/> Desc in that case
```
MATCH (me:User {userId: '99999999999'})-[myRating:RATED]->(m:Movie)<-[otherRating:RATED]-(other:User)
WITH me, other, COLLECT(myRating.rating) AS myRatings,COLLECT(otherRating.rating) AS othersRating, COLLECT(m) AS movies
WHERE other <> me
WITH me, other, gds.similarity.jaccard(myRatings, othersRating) AS similarity,myRatings, othersRating, movies
ORDER BY similarity DESC
LIMIT 5
RETURN other, movies, similarity, myRatings, othersRating
```

### Get users which also rated a movie similar to me using COSINE <br/> Desc in that case
```
MATCH (me:User {userId: '99999999999'})-[myRating:RATED]->(m:Movie)<-[otherRating:RATED]-(other:User)
WITH me, other, COLLECT(myRating.rating) AS myRatings,COLLECT(otherRating.rating) AS othersRating, COLLECT(m) AS movies
WHERE other <> me
WITH me, other, gds.similarity.cosine(myRatings, othersRating) AS similarity,myRatings, othersRating, movies
ORDER BY similarity DESC
LIMIT 5
RETURN other, movies, similarity, myRatings, othersRating
```

### With those user ids we can see which movies the other user also rated highly. <br/> Get all users the user rated with \> 8.0
```
MATCH (u:User {userId: '<similar user id>'})-[r:RATED]->(m:Movie)
where r.rating > 8.0
RETURN u, m
```
