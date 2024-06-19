# Capi Docker Files

These Docker files are used to build Docker images in our [CI](https://concourse.app-runtime-interfaces.ci.cloudfoundry.org/teams/capi-team/pipelines/docker-builds). Those Docker images are then used to create containers in which Concourse tasks are run.

## Building

To manually build a docker image (e.g. capi-ruby-units) and push to the docker repository:
```
cd capi-ruby-units
docker build -t $(cat repository) .
docker push $(cat repository)
```
