# coffee-service
Coffee API written in Go

[![CircleCI](https://circleci.com/gh/hashicorp-demoapp/coffee-service.svg?style=svg)](https://circleci.com/gh/hashicorp-demoapp/coffee-service)

Docker Image: [https://hub.docker.com/r/hashicorpdemoapp/coffee-service](https://hub.docker.com/r/hashicorpdemoapp/coffee-service)

## Running locally

Instructions:
1. Install Consul with DNS support from previous exercise.
2. `docker pull hashicorpdemoapp/coffee-service:v0.0.1`
3. Run the coffee app `docker run -d  --net datacenter-deploy-dns_vpcbr -p 9090:9090 --env BIND_ADDRESS=localhost:9090 --env VERSION=v3 --env LOG_LEVEL=DEBUG --name=coffee-service hashicorpdemoapp/coffee-service:v0.0.1`
4. Register the coffee app with Consul using the REST API (where the address is the IP address of your coffee instance from `docker inspect coffee-service`) `curl -X PUT -d '{"ID": "Coffee", "Name": "Coffee", "Address": "10.17.0.2"}' http://localhost:8500/v1/agent/service/register`
8. Can you now `ping coffee.service.consul`?
9. We should now be able to access the container from within another container (note - we need to be in the same network segment as the systems we're trying to access):

docker run -it --rm --dns 10.5.0.2 --net datacenter-deploy-dns_vpcbr busybox ping coffee.service.consul
