# Cheatsheet with useful Docker/Kubectl commands

### Building the docker image, tagging it as "axondb-single"
```
docker build ./docker -t axondb-single
```

### Running the docker image locally, exposing the ports on localhost for direct use by an application.
```
docker run --rm -p8023:8023 -p8123:8123 -m 1G -e axoniq.axondb.hostname=localhost axondb-single
```

### Running the docker image locally, for use in combination with AxonHub.
The data connection won't go through the host, but over the container network.
```
docker run --rm -p8023:8023 -m 1G --name axondb -h axondb axondb-single
```


### Setting the prefix for the docker repository
(This is assumed to have been done in the following commands.)
```
export DOCKER_IMAGE_PREFIX=<set as appropriate>
```

### Pushing the docker image to the google container repo
```
docker tag axondb-single $DOCKER_IMAGE_PREFIX/axondb-single
docker push $DOCKER_IMAGE_PREFIX/axondb-single
```

### Running on Kubernetes. This will also do an expand of $DOCKER_IMAGE_PREFIX in the yaml.
```
envsubst <axondb-single.yaml | kubectl apply -f -
```

### Removing everything from Kubernetes.
```
kubectl delete statefulsets/axondb service/axondb service/axondb-gui pvc/data-axondb-0
```
