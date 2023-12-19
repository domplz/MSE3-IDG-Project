## Download VirtualBox and Sparql.ova
Follow instructions of
https://moodle.technikum-wien.at/pluginfile.php/2031623/mod_folder/content/0/Lesson-5-RDF-and-SPARQL.pdf?forcedownload=1

## open http://localhost:9090/sparql

# PART A:

## create \<SocialNetwork\> graph
CREATE GRAPH \<SocialNetwork\>

## insert provided data
INSERT DATA {GRAPH \<SocialNetwork\> {
\<http://example.neo4j/john\> \<http://www.lib.org/schema#firstName\> "John" .
\<http://example.neo4j/john\> \<http://www.lib.org/schema#lastName\> "Cook" .
\<http://example.neo4j/john\> \<http://www.lib.org/schema#gender\> "male" .
\<http://example.neo4j/john\> \<http://www.lib.org/schema#country\> "Chile" .
\<http://example.neo4j/julie\> \<http://www.lib.org/schema#firstName\> "Julie" .
\<http://example.neo4j/julie\> \<http://www.lib.org/schema#lastName\> "Freud" .
\<http://example.neo4j/julie\> \<http://www.lib.org/schema#country\> "Chile" .
\<http://example.neo4j/peter\> \<http://www.lib.org/schema#firstName\> "Peter" .
\<http://example.neo4j/peter\> \<http://www.lib.org/schema#lastName\> "Norvig" .
\<http://example.neo4j/peter\> \<http://www.lib.org/schema#country\> "US" .
\<http://example.neo4j/peter\> \<http://www.lib.org/schema#gender\> "male" .
\<http://example.neo4j/mary\> \<http://www.lib.org/schema#firstName\> "Mary" .
\<http://example.neo4j/mary\> \<http://www.lib.org/schema#lastName\> "Lindt" .
\<http://example.neo4j/mary\> \<http://www.lib.org/schema#country\> "Sweden" .
\<http://example.neo4j/mary\> \<http://www.lib.org/schema#gender\> "female" .
\<http://example.neo4j/mary\> \<http://www.lib.org/schema#knows\> \<http://example.neo4j/peter\> .
\<http://example.neo4j/john\> \<http://www.lib.org/schema#knows\> \<http://example.neo4j/julie\> .
\<http://example.neo4j/julie\> \<http://www.lib.org/schema#knows\> \<http://example.neo4j/john\> .
\<http://example.neo4j/julie\> \<http://www.lib.org/schema#follows\> \<http://example.neo4j/john\> .
\<http://example.neo4j/john\> \<http://www.lib.org/schema#follows\> \<http://example.neo4j/peter\> .
\<http://example.neo4j/peter\> \<http://www.lib.org/schema#follows\> \<http://example.neo4j/mary\> .
\<http://example.neo4j/mary\> \<http://www.lib.org/schema#follows\> \<http://example.neo4j/julie\> .
\<http://example.neo4j/peter\> \<http://www.lib.org/schema#dislikes\> \<http://example.neo4j/john\> .
\<http://example.neo4j/john\> \<http://www.w3.org/1999/02/22-rdf-syntax-ns#type\> \<http://xmlns.com/foaf/0.1/Person\> .
\<http://example.neo4j/julie\> \<http://www.w3.org/1999/02/22-rdf-syntax-ns#type\> \<http://xmlns.com/foaf/0.1/Person\> .
\<http://example.neo4j/peter\> \<http://www.w3.org/1999/02/22-rdf-syntax-ns#type\> \<http://xmlns.com/foaf/0.1/Person\> .
\<http://example.neo4j/mary\> \<http://www.w3.org/1999/02/22-rdf-syntax-ns#type\> \<http://xmlns.com/foaf/0.1/Person\> .
\<http://example.neo4j/p1\> \<http://www.lib.org/schema#content\> "I love U2" .
\<http://example.neo4j/p1\> \<http://www.lib.org/schema#language\> "Chile" .
\<http://example.neo4j/p2\> \<http://www.lib.org/schema#content\> "Queen is awesome" .
\<http://example.neo4j/p3\> \<http://www.lib.org/schema#content\> "I hate U2" .
\<http://example.neo4j/p1\> \<http://www.w3.org/1999/02/22-rdf-syntax-ns#type\> \<http://xmlns.com/foaf/0.1/Post\> .
\<http://example.neo4j/p2\> \<http://www.w3.org/1999/02/22-rdf-syntax-ns#type\> \<http://xmlns.com/foaf/0.1/Post\> .
\<http://example.neo4j/p3\> \<http://www.w3.org/1999/02/22-rdf-syntax-ns#type\> \<http://xmlns.com/foaf/0.1/Post\> .
\<http://example.neo4j/t1\> \<http://www.lib.org/schema#content\> "U2" .
\<http://example.neo4j/t1\> \<http://www.w3.org/1999/02/22-rdf-syntax-ns#type\> \<http://xmlns.com/foaf/0.1/Tag\> .
\<http://example.neo4j/t2\> \<http://www.lib.org/schema#content\> "Queen" .
\<http://example.neo4j/t2\> \<http://www.w3.org/1999/02/22-rdf-syntax-ns#type\> \<http://xmlns.com/foaf/0.1/Tag\> .
\<http://example.neo4j/t3\> \<http://www.lib.org/schema#content\> "U2" .
\<http://example.neo4j/t3\> \<http://www.w3.org/1999/02/22-rdf-syntax-ns#type\> \<http://xmlns.com/foaf/0.1/Tag\> .
\<http://example.neo4j/p1\> \<http://www.lib.org/schema#hasTag\> \<http://example.neo4j/t1\> .
\<http://example.neo4j/p2\> \<http://www.lib.org/schema#hasTag\> \<http://example.neo4j/t2\> .
\<http://example.neo4j/p3\> \<http://www.lib.org/schema#hasTag\> \<http://example.neo4j/t1\> .
\<http://example.neo4j/julie\> \<http://www.lib.org/schema#likes\> \<http://example.neo4j/p1\> .
\<http://example.neo4j/john\> \<http://www.lib.org/schema#likes\> \<http://example.neo4j/p1\> .
\<http://example.neo4j/john\> \<http://www.lib.org/schema#dislikes\> \<http://example.neo4j/p2\> .
\<http://example.neo4j/peter\> \<http://www.lib.org/schema#dislikes\> \<http://example.neo4j/p3\> .
\<http://example.neo4j/john\> \<http://www.lib.org/schema#dislikes\> \<http://example.neo4j/p3\> .
\<http://example.neo4j/julie\> \<http://www.lib.org/schema#dislikes\> \<http://example.neo4j/p3\> .
\<http://example.neo4j/peter\> \<http://www.lib.org/schema#likes\> \<http://example.neo4j/p2\> .
}}

