## Installation

```
brew install docker
brew install docker-machine
docker-machine create --driver virtualbox default
eval "$(docker-machine env default)"
docker login
```

## Building

```
cd ~/workspace/capi-dockerfiles/capi-go-units
docker build -t $(cat repository) .
docker push $(cat repository)
```

