# coffee-service
Coffee API written in Go

[![CircleCI](https://circleci.com/gh/hashicorp-demoapp/coffee-service.svg?style=svg)](https://circleci.com/gh/hashicorp-demoapp/coffee-service)

Docker Image: [https://hub.docker.com/r/hashicorpdemoapp/coffee-service](https://hub.docker.com/r/hashicorpdemoapp/coffee-service)

## Running locally

Instructions:
1. Run Consul in host mode with DNS 'docker run -d --net=host -e 'CONSUL_ALLOW_PRIVILEGED_PORTS=' consul -dns-port=53 -recursor=8.8.8.8'
2. 'docker pull hashicorpdemoapp/coffee-service:v0.0.1'
3. Run the coffee app `docker run -d -p 9090:9090 --env BIND_ADDRESS=localhost:9090 --env VERSION=v3 --env LOG_LEVEL=DEBUG --name=coffee-service hashicorpdemoapp/coffee-service:v0.0.1`
4. Register the coffee app with Consul using the REST API (where the address is the IP address of your coffee instance from 'docker inspect coffee-service') 'curl -X PUT -d '{"ID": "Coffee", "Name": "App", "Address": "172.17.0.5"}' http://localhost:8500/v1/agent/service/register'
5. Can you now 'ping coffee.consul.service'
