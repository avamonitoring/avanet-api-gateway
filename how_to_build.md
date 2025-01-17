# How to build krakend for use with AvaNet

## Prerequisite

Clone 
* https://github.com/avamonitoring/avanet-gateway-access-control
* https://github.com/avamonitoring/avanet-gateway-access-logging
* https://github.com/avamonitoring/lura

into the same parent directory as this repo.

## Build

```
docker run --rm -it -v //c/path/to/avanet-api-gateway:/go/github.com/avamonitoring/avanet-api-gateway -v //c/path/to/avanet-gateway-access-logging:/go/github.com/avamonitoring/avanet-gateway-access-logging -v //c/path/to/avanet-gateway-access-control:/go/github.com/avamonitoring/avanet-gateway-access-control -v //c/path/to/lura:/go/github.com/avamonitoring/lura golang:1.18.1

cd /go/github.com/avamonitoring/avanet-api-gateway
make build
```

(`Makefile` has `build_on_docker` with `GOLANG_VERSION` = 1.17.9 and `go.mod` indicates 1.17.)

## Build Docker image

The build above will put `krakend` binary and this directory.

Thereafter, do
```
sudo docker build . -t 059741451001.dkr.ecr.eu-north-1.amazonaws.com/krakend:my_tag
```
You can also do
```
sudo make docker
```

## Pushing the image

Authenticate against AWS ECR
```
aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin 059741451001.dkr.ecr.eu-north-1.amazonaws.com
```

Push the image
```
docker push 059741451001.dkr.ecr.eu-north-1.amazonaws.com/krakend:my_tag
```
