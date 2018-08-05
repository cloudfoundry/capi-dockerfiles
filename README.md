# Capi Docker Files

These Docker files are used to build Docker images in our [CI](http://capi.ci.cf-app.com/teams/main/pipelines/docker-images). Those Docker images are then used to create containers in which Concourse tasks are run.

## Building

To manually build a docker image and push to the docker repository:
```
cd ~/workspace/capi-dockerfiles/capi-go-units
docker build -t $(cat repository) .
docker push $(cat repository)
```

