![](./assets/logo-orange-grey-bar.png)

## What is TapData?

TapData is a live data platform designed to connect data silos and provide fresh data to the downstream data driven applications & analytics. 

<img width="603" alt="image" src="./assets/tapdata-infra.png">

TapData provides two ways to achieve this: Live Data Integration and Live Data Service. 

Live Data Integration is supported by TapData's real time data pipelines based on CDC technology, where you can easily connect and capture all the data plus all the changes from disparate data sources, without any custom coding. TapData supports many data sources out of box, including dozens of popular databases, you may also use TapData's PDK(Plugin Development Kit) quickly add your own data sources. 

Live Data Service is an automatica data API service to allow users instantly create a RESTful API implementation via configuration. TapData will provide API Server to host those API endpoints. The backing data table are stored in a MongoDB cluster which is part of the TapData architecture. The data in MongoDB is typically replicated and processed from disparate data sources, via the Live Data Integration capability.  As an alternative, if your data source allows, you may also create data APIs directly from source databases such as Oracle, MySQL, SQLServer etc. 

The term "live has two meanings:

- When you are using Live Data Integrations, TapData will collect data in a "live" mode means it will listen for the changes on the source database and capture the change immediately and send it to the pipeline for processing and downstream consumption. Sometime this is called CDC technology. The data is always fresh and lively throughout the data pipeline. 

- When you are using Live Data Services, the backing data table is lively updated by TapData Live Data Integration pipelines and stays up-to-date with the source systems.  


## Primary Use Cases

- Heterogeneous Database Replication such as MySQL to MongoDB or ES

- Real Time Data Pipelines, a better alternative to Kafka based data pipelines

- Event-driven Applications, such as fraud detection or event notifications


## How It Works

```
# Create Mysql DataSource
> Demo-Mysql = DataSource("mysql","Demo-Mysql").host("demo-mysql").port(3306).username('root').password('password').db('demo')
> Demo-Mysql.save()

# Create MongoDB DataSource
> Demo-Mongo = DataSource("mongodb","Demo-Mongo").uri("mongodb://root:password@demo-mongo:27017/demo?authSource=admin")
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




## Features

- Build end to end real time data pipelines in minutes
- CDC based data replication, support dozens of popular data sources
- Low latency: sub-second performance compared to seconds with Kafka based solution 
- Built-in incremental data verification
- At least once guarantee
- Developer friendly programmable pipeline API, managing data pipelines using code, not SQL
- Interactive shell, easily create, run and monitor pipelines and manage data services
- Javascript / Python UDF support 
- Integration with Kafka as consumer or producer
- Code-less publish data API, support parameter
- Horizontal scaling
- Highly available pipelines


For more details and latest updates, see [TapData docs](./docs/About TapData/about-tapdata.md) and [release notes](./docs/Release Notes/all-releases.md).

## More Use Cases: Who & When Can Use TapData

#### Application Develoepers

TapData can be used by Application developers in following use cases:

- 「Coming soon in beta」Automatica API backend (Backend as a service) for data CRUD operations
- Code-less CQRS implementation
- Code-less RDBMS caching solution
- Code-less Producer / Consumer for Kafka 
- Mainframe offloading
- Implement CQRS pattern
- Full text search / Graph search 

#### Data Engineers or Data Analysts

For data engineers or data analysts,  TapData can be used as a modern, general purpose, low code ETL platform for various data sync, processing or data modeling activities.

- Data extract / transform / load
- Data processing for data warehouse
- Data modeling
- Kafka-based data integration alternative
- Event streaming platform

#### DBAs / System Engineers

TapData can be used by DBAs in following use cases:

- Heterogeneous database replication
- Real time backup
- Database HA
- Database clustering 
- Disaster Recovery strategy
- Sync to cloud or cross cloud data replication

#### Data Steward

TapData can be used by data stewards in following possible scenarios:

- 「Coming soon in beta」Build an enterprise master data management platform, either as a hub or transactional type
- 「Coming soon in beta」As a metadata management solution
- 「Coming soon in beta」As a data as a service platform to facilitate fast data distribution to BUs


## Road Map

- Open metadata compatibility 
- Improved event cache store
- More pre-built processors
- Support more data store solution in addition to MongoDB
- Aggregation framework on data pipeline
- Java SDK


## Community

You can join these groups and chats to discuss and ask TapData related questions:

- [WeChat Channel](https://www.tapdata.net) （todo）

In addition, you may enjoy following:

- Question in the Github Issues
- The TapData Team [Blog](https://tapdata.net/blog.html) 

For support, please contact [TapData](https://tapdata.net/tapdata-enterprise/demo.html). (todo: a brand new contact us page)

## Quick start

### To start using TapData

See [Quick Start Guide](./docs/Quick Start/quick-start.md). 

### To start using TapData Cloud

We provide TapData Cloud - a fully-managed Data Replication and Migration Service for you. You can [sign up](https://auth.tapdata.net/login) and get started with TapData Cloud Free Tier.

See [TapData Cloud Quick Start](https://tapdata.net/docs-tapdata-cloud.html).

## 「WIP」Contributing

The [community repository](https://github.com/tapdata/community) hosts all information about the TapData community, including how to contribute to TapData, how TapData community is governed, how special interest groups are organized, etc.

Contributions are welcomed and greatly appreciated. See [Contribution to TapData](./docs/contribution-to-tapdata.md) for details on typical contribution workflows. 



## Case studies

- [MySQL to MySQL](./docs/Case Study/ETL/mysql-to-mysql.md)
- [MySQL to MongoDB](./docs/Case Study/ETL/mysql-to-mongodb.md)
- [MongoDB to MongoDB](./docs/Case Study/ETL/mongodb-to-mongodb.md)

## 「WIP」License

TapData is under the SSPL v1 license. See the [LICENSE](./LICENSE.txt) file for details. (Copy from mongodb need modify)
