## Clone snomed-database-loader

```bash
darwin@LAPTOP-MMLBEP53:~/undergit/SnomedCT-Property-Graph$ git clone https://github.com/IHTSDO/snomed-database-loader.git
```

## Install py2neo

```bash
darwin@LAPTOP-MMLBEP53:~/undergit/SnomedCT-Property-Graph$ python -m venv venv
darwin@LAPTOP-MMLBEP53:~/undergit/SnomedCT-Property-Graph$ source venv/bin/activate
(venv) darwin@LAPTOP-MMLBEP53:~/undergit/SnomedCT-Property-Graph$ pip install py2neo
```

## Install Neo4j

```bash
(venv) darwin@LAPTOP-MMLBEP53:~/undergit/SnomedCT-Property-Graph$ docker run \
    --name neo4j \
    -p 7474:7474 -p 7687:7687 \
    -e NEO4J_AUTH=neo4j/password \
    -v $(pwd)/neo4j/data:/data \
    -v $(pwd)/neo4j/conf:/conf \
    -d neo4j:4.4.39-enterprise \
    --env=NEO4J_ACCEPT_LICENSE_AGREEMENT=yes
  
(venv) darwin@LAPTOP-MMLBEP53:~/undergit/SnomedCT-Property-Graph$ docker ps
CONTAINER ID   IMAGE                     COMMAND                  CREATED         STATUS         PORTS                                                      NAMES
50fc25ce6311   neo4j:4.4.39-enterprise   "tini -g -- /startup…"   5 seconds ago   Up 3 seconds   0.0.0.0:7474->7474/tcp, 7473/tcp, 0.0.0.0:7687->7687/tcp   neo4j
```

## Build the database

```bash
(venv) darwin@LAPTOP-MMLBEP53:~/undergit/SnomedCT-Property-Graph$ python snomed-database-loader/NEO4J/snomed_g_graphdb_build_tools.py db_build \
  --release_type full \
  --mode build \
  --action create \
  --rf2 /home/darwin/undergit/SnomedCT-Property-Graph/snomed_release/SnomedCT_InternationalRF2_PRODUCTION_20230901T120000Z/Full \
  --neopw password \
  --output_dir Output
SNOMED_G bin directory [/home/darwin/undergit/SnomedCT-Property-Graph/snomed-database-loader/NEO4J/]
sequence did not exist, primed
JOB_START
FIND_ROLENAMES
FIND_ROLEGROUPS

```