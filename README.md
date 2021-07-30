# BigDataAsm1
# Set up
docker network create kafka-network 

docker network create cassandra-network  

# Cassandra 
docker-compose -f cassandra/docker-compose.yml up -d --build

cqlsh -f schema-faker.cql

cqlsh -f schema-ghibli.cql

cqlsh --cqlversion=3.4.4 127.0.0.1 

use kafkapipeline;

select * from twitterdata;

select * from weatherreport;

select * from fakerdata;

select * from ghiblidata;

# Kafka
docker-compose -f kafka/docker-compose.yml up -d --build

# Producer 
docker-compose -f faker-producer/docker-compose.yml up -d

docker-compose -f owm-producer/docker-compose.yml up -d 

docker-compose -f twitter-producer/docker-compose.yml up

docker-compose -f ghibli-producer/docker-compose.yml up -d
# Consumer
cd .\consumers\   =====>    docker build -t twitterconsumer .

cd ..             =====>    docker-compose -f consumers/docker-compose.yml up --build

# Visual 
docker-compose -f data-vis/docker-compose.yml up -d --build

# Tear down
docker-compose -f data-vis/docker-compose.yml down              # data-vis

docker-compose -f consumers/docker-compose.yml down             # consumers   

docker-compose -f owm-producer/docker-compose.yml down          # open weather

docker-compose -f faker-producer/docker-compose.yml down        # faker-producer

docker-compose -f ghibli-producer/docker-compose.yml down       # ghibli-producer

docker-compose -f twitter-producer/docker-compose.yml down      # twitter-producer

docker-compose -f kafka/docker-compose.yml down                  

docker-compose -f cassandra/docker-compose.yml down          

docker system prune -a
