# Apache Cassandra

## Introduction

In our lecture, we were tasked with creating a presentation in which we have to show a database, which would stand out from the usual Relational and Document databases. Apache Cassandra is one such database.
Cassandra is set up in a funny middle ground, since it borrows a lot of the same properties you'd be familiar with from the typical Relational-database, it even uses a lot of the same commands as queries.

## The setup process

### Setting up the Database

To set up the database is fairly simple, considering you're using Docker to run it, which I presume you do, as you're here ;)

But to start, you can pull the latest images from Docker run using the following

```console
docker pull cassandra:latest
```

Or just skip it entirely by just running the image directly, along with a network, which we will be using to connect to it later

```console
docker network create cassandra

docker run --rm -d --name cassandra --hostname cassandra --network cassandra cassandra
```

### Connecting to the database

After we've set it up, we can go over to how we'd connect to it. I was looking around for a user interface which we could use to show it off, but every image I could find seemed to be using an outdated
version of Cassandra. So we'll be using CQL (Cassandra Query Language), which is its own language used to make queries. We'll run it like any other docker container and connect to it through the network
we created earlier

#### *Important note*

Mind the version number, if you follow some of the online guides it will be using 3.4.5, which won't be able to access it. For now using 3.4.7 works with this setup.

```console
docker run --rm -it --network cassandra nuvo/docker-cqlsh cqlsh cassandra 9042 --cqlversion='3.4.7'
```

After running this, you'll be prompted with the CQL cli, where you can start using the database.

## Docker Compose

In this repository, we've provided a `docker-compose.yml` which you can easily use to bootup an cassandra instance. It is setup to use the default login credentials, which I'd would ***highly recommend***!

The default credentials are the following
```yml
Username: cassandra
Password: cassandra
```

Once it is up and running, it'll take a few minutes for it to fully start. After it is up, you can connect to it either directly though the host machine using

```console
docker exec -it cassandra cqlsh -u cassandra -p cassandra
```

Or by the CQL as provided earlier

```console
docker run --rm -it --network cassandra-network nuvo/docker-cqlsh cqlsh cassandra 9042 --cqlversion='3.4.7' -u cassandra -p cassandra
```

After that, make sure to alter the password

```console
ALTER USER cassandra WITH PASSWORD 'your_strong_password';
```

## Closing words

And that's it! Now you're up and running with a cool Apache Cassandra database B)

Now go out there and drops some tables <3


