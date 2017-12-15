# Install Docker Registry (non DTR)

<!--

## Local Mac OS

1. `docker-machine create --engine-insecure-registry 192.168.88.10:5000 -d virtualbox --virtualbox-hostonly-cidr 192.168.99.1/24 --virtualbox-memory '1024' --virtualbox-boot2docker-url https://releases.rancher.com/os/latest/rancheros.iso demo1`

## Docker Trusted Registry

1. `docker run -it --rm docker/dtr:2.2.6 install --ucp-node 192.168.88.10 --ucp-insecure-tls`
-->

## Run a Docker Registry

1. `docker run -d -p 5000:5000 --restart=always --name registry registry:2`
2. `curl 192.168.88.10:5000/v2/_catalog`

Expose the registry (development only insecure)

3. Create file `/etc/docker/daemon.json`

```
{
  "insecure-registries" : ["192.168.88.10:5000"]
}
```

4. `sudo cat /etc/docker/daemon.json`
5. `sudo service docker restart`

Secure registry docs at  [https://docs.docker.com/registry/deploying/](https://docs.docker.com/registry/deploying/)

Push to the Registry via command line

6. `docker tag demo-app:1.0.0 192.168.88.10:5000/demo-app:1.0.0`
7. `docker push 192.168.88.10:5000/demo-app:1.0.0`
