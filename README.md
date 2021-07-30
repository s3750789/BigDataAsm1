# BigDataAsm1
# Set up
docker network create kafka-network 

docker network create cassandra-network  

# Cassandra 
docker-compose -f cassandra/docker-compose.yml up -d --build

cqlsh --cqlversion=3.4.4 127.0.0.1 

use kafkapipeline;

select * from twitterdata;

select * from weatherreport;

select * from fakerdata;
