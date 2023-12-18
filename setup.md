# run docker compose up for the first time

# copy recommendations.db.dump to /mnt/import
# copy plugins (apoc core/extedned, neo4j graph data science, osm, postgres) into plugins folder

# run in docker exec
# --overwrite-destination=true (if exists)
neo4j-admin database load recommendations.db --from-path /import

# show dbs
neo4j-admin database info


# edit neo4j.conf
# das wird gebraucht um die db auszuwählen anscheinend
# webdb.db = gewünschter db name
dbms.default_database=recommendations.db
dbms.allow_upgrade=true
dbms.directories.import=import
# activate plugins: First copy plugin files to mnt/var/lib/neo4j/plugins
dbms.security.procedures.unrestricted=apoc.*,apoc.algo.*, algo.*
dbms.security.procedures.allowlist=apoc.coll.*,apoc.load.*,apoc.*

# container restart
neo4j stop