#docker #networks #subnet #ipam

When working with Docker Compose, you can define and configure networks for your containers. This includes setting up subnets for different network segments. Below is an example of how to declare a subnet in a `docker-compose.yml` file.

``` bash
docker network create --driver=bridge --subnet=<subnet> --gateway=<gateway> <subnet_network>
```

``` yaml
version: '3'
services:
  # Your service definitions.

networks:
  subnet_network:
    name: "subnet_network"
    driver: "bridge"
    # It can either be external or internal.
    external: true
    ipam:
      config:
        # An example of subnet could be "192.168.210.0/24".
        - subnet: "XXX.XXX.XXX.XXX/24"
```
