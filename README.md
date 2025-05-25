# Dockerized Node.js App with MongoDB

This repository demonstrates how to set up a simple Docker-based development environment using **Node.js** and **MongoDB**, connected via a custom Docker network.

## 🛠️ Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed on your machine.

---

## 📦 Setup Instructions

#### 1. Create a Custom Docker Network

Create a user-defined bridge network to enable communication between the containers:

```bash
docker network create my_network
```
### 2. Run the MongoDB Container

Start the MongoDB container and connect it to the custom network:

docker run --name mongocontainer \
  --network my_network \
  -p 27017:27017 \
  -v mongo_db_data:/data/db mongo

--name mongocontainer: Assigns a name to the container.

--network my_network: Connects the container to the custom network.

-p 27017:27017: Exposes MongoDB on port 27017.

-v mongo_db_data:/data/db: Persists MongoDB data using a Docker volume.

### 3. Run the Node.js Application Container

Make sure Node.js app is prepared with the appropriate Dockerfile.

Then, run the application container:

docker run --name node_app \
  --network my_network \
  -p 3000:3000 node_app_image

const uri = "mongodb://mongocontainer:27017/your_database";
