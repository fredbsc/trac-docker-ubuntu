# trac-docker

[![](https://images.microbadger.com/badges/version/stephenhsu/trac.svg)](https://hub.docker.com/r/stephenhsu/trac/ "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/stephenhsu/trac.svg)](https://hub.docker.com/r/stephenhsu/trac/)
[![Docker Hub](http://img.shields.io/docker/pulls/stephenhsu/trac.svg)](https://hub.docker.com/r/stephenhsu/trac/)

This repo is used to host a bunldle to create a docker container (based on
Ubuntu Xenial) running [Trac](http://trac.edgewall.org),
which is an enhanced wiki and issue tracking system for software development
projects. Trac uses a minimalistic approach to web-based software project
management. It helps developers write great software while staying out of
the way. Trac should impose as little as possible on a team's established
development process and policies.


# How to get the image

* Build it using Dockerfile

    ```ssh
    $ git clone https://github.com/dixudx/trac-docker
    $ cd trac-docker
    $ docker build -t trac ./
    ```

* just pull it from Dockerhub

    ```
    $ docker pull stephenhsu/trac
    ```


# How to run the container

## Quick Start

Just run

```
$ docker run -d -p 8123:8123 --name my_trac stephenhsu/trac
```

After several seconds, you can visit the web page at
<http://localhost:8123>

## Environment Variables Explanations

Most of below

* `TRAC_ADMIN_NAME` (default is `trac_admin`):

    the admin username of Trac

* `TRAC_ADMIN_PASSWD` (default is `passw0rd`):

    the admin password of Trac

* `TRAC_PROJECT_NAME` (default is `trac_project`):

    the Trac project name

* `TRAC_DIR` (default is `/var/local/trac`):

    This directory stores all the data and configurations. You can bind a volume
    when starting a container.

* `TRAC_INI` (default is `$TRAC_DIR/conf/trac.ini`):

    This ini file will be automatically generated by the container.
    Also you can made some customizations based on your needs.

* `DB_LINK` (default is `sqlite:db/trac.db`):

    A database system is needed. The database can be either `SQLite`,
    `PostgreSQL` or `MySQL`.

    Please refer <https://trac.edgewall.org/wiki/TracInstall#MandatoryDependencies>
    for more detailed infomation.

    * For the PostgreSQL database

        See [DatabaseBackend](https://trac.edgewall.org/intertrac/DatabaseBackend%23Postgresql) for details.

    * For the MySQL database

        Trac works well with MySQL.
        Given the caveats and known issues surrounding MySQL,
        read the [MySqlDb](https://trac.edgewall.org/intertrac/MySqlDb) page
        before creating the database.


## Wants More Secure

This container image is powered by [Apache Web Server](https://httpd.apache.org/).
You can make your own customizations (such as adding TLS etc.) in
`./trac.conf` and map to `/etc/apache2/sites-available/trac.conf` when
starting a container.

```
$ docker run -d -p 8123:8123 -v ./trac.conf:/etc/apache2/sites-available/trac.conf --name my_trac stephenhsu/trac
```

# Reference

* [Trac Official Doc](https://trac.edgewall.org/wiki/TracGuide)