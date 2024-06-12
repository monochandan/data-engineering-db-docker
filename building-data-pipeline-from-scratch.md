#### Building data pipeline from scratch

    Documents/elt
    touch elt_script.py
    touch docker-compose.yaml

    docker compose up
    docker compose down



# version mismatch between the PostgreSQL server and the pg_dump client.
# The PostgreSQL server is version 16.3, while the pg_dump client is version 15.6.

so, in docker-compose.yaml file:

    source_postgres:
        # list the image
        image: postgres:15.6 ## changed from latest

    destination_postgres:
        image: postgres:15.6 # changed from latest

open anotehr bash terminal (dont compose down the previous one)

    winpty docker exec -it elt-destination_postgres-1 psql -U postgres

To connect to database destination_db:

    \c destination_db
    
To see the tables:

    \dt

    <img width="382" alt="image" src="https://github.com/monochandan/data-engineering-db-docker/assets/29684226/2002fbfc-e80c-47c4-988d-294c28668acf">
