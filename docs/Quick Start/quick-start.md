# Quick Start

Maintainer: @Edison

This guide walks you through the quickest way to get started with TapData using [Docker Compose](https://github.com/docker/compose) , and will show a sample of the datamovement from MySQL to MongoDB in Real-Time.

You can also deploy your TapData by either of the following methods:

- Git
- Docker

Please refer to [Installation](../Deployment/install-and-start.md) for steps. 

## Prerequisites

Make sure [Docker](https://www.docker.com/) and [Docker Compose](https://github.com/docker/compose) has been successfully installed. 



## Let's make data on tap!

1. Install  

```
# Download the quick start docker-compose file
curl -O ./docker-compose.yml https://xxx.xx.xx/tapdata/tapdata-quick-start-compose.yml

# Get start!
docker-compose up -d
```



2. Check the service status

```
docker-compose ps

docker-compose exec tapdata tapdata status
```



3. Create TapData DataSource & Job to transform the Data from mysql to mongoDB.

```
# Login to TapData using ishell
docker-compose exec ishell ishell 

# Demo Database is 'demo'
# Demo Table is 'Customer'

# Create Mysql DataSource
> Demo-Mysql = DataSource("mysql","Demo-Mysql").host("demo-mysql").port(3306).username('root').password('root').db('demo')
> Demo-Mysql.save()

# Create MongoDB DataSource
> Demo-Mongo = DataSource("mongodb","Demo-Mongo").uri("mongodb://root:root@demo-mongo:27017/demo?authSource=admin")
> Demo-Mongo.save()

# Create a job that transform the Customer table in Mysql to  MongoDB  and add/set filed 'updated' at the same time.
> Demo-job = Pipeline("Demo-job").readFrom(Demo-Mysql.Customer).js('record["updated"]=new Date() ;return record;').writeTo(Demo-Mongo.Customer-v1)

> Demo-job.start()

# Check the status of job
> show jobs
> monitor job Demo-job

# Check the log of job
> logs job Demo-job limit=5 tail=True 


```



4. Feel the data flow

```


# Insert a record in mysql  and see what gonna happen
docker-compose exec mysql-demo mysql 

Mysql > use demo
Mysql > select * from Customer;
Mysql > insert into Customer values(1009,"Edison",30,"China")

# Check the new data in mongo
docker-compose exec mongo-demo mongo

MongoDB > use demo
MongoDB > db.Customer-v1.find()

# Update a record in mysql and see what gonna happen
docker-compose exec mysql-demo mysql

Mysql > use demo
Mysql > select * from Customer;
Mysql > update Customer set age = 30 where id=1009;

# Check the new data in mongo
docker-compose exec mongo-demo mongo

MongoDB > use demo
MongoDB > db.Customer-v1.find({id:1009})

```