## check inserted triplets
SELECT *
FROM \<SocialNetwork\>
WHERE { ?s ?p ?o }

# PART B
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX lib: <http://www.lib.org/schema#>

SELECT (COUNT(?interaction) as ?totalLikesDislikes)
WHERE {
  ?person (foaf:likes|lib:dislikes) ?post .
  ?post lib:hasTag ?tag .
  ?tag lib:content "U2" OR ?tag lib:content "Queen" .
  ?interaction ?likeDislikeProperty ?post .
}

# Part C
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX lib: <http://www.lib.org/schema#>

SELECT ?name ?lastName ?gender
WHERE {
  ?follower foaf:follows ?person .
  ?person (foaf:likes|lib:dislikes) ?post .
  ?post lib:hasTag ?tag .
  ?tag lib:content "U2" .
  ?follower (foaf:likes|lib:dislikes) ?otherPost .
  FILTER (
    (COUNT(DISTINCT ?otherPost) >= 2) || 
    EXISTS { 
      ?follower foaf:likes ?u2Post .
      ?u2Post lib:hasTag ?u2Tag .
      ?u2Tag lib:content "U2" 
    }
  )
  ?person foaf:firstName ?name .
  ?person foaf:lastName ?lastName .
  ?person foaf:gender ?gender .
}
GROUP BY ?name ?lastName ?gender
HAVING COUNT(DISTINCT ?otherPost) >= 2 || COUNT(DISTINCT ?u2Post) >= 1

## ODER

PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX lib: <http://www.lib.org/schema#>

SELECT ?name ?lastName ?gender
WHERE {
  ?follower foaf:follows ?person .
  ?person (foaf:likes|lib:dislikes) ?post .
  ?post lib:hasTag ?tag .
  ?tag lib:content "U2" .
  ?follower (foaf:likes|lib:dislikes) ?otherPost .
  FILTER (
    (COUNT(DISTINCT ?otherPost) >= 2) || 
    EXISTS { 
      ?follower foaf:likes ?u2Post .
      ?u2Post lib:hasTag ?u2Tag .
      ?u2Tag lib:content "U2" 
    }
  )
  ?person foaf:firstName ?name .
  ?person foaf:lastName ?lastName .
  ?person foaf:gender ?gender .
}
GROUP BY ?name ?lastName ?gender
