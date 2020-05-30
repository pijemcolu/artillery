# Artillery

Artillery is a load testing application. More info & docs about 
artillery can be found (directly on ther page)[https://artillery.io]

## Docker containers

This repository contains the artillery container image dockerfiles published (on dockerhub)[https://hub.docker.com/r/pijemcolu/artillery]


Run artillery:
```
docker run -it pijemcolu/artillery:ubuntu
```

Available tags:
- `node` - node based container
- `ubuntu` - ubuntu based container

Quick load test as in [artillery docs](https://artillery.io/docs/getting-started/#run-a-quick-test):
```
docker run -it pijemcolu/artillery:ubuntu quick --count 10 -n 20 https://artillery.io/
```

## Azure container instances

To run the container for example in azure with a mounted fileshare containing 
test.yml defining the test further:
```
az container create \
    -g $group \
    -n $containerName\
    --image pijemcolu/artillery:ubuntu \
    --cpu 1 \
    --memory 1 \
    --restart-policy "Never" \
    --azure-file-volume-account-name $storageaccountName \
    --azure-file-volume-account-key $storageKey \
    --azure-file-volume-share-name $fileshareName \
    --azure-file-volume-mount-path /artillery \
    --command-line "artillery run /artillery/test.yml -v '{\"config\": {\"target\": \"$url" }}'" \
    --no-wait
```
