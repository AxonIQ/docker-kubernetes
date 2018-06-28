# Cheatsheet with useful Docker/Kubectl commands

### Building the docker image, tagging it as "axondb-single"
```
docker build ./docker -t axonhub-single
```

### Running the docker image locally, exposing the ports on localhost
See the README.md in the axondb-single directory on how to start the assumed axondb container.
```
docker run --rm -p8024:8024 -p8124:8124 -m 1G -e axoniq.axonhub.hostname=localhost -e axoniq.axondb.servers=axondb axonhub-single
```

### Setting the prefix for the docker repository
(This is assumed to have been done in the following commands.)
```
export DOCKER_IMAGE_PREFIX=<set as appropriate>
```

### Pushing the docker image to the google container repo
```
docker tag axonhub-single $DOCKER_IMAGE_PREFIX/axonhub-single
docker push $DOCKER_IMAGE_PREFIX/axonhub-single
```

### Running on Kubernetes. This will also do an expand of $DOCKER_IMAGE_PREFIX in the yaml.
```
envsubst <axonhub-single.yaml | kubectl apply -f -
```

### Removing everything from Kubernetes.
```
kubectl delete statefulsets/axonhub service/axonhub service/axonhub-gui pvc/data-axonhub-0
```
