# Capi Docker Files

These Docker files are used to build Docker images in our [CI](http://capi.ci.cf-app.com/teams/main/pipelines/docker-images). Those Docker images are then used to create containers in which Concourse tasks are run.

If you are looking for the Dockerfile used for the sync-integration-tests, you will find it in the [sync-integration-tests](https://github.com/cloudfoundry/sync-integration-tests/blob/master/concourse/Dockerfile) repository.

## Building

To manually build a docker image and push to the docker repository:
```
cd ~/workspace/capi-dockerfiles/capi-go-units
docker build -t $(cat repository) .
docker push $(cat repository)
```

