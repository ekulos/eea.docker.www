# Docker orchestration for EEA main portal (development)

Docker orchestration for EEA main portal services (devel)

## Installation

### Setup host

    $ sudo bash
    $ git clone https://github.com/eea/eea.docker.www.git /var/local/deploy/eea.docker.www
    $ cd /var/local/deploy/eea.docker.www/devel
    $ ./setup.sh
    $ su zope-www

### Setup database

    $ docker-compose up -d postgres
    $ docker exec -it devel_postgres_1 bash
      $ gunzip -c /postgresql.backup/datafs.gz | psql -U zope datafs
      $ exit

## Start

    $ docker-compose up -d

See everything is up-and-running

    $ docker-compose ps

## Scale

    $ docker-compose scale plone=4
    $ docker-compose scale async=2

## Access

Replace `XXX.XXX.XXX.XXX` with your machine's public IP.
Optionally add a ngnix entry on swarm-master. See `alin-devel` for an example.


### Site

    http://XXX.XXX.XXX.XXX

### HAProxy Statistics

    http://XXX.XXX.XXX.XXX:1936


## Upgrade

### Docker images

    $ docker-compose pull
    $ docker-compose stop
    $ docker-compose -f docker-remove.yml rm -v
    $ docker-compose up -d --no-recreate
    $ docker-compose logs

### Source code

    $ docker-compose up source_code

### Database

    $ rm backup/datafs.gz
    $ ./setup.sh

    $ docker-compose stop
    $ docker-compose rm -v postgres postgres_data
    $ docker-compose up -d postgres
    $ docker exec -it devel_postgres_1 bash
      $ gunzip -c /postgresql.backup/datafs.gz | psql -U zope datafs
      $ exit

## Debug

As you can not directly add `pdb` anymore within your code, you'll have to use `rpdb`.

Add rpdb breakpoint:

    import rpdb; rpdb.set_trace("0.0.0.0")

Restart Plone container:

    $ docker-compose restart plone
    $ docker-compose logs plone

You'll get something like this within logs when the breakpoint is reached:

    plone_1 | pdb is running on 0.0.0.0:4444

Find your host ip:

    $ ip addr | grep "inet 10" | gawk '{print $2}' | sed "s/\/24//g"

This will return something like:

    10.1.2.3

And now start debugging (replace `10.1.2.3` with your ip address):

    nc 10.1.2.3 4444