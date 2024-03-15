# Nginx Proxy Manager

## Overview

[Homepage](https://nginxproxymanager.com)

## Best practice: Use a Docker network

By creating a custom Docker network, you don't need to publish ports for your upstream services to all of the Docker host's interfaces.

Create a network, ie "nginx-exposed":

```bash
docker network create nginx-exposed
```

Then add the following to the docker-compose.yml file for both NPM and any other services running on this Docker host:

```yaml
networks:
  default:
    external: true
    name: nginx-exposed
```

Now in the NPM UI you can create a proxy host with portainer as the hostname, and port 9000 as the port. Even though this port isn't listed in the docker-compose file, it's "exposed" by the Portainer Docker image for you and not available on the Docker host outside of this Docker network. The service name is used as the hostname, so make sure your service names are unique when using the same network.
