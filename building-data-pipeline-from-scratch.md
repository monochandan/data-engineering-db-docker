#### Building data pipeline from scratch

    Documents/elt
    touch elt_script.py
    touch docker-compose.yaml

    docker compose up


# version mismatch between the PostgreSQL server and the pg_dump client.
# The PostgreSQL server is version 16.3, while the pg_dump client is version 15.6.

so, in docker-compose.yaml file:

    source_postgres:
        # list the image
        image: postgres:15.6 ## changed from latest

    destination_postgres:
        image: postgres:15.6 # changed from latest
