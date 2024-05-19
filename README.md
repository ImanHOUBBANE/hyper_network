# Hyper Network
Create two containers: one running Adminer and the other running a PostgreSQL database, and set up communication between them.

#Creation of volume
docker volume create hyper-volume

#Creation of network
docker network create hyper-network

#Pull PostgreSQL image
docker pull postgres:15.3

#Verification of containers
docker container ps

#Create PostgreSQL container with specified settings
docker run --name hyper-postgres -e POSTGRES_PASSWORD=hyper2023 -e POSTGRES_USER=hyper -e POSTGRES_DB=hyper-db -p 5432:5432 --network hyper-network --volume hyper-volume:/var/lib/postgresql/data -d postgres:15.3

#Pull Adminer image
docker pull adminer:4.8.1

# Create Adminer container
docker run --name hyper-adminer -p 8080:8080 --network hyper-network -d adminer:4.8.1

# Stop and delete the hyper-postgres container
docker container stop hyper-postgres
docker container rm hyper-postgres

# Stop and delete the hyper-adminer container
docker container stop hyper-adminer
docker container rm hyper-adminer

# Delete the hyper-network network
docker network rm hyper-network

# Delete the hyper-volume volume
docker volume rm hyper-volume

