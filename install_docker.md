## Create a new Virtual Machine with Docker Enterprise Edition installed

1. `vagrant up`
2. `vagrant ssh`
3. If this is a new VM update, upgrade and reboot:
  - `sudo apt-get update && sudo apt-get dist-upgrade -yy && exit`
  - `vagrant reload`
  - `vagrant ssh`
3. Export your Docker EE URL, example:
  - `export DOCKER_EE_URL=<https://storebits.docker.com/ee/ubuntu/sub-xxxxx-xxxxx-xxxxx-xxxx-xxxxx-xxx>`
4. `sh /vagrant/install_docker.sh`
5. Reboot (sanity check that all is good)
  - `exit`
  - `vagrant reload`
  - `vagrant ssh`
7. Install Docker UCP (note the version, this will require upgrading over time)

*Note*: The install will prompt you for an Admin name and Admin Password.

*Note*: Hit Enter (no value) when prompted for *Additional aliases (SANs)*.

```
docker container run --rm -it --name ucp \
  -v /var/run/docker.sock:/var/run/docker.sock \
  docker/ucp:2.2.4 install \
  --host-address 192.168.88.10 \
  --interactive
```

5. Login to UCP at [https://192.168.88.10:443](https://192.168.88.10:443)
