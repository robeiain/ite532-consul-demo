# coffee-service
Coffee API written in Go

[![CircleCI](https://circleci.com/gh/hashicorp-demoapp/coffee-service.svg?style=svg)](https://circleci.com/gh/hashicorp-demoapp/coffee-service)

Docker Image: [https://hub.docker.com/r/hashicorpdemoapp/coffee-service](https://hub.docker.com/r/hashicorpdemoapp/coffee-service)

## Running locally

Instructions:
1. Make sure Consul is available locally `docker pull consul:latest`
2. Stop local DNS resolution `systemctl stop systemd-resolved`
3. Edit the DNS config file to look at the local host for DNS lookups `nano /etc/resolv.conf` and change the address `127.0.0.53` to `127.0.0.1`
4. Run Consul in host mode with DNS `docker run -d -e CONSUL_ALLOW_PRIVILEGED_PORTS=yes --net host --name consul consul agent -bootstrap -server -dns-port=53 -bind=10.0.0.120 -recursor=8.8.8.8`
5. `docker pull hashicorpdemoapp/coffee-service:v0.0.1`
6. Run the coffee app `docker run -d -p 9090:9090 --env BIND_ADDRESS=localhost:9090 --env VERSION=v3 --env LOG_LEVEL=DEBUG --name=coffee-service hashicorpdemoapp/coffee-service:v0.0.1`
7. Register the coffee app with Consul using the REST API (where the address is the IP address of your coffee instance from `docker inspect coffee-service`) `curl -X PUT -d '{"ID": "Coffee", "Name": "App", "Address": "172.17.0.2"}' http://localhost:8500/v1/agent/service/register`
8. Can you now `ping coffee.consul.service`
