# *
# * This Source Code Form is subject to the terms of the Mozilla Public
# * License, v. 2.0. If a copy of the MPL was not distributed with this
# * file, You can obtain one at http://mozilla.org/MPL/2.0/.
# *

# Dockerfile for OED Postgres server.
# Use a pinned version
FROM postgres:15.3

RUN apt-get update \
 && apt-get install -y --no-install-recommends gnupg ca-certificates wget lsb-release \
 && echo "deb https://packagecloud.io/timescale/timescaledb/debian/ $(lsb_release -cs) main" > /etc/apt/sources.list.d/timescaledb.list \
 && wget -qO- https://packagecloud.io/timescale/timescaledb/gpgkey | gpg --dearmor > /etc/apt/trusted.gpg.d/timescaledb.gpg \
 && apt-get update \
 && apt-get install -y --no-install-recommends timescaledb-2-postgresql-15 timescaledb-tools \
 && rm -rf /var/lib/apt/lists/*

# All SQL files in the build context
# get copied into the container and
# run on init.
COPY *.sql /docker-entrypoint-initdb.d/
