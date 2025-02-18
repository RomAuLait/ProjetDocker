```docker network create \
  --driver bridge \
  --subnet=172.1.1.0/24 \
  MyBridgedNetwork
  ```

```
docker run -d \
  --name nginx-container \
  --network MyBridgedNetwork \
  nginx

```

```
  docker exec -it nginx-container bash

```

```
  echo "Projet docker Remy" > /usr/share/nginx/html/index.html

```

```
  docker commit nginx-container my-custom-nginx

```

```
  docker stop nginx-container && docker rm nginx-container
docker run -d \
  --name nginx-container \
  --network MyBridgedNetwork \
  my-custom-nginx

```
```
  docker volume create bdd

```

```
  docker run -d \
  --name mongodb-container \
  --network MyBridgedNetwork \
  -v bdd:/data/db \
  mongo

```

```
  docker run -d \
  --name mongo-express \
  --network MyBridgedNetwork \
  -e ME_CONFIG_MONGODB_SERVER=mongodb-container \
  -p 8081:8081 \
  mongo-express

```

```
  docker network create \
  --driver bridge \
  --subnet=172.2.2.0/24 \
  BCNetwork

```

```
    FROM ethereum/client-go:latest

# Configurer les options du nœud
CMD ["--dev", "--http", "--http.addr", "0.0.0.0", "--http.port", "8545"]

```

```
    docker build -t my-ethereum-node .

```

```
    docker tag my-ethereum-node <Romaulait>/my-ethereum-node
docker push <Romaulait>/my-ethereum-node

```

```
    docker volume create blockchain

```

```
docker run -d \
  --name eth-node \
  --network BCNetwork \
  -v blockchain:/root/.ethereum \
  my-ethereum-node

```