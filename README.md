# PostgreSQL 17 with PostGIS for arm64

This image provides tags Postgres with [PostGIS](http://postgis.net/) extensions installed. This image is based on the official [`postgres`](https://registry.hub.docker.com/_/postgres/) image and provides the debian variant for PostGIS 3.5.x. 

This image ensures that the default database created by the parent `postgres` image will have the following extensions installed:

| installed extensions | [initialized](https://github.com/postgis/docker-postgis/blob/master/initdb-postgis.sh)|
|---------------------|-----|
| `postgis`           | yes |
| `postgis_topology`  | yes |
| `postgis_tiger_geocoder` | yes |
| `postgis_raster` | |
| `postgis_sfcgal` | |
| `address_standardizer`| |
| `address_standardizer_data_us`| |

Unless `-e POSTGRES_DB` is passed to the container at startup time, this database will be named after the admin user (either `postgres` or the user specified with `-e POSTGRES_USER`).

Check the documentation on the [`postgres` image](https://registry.hub.docker.com/_/postgres/) and [Docker networking](https://docs.docker.com/network/) for more details and alternatives on connecting different containers.

See [the PostGIS documentation](http://postgis.net/docs/postgis_installation.html#create_new_db_extensions) for more details on your options for creating and using a spatially-enabled database.

## Supported Environment Variables

Since the docker-postgis repository is an extension of the official Docker PostgreSQL repository, all environment variables supported there are also supported here:

* `POSTGRES_PASSWORD`
* `POSTGRES_USER`
* `POSTGRES_DB`
* `POSTGRES_INITDB_ARGS`
* `POSTGRES_INITDB_WALDIR`
* `POSTGRES_HOST_AUTH_METHOD`
* `PGDATA`

Read more:  https://github.com/docker-library/docs/blob/master/postgres/README.md

Warning: **the Docker specific variables will only have an effect if you start the container with a data directory that is empty;** any pre-existing database will be left untouched on container startup.

## Security

It's crucial to be aware that in a cloud environment, with default settings, these images are vulnerable, and there's a high risk of cryptominer infection if the ports are left open. ( [Read More](https://github.com/docker-library/postgres/issues/770#issuecomment-704460980) )
