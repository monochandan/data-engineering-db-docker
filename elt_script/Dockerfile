FROM python:3.8-slim

# install postgresql command-line tools
RUN apt-get update && apt-get install -y postgresql-client

# version mismatch between the PostgreSQL server and the pg_dump client.
# The PostgreSQL server is version 16.3, while the pg_dump client is version 15.6.
# install postgres command line tool version 16
# RUN apt-get update && apt-get install -y wget gnupg2 \
#     && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
#     && echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list \
#     && apt-get update \
#     && apt-get install -y postgresql-client-16 \
#     && apt-get clean \
#     && rm -rf /var/lib/apt/lists/*

# copy the ELT script
COPY elt_script.py .

# set the default command to run the ELT script
CMD [ "python", "elt_script.py" ]